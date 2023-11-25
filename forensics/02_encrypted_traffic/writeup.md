### Encrypted traffic
Level: Easy

Rus: В нашей компании произошла утечка. Узнайте каким образом злоумышленник слил информацию.

Eng: There was a leak in our company. Find out how the attacker leaked the information.

### Solution

We download zip archive from the task page and extract it. There is file flag.jpg, but it can not be opened as image.
```
┌──(root㉿kali)-[/home]
└─$ file flag_fake_evidence.jpg 
flag_fake_evidence.jpg: PDF document, version 1.7, 1 pages
                                                                                                                                                            
┌──(root㉿kali)-[/home]
└─$ pdf2john flag_fake_evidence.pdf > hash.txt
                                                                                                                                                            
┌──(root㉿kali)-[/home]
└─$ cat hash.txt
flag_fake_evidence.pdf:$pdf$2*3*128*-4*1*16*8f60187c054e0f37214505597f60c66c*32*46836cbd0c5fb6a9dd452481954ee90428bf4e5e4e758a4164004e56fffa0108*32*0c34c06e3dc37eb2362a2f87cf65e65551a6eb55c7306d969d7bc440f80e3193
                                                                                                                                                            
                                                                                                                                                            
┌──(root㉿kali)-[/home]
└─$ john --wordlist=/home/ekt/Desktop/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (PDF [MD5 SHA2 RC4/AES 32/64])
Cost 1 (revision) is 3 for all loaded hashes
Will run 6 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
147258369        (flag_fake_evidence.pdf)     
1g 0:00:00:00 DONE (2023-11-18 06:38) 9.090g/s 5236p/s 5236c/s 5236C/s bond007..yankee
Use the "--show --format=PDF" options to display all of the cracked passwords reliably
Session completed. 
```

Open pdf with password, and flag will be there.

get flag in the response: CODEBY{D0N'T_ST0R3_TH3_FL4G_1N_4_PDF}