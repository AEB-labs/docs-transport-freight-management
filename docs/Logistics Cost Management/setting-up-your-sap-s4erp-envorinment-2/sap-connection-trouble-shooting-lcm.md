---
title: SAP connection trouble shooting (LCM)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
You had issues with establishing a connection from your SAP to our data center? 
You should check the following prerequisites:
- When accessing the AEB data center, an HTTPS service must be running (you can access the list of services using transaction SMICM).
- When creating via SOAMANGER and using HTTPS, the certificates must be loaded into the SSL-CLIENT (Anonymous) node. (Transaction STRUST)
- The SAPCRYPTOLIB or COMMON Crypto DLL must be installed and active in the version according to the system requirements. (Transaction STRUST)
- In most cases, errors when calling the Web service are logged in the ICM log. You can open this log in transaction SMICM. (Alternatively, you can open the file "dev.icm" in transaction ST11). 

There are some known errors and solutions:
[block:parameters]
{
  "data": {
    "h-0": "Issue/Error",
    "h-1": "Solution",
    "0-0": "\"GET_BUSINESS_SYSTEM_ERROR An error occurred when determining the business system (SLD_API_EXCEPTION)\"",
    "0-1": "Check the logical port in transaction LPCONFIG. Is it created and linked to the correct HTTP connection?  No standard port must be defined for the proxy class.",
    "1-0": "Only a green tick appears in the connection test in the SM59 for an SSL connection.",
    "1-1": "The service for HTTPS is not running.",
    "2-0": "'HTTPIO_PLG_CANCELED'",
    "2-1": "There is probably no service available for the required process (HTTP or HTTPs) or these are not active. \nAlso to be checked: Is the connection in the SM59 really of type G? Are all PSEs in the STRUST below the SSL client green?",
    "3-0": "'Create failed: Argument not found'",
    "3-1": "The problem could be related to the service port - is there the correct port, for example 443', or is there a typing error (e.g. space)? \nThere may also be something wrong with the SSL client stored in the destination. Check it in the STRUST - is this SSL client in 'green' status? Are the AEB certificates also installed there?",
    "4-0": "'ICM_HTTP_SSL_ERROR'",
    "5-0": "  * 'ICM_CONNECTION_FAILED' and in log file dev.icm the error 'NIECONN_REFUSED' occurs. ",
    "4-1": "The problem may be related to the SSL certificates. Are all required certificates installed in the STRUST? Has the ICM been restarted to reload them?\nThe correct [SSL certificate](https://cybernews.com/resources/web-hosting-glossary/#ssl-tls) list must still be entered in the connection. \nA fixed IP address has been entered in the destination. For connections to the AEB computer center, the host must be rz3.aeb.de.",
    "5-1": "The name resolution for the host address \"rz3.aeb.de\" does not work because DNS is not set correctly. \nThe problem could also be related to the fact that a proxy is required to connect to external websites. If this is the case, the proxy parameters must be stored in the SM59 destination.",
    "6-0": "'ICM_HTTP_CONNECTION_FAILED' and in log file dev.icm the error 'NIECONN_REFUSED' occurs.",
    "6-1": "This may be because the destination forgot to activate SSL. The correct SSL client certificate must also be selected there.\n\nThe firewall may block the connection to the target system. It is possible that the port of the target system is not released.",
    "7-0": "ICM_HTTP_CONNECTION_FAILED' always occurs.",
    "7-1": "Several possible causes. The problem could be related to the port entered in the SM59. Is the correct HTTPS port 443 or the correct HTTP port of the target system stored there? Or is a proxy required for connections?",
    "8-0": "ICM_HTTP_CONNECTION_FAILED' occurs sporadically only",
    "8-1": "The error ICM_HTTP_CONNECTION_FAILED means that no connection could be established between SAP and the target system. If this message occurs only sporadically, it may be a problem at the TCP level of the server on which the AEB solution is running.\nMicrosoft documents a parameter in the registry for Windows to release TCP connections after a certain waiting time: https://technet.microsoft.com/en-us/library/cc938217.aspx\nSince the value is usually set to 120 seconds, reducing the waiting time can solve the problem. \n\nTranslated with www.DeepL.com/Translator",
    "9-0": "'ICM_HTTP_TIMEOUT'.",
    "9-1": "It may be due to the proxy used, the SSL certificates must be known there. The proxy must not hold obsolete certificates. If so, remove them from the certificate memory. Even if a decryption of the SSL connection can lead to the error.",
    "10-0": "Unsupported xstream found: (HTTP Code 200 : OK)",
    "10-1": "One possible cause is incorrect SSL settings in the connection or the logical port.",
    "11-0": "SOAP:1.007 SRT: Unsupported xstream found: (HTTP Code 404 : Not Found)",
    "11-1": "An incorrect path prefix is entered in the destination or logical port.",
    "12-0": "The log file dev.icm contains: \nthe verification of the server's certif-icate chain failed' or also\nUntrusted Chain PEER_CERT_UNTRUSTED",
    "12-1": "The SSL certificates have not been read correctly, or not all of them are known in the PSE. This error is also described in more detail in SAP Note 1094342.",
    "13-0": "SOAP:1.023: SRT: Processing error in Internet Communication Frame-work: (\"ICF Error when receiving the response: ICM_HTTP_CONNECTION_BROKEN\")",
    "13-1": "This error means that the already established connection has been interrupted. This is most likely due to the fact that there are short interruptions in the network / Internet connection. This may also occur if the password of the connection user is wrong.",
    "14-0": "ICF Error when receiving the re-sponse: ICM_HTTP_CONNECTION_FAILED",
    "14-1": "Error pattern: There are repeated interruptions. In between, however, many calls also work. The ICM log contains the error message NIECONN_REFUSED for the affected user, but with the IP address of the proxy server. This user has no authorization to establish an external connection via the proxy.",
    "15-0": "SOAP:1.013 SRT: ASSERT failed: field is initial",
    "15-1": "See SAP Note 921347.",
    "16-0": "SOAP:1.008 SRT: Couldn't create Object: ICF error when creating HTTP client object by config for URL",
    "17-0": "SOAP:1036 SRT: HTTP-Code 415: (\"Unsupported 22Media Type\")",
    "16-1": "## The password of the connection user is incorrectly stored in the SM59 or in the SOAMANAGER.\n##The AEB solution runs in the AEB data center and the connection user does not have the role I_BUSINESSFACADE in the AEB solution. ",
    "17-1": "In SOAMANGER SOAP 1.2 is set to 1.1 instead of SOAP 1.1."
  },
  "cols": 2,
  "rows": 18
}
[/block]