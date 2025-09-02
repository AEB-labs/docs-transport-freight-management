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

*REST*
https://rz3.aeb.de/demo1cai/rest/swagger.json 

*SOAP*
https://rz3.aeb.de/demo1cai/servlet/bf/DLCarrierBF?WSDL
https://rz3.aeb.de/demo1cai/servlet/bf/doc/DLCarrierBF/de/aeb/xnsg/dl/bf/IDLCarrierBF.html

Client: APITEST
User: API_TEST
PW: API_TEST2018

The API is only available via Secure Socket Layer (SSL).
[block:callout]
{
  "type": "danger",
  "body": "The client APITEST is intended for basic connectivity testing and is used by different users. Don't use it with sensitive data."
}
[/block]
## REST Authentication 
First you have to request an authentication token by using the URL https://rz3.aeb.de/demo1cai/rest/logon/user
[block:code]
{
  "codes": [
    {
      "code": "{\n\t\"clientName\": \"APITEST\",\n\t\"userName\": \"API_TEST\",\n\t\"password\": \"API_TEST_007\",\n\t\"localeName\": \"en\",\n\t\"isExternalLogon\": \"true\"\n}",
      "language": "json"
    }
  ]
}
[/block]
You will then get a token back, which you have to use as request header in the subsequent requests (see X-XNSG_WEB_TOKEN).
[block:code]
{
  "codes": [
    {
      "code": "POST /demo1cai/rest/DLCarrierBFBean/createShipment HTTP/1.1\nHost: rz3.aeb.de\nConnection: keep-alive\nContent-Length: 275\naccept: application/json\nOrigin: https://rz3.aeb.de\nX-XNSG_WEB_TOKEN: eyJlbmdpbmVJZCI6IjUwMzE2OTEwNF9XbVZ3VGV4YWVGIiwiaWQiOiJVU0VSX0NMSUVOVCJ9.eyJ1c2VyTmFtZSI6IldTTSIsImNsaWVudElkZW50Q29kZSI6IlVOSVRFREIifQ==.AwgakGOMN0IRJo6cGkVS1DXpbGOozG7o8vQD3DEalYb2oE0qRUmifyh9vfms1NWeMwTJUpelRo9fLy5eSm92k+vull2q3GJfhkVT7Oqa9HUobIZFSDVPL4z5++ovnemuyuz2qZdTXHP6qPepk+DV2WTitam0zgNGAJidGBUK/Q4=\nUser-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36\ncontent-type: application/json\nReferer: https://rz3.aeb.de/demo1cai/swagger/index.jsp\nAccept-Encoding: gzip, deflate, br\nAccept-Language: de-DE,de;q=0.9,en-US;q=0.8,en;q=0.7\nCookie: JSESSIONID=2FAF58F26389F7CF95AA9E2778136C52.test2ici_node1",
      "language": "http"
    }
  ]
}
[/block]
## SOAP Authentication 
Authentication data must be provided for every call. It is expected as an HTTP authentication (HTTP basic protocol). The user and client login data is transmitted in the format <user>@<client>:<password>.
The login data must be base 64–encoded. The password is written out, so this is why we require using HTTPS encryption and the data cannot be intercepted by unauthorized parties.
Example:
User = API_TEST
Client = APITEST
Password = API_TEST_007
The string "API_TEST@APITEST:API_TEST_007", when encoded in base 64, yields “QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVF8wMDc=". The following line would therefore be added to the HTTP header:
Authorization: Basic QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVF8wMDc=