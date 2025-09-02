---
title: Setting up your environment
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
  pages:
    - type: basic
      slug: the-first-shipment
      title: The first shipment
---
## Credentials

Before you can start using the Carrier Connect API, you need a user and a password.

If you do not have your own client yet, you can use the following credentials to test the API.

*REST*\
[https://rz3.aeb.de/demo1cai/rest/swagger.json](https://rz3.aeb.de/demo1cai/rest/swagger.json)

*SOAP*\
[https://rz3.aeb.de/demo1cai/servlet/bf/DLCarrierBF?WSDL](https://rz3.aeb.de/demo1cai/servlet/bf/DLCarrierBF?WSDL)\
[https://rz3.aeb.de/demo1cai/servlet/bf/doc/DLCarrierBF/de/aeb/xnsg/dl/bf/IDLCarrierBF.html](https://rz3.aeb.de/demo1cai/servlet/bf/doc/DLCarrierBF/de/aeb/xnsg/dl/bf/IDLCarrierBF.html)

Client: APITEST\
User: API\_TEST\
PW: API\_TEST2018

The API is only available via Secure Socket Layer (SSL).

> ❗️ The client APITEST is intended for basic connectivity testing and is used by different users. Don't use it with sensitive data.

## REST Authentication

First you have to request an authentication token by using the URL [https://rz3.aeb.de/demo1cai/rest/logon/user](https://rz3.aeb.de/demo1cai/rest/logon/user)

```json
{
	"clientName": "APITEST",
	"userName": "API_TEST",
	"password": "API_TEST_007",
	"localeName": "en",
	"isExternalLogon": "true"
}
```

You will then get a token back, which you have to use as request header in the subsequent requests (see X-XNSG\_WEB\_TOKEN).

```http
POST /demo1cai/rest/DLCarrierBFBean/createShipment HTTP/1.1
Host: rz3.aeb.de
Connection: keep-alive
Content-Length: 275
accept: application/json
Origin: https://rz3.aeb.de
X-XNSG_WEB_TOKEN: eyJlbmdpbmVJZCI6IjUwMzE2OTEwNF9XbVZ3VGV4YWVGIiwiaWQiOiJVU0VSX0NMSUVOVCJ9.eyJ1c2VyTmFtZSI6IldTTSIsImNsaWVudElkZW50Q29kZSI6IlVOSVRFREIifQ==.AwgakGOMN0IRJo6cGkVS1DXpbGOozG7o8vQD3DEalYb2oE0qRUmifyh9vfms1NWeMwTJUpelRo9fLy5eSm92k+vull2q3GJfhkVT7Oqa9HUobIZFSDVPL4z5++ovnemuyuz2qZdTXHP6qPepk+DV2WTitam0zgNGAJidGBUK/Q4=
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36
content-type: application/json
Referer: https://rz3.aeb.de/demo1cai/swagger/index.jsp
Accept-Encoding: gzip, deflate, br
Accept-Language: de-DE,de;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: JSESSIONID=2FAF58F26389F7CF95AA9E2778136C52.test2ici_node1
```

## SOAP Authentication

Authentication data must be provided for every call. It is expected as an HTTP authentication (HTTP basic protocol). The user and client login data is transmitted in the format `<user>@<client>:<password>`.\
The login data must be base 64–encoded. The password is written out, so this is why we require using HTTPS encryption and the data cannot be intercepted by unauthorized parties.\
Example:\
User = API\_TEST\
Client = APITEST\
Password = API\_TEST\_007\
The string "API\_TEST\@APITEST:API\_TEST\_007", when encoded in base 64, yields “QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVF8wMDc=". The following line would therefore be added to the HTTP header:\
Authorization: Basic QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVF8wMDc=