---
title: SAP connection trouble shooting (Document Service)
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
You had issues with establishing a connection from your SAP to our data center?\
You should check the following prerequisites:

* When accessing the AEB data center, an HTTPS service must be running (you can access the list of services using transaction SMICM).
* When creating via SOAMANGER and using HTTPS, the certificates must be loaded into the SSL-CLIENT (Anonymous) node. (Transaction STRUST)
* The SAPCRYPTOLIB or COMMON Crypto DLL must be installed and active in the version according to the system requirements. (Transaction STRUST)
* In most cases, errors when calling the Web service are logged in the ICM log. You can open this log in transaction SMICM. (Alternatively, you can open the file "dev.icm" in transaction ST11).

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Issue/Error
      </th>

      <th>
        Solution
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        GET\_BUSINESS\_SYSTEM\_ERROR An error occurred when determining the business system (SLD\_API\_EXCEPTION)
      </td>

      <td>
        Check the logical port in transaction LPCONFIG. Is it created and linked to the correct HTTP connection?  No standard port must be defined for the proxy class.
      </td>
    </tr>

    <tr>
      <td>
        Only a green tick appears in the connection test in the SM59 for an SSL connection.
      </td>

      <td>
        The service for HTTPS is not running.
      </td>
    </tr>

    <tr>
      <td>
        HTTPIO\_PLG\_CANCELED
      </td>

      <td>
        There is probably no service available for the required process (HTTP or HTTPs) or these are not active.\
        Also to be checked: Is the connection in the SM59 really of type G? Are all PSEs in the STRUST below the SSL client green?
      </td>
    </tr>

    <tr>
      <td>
        'Create failed: Argument not found'
      </td>

      <td>
        The problem could be related to the service port - is there the correct port, for example 443', or is there a typing error (e.g. space)?\
        The problem could also be related to the fact that a proxy is required to connect to external websites. If this is the case, the proxy parameters must be stored in the SM59 destination.
      </td>
    </tr>

    <tr>
      <td>
        'ICM\_HTTP\_SSL\_ERROR'
      </td>

      <td>
        The problem may be related to the SSL certificates. Are all required certificates installed in the STRUST? Has the ICM been restarted to reload them?\
        The correct [SSL certificate](https://hosting.review/web-hosting-glossary/#12) list must still be entered in the connection.\
        A fixed IP address has been entered in the destination. For connections to the AEB computer center, the host must be rz3.aeb.de.
      </td>
    </tr>

    <tr>
      <td>
        * 'ICM\_HTTP\_CONNECTION\_FAILED' and in log file dev.icm the error 'NIECONN\_REFUSED' occurs.
      </td>

      <td>
        The name resolution for the host address "rz3.aeb.de" does not work because DNS is not set correctly.\
        The problem could also be related to the fact that a proxy is required to connect to external websites. If this is the case, the proxy parameters must be stored in the SM59 destination.
      </td>
    </tr>

    <tr>
      <td>
        'ICM\_HTTP\_CONNECTION\_FAILED' and in log file dev.icm the error 'NIECONN\_REFUSED' occurs.
      </td>

      <td>
        This may be because the destination forgot to activate SSL. The correct SSL client certificate must also be selected there.

        The firewall may block the connection to the target system. It is possible that the port of the target system is not released.
      </td>
    </tr>

    <tr>
      <td>
        ICM\_HTTP\_CONNECTION\_FAILED' always occurs.
      </td>

      <td>
        Several possible causes. The problem could be related to the port entered in the SM59. Is the correct HTTPS port 443 or the correct HTTP port of the target system stored there? Or is a proxy required for connections?
      </td>
    </tr>

    <tr>
      <td>
        ICM\_HTTP\_CONNECTION\_FAILED' occurs sporadically only
      </td>

      <td>
        The error ICM\_HTTP\_CONNECTION\_FAILED means that no connection could be established between SAP and the target system. If this message occurs only sporadically, it may be a problem at the TCP level of the server on which the AEB solution is running.\
        Microsoft documents a parameter in the registry for Windows to release TCP connections after a certain waiting time: [https://technet.microsoft.com/en-us/library/cc938217.aspx](https://technet.microsoft.com/en-us/library/cc938217.aspx)\
        Since the value is usually set to 120 seconds, reducing the waiting time can solve the problem. 

        Translated with [www.DeepL.com/Translator](http://www.DeepL.com/Translator)
      </td>
    </tr>

    <tr>
      <td>
        'ICM\_HTTP\_TIMEOUT'.
      </td>

      <td>
        It may be due to the proxy used, the SSL certificates must be known there. The proxy must not hold obsolete certificates. If so, remove them from the certificate memory. Even if a decryption of the SSL connection can lead to the error.
      </td>
    </tr>

    <tr>
      <td>
        Unsupported xstream found: (HTTP Code 200 : OK)
      </td>

      <td>
        One possible cause is incorrect SSL settings in the connection or the logical port.
      </td>
    </tr>

    <tr>
      <td>
        SOAP:1.007 SRT: Unsupported xstream found: (HTTP Code 404 : Not Found)
      </td>

      <td>
        An incorrect path prefix is entered in the destination or logical port.
      </td>
    </tr>

    <tr>
      <td>
        SOAP:1.023: SRT: Processing error in Internet Communication Frame-work: ("ICF Error when receiving the response: ICM\_HTTP\_CONNECTION\_BROKEN")
      </td>

      <td>
        This error means that the already established connection has been interrupted. This is most likely due to the fact that there are short interruptions in the network / Internet connection. This may also occur if the password of the connection user is wrong.
      </td>
    </tr>

    <tr>
      <td>
        ICF Error when receiving the re-sponse: ICM\_HTTP\_CONNECTION\_FAILED
      </td>

      <td>
        Error pattern: There are repeated interruptions. In between, however, many calls also work. The ICM log contains the error message NIECONN\_REFUSED for the affected user, but with the IP address of the proxy server.\
        This user has no authorization to establish an external connection via the proxy.
      </td>
    </tr>

    <tr>
      <td>
        SOAP:1.013 SRT: ASSERT failed: field is initial
      </td>

      <td>
        See SAP Note 921347.
      </td>
    </tr>

    <tr>
      <td>
        SOAP:1.008 SRT: Couldn't create Object: ICF error when creating HTTP client object by config for URL
      </td>

      <td>
        ## The password of the connection user is incorrectly stored in the SM59 or in the SOAMANAGER.

        ## The AEB solution runs in the AEB data center and the connection user does not have the role I\_BUSINESSFACADE in the AEB solution.
      </td>
    </tr>

    <tr>
      <td>
        SOAP:1036 SRT: HTTP-Code 415: ("Unsupported 22Media Type")
      </td>

      <td>
        In SOAMANGER SOAP 1.2 is set to 1.1 instead of SOAP 1.1.
      </td>
    </tr>

    <tr>
      <td>
        SOAP:1.007 SRT: Unsupported xstream found: (HTTP Code 404 : Not Found)
      </td>

      <td>
        An incorrect path prefix is entered in the destination or logical port.
      </td>
    </tr>
  </tbody>
</Table>
