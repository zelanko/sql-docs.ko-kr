---
title: Kerberos 통합 인증을 사용하여 SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c36df2b7cc6feda976a3edfdadbac68e9b96dd3
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279045"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Kerberos 통합 인증을 사용하여 SQL Server에 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]부터 응용 프로그램에서 유형 4 Kerberos 통합 인증을 사용하여 데이터베이스에 연결한다는 것을 나타내기 위해 **authenticationScheme** 연결 속성을 사용할 수 있습니다. 참조 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md) 연결 속성에 대 한 자세한 내용은 합니다. Kerberos에 대 한 자세한 내용은 참조 하세요. [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758)합니다.  
  
 Java **Krb5LoginModule**과 함께 통합 인증을 사용하면 [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)를 사용하여 모듈을 구성할 수 있습니다.  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 IBM Java VM에 대해 다음 속성을 설정합니다.  
  
-   **useDefaultCcache = true**  
  
-   **moduleBanner = false**  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 다른 모든 Java VM에 대해 다음 속성을 설정합니다.  
  
-   **useTicketCache = true**  
  
-   **doNotPrompt = true**  
  
## <a name="remarks"></a>Remarks  
 이전 버전 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], 응용 프로그램 통합된 인증 (Kerberos 또는 NTLM을 사용 하 여, 사용할 수 있는에 따라)을 지정할 수를 사용 하 여 합니다 **integratedSecurity** 연결 속성 및 참조 하 여  **sqljdbc_auth.dll**에 설명 된 대로 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)합니다.  
  
 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]부터 응용 프로그램에서는 순수한 Java Kerberos 구현을 사용하는 Kerberos 통합 인증을 사용하여 데이터베이스에 연결한다는 것을 나타내기 위해 **authenticationScheme** 연결 속성을 사용할 수 있습니다.  
  
-   통합된 인증을 사용 하려는 경우 **Krb5LoginModule**를 지정 해야 합니다 **integratedSecurity = true** 연결 속성입니다. 그런 다음 지정 해야 합니다 **authenticationScheme JavaKerberos =** 연결 속성입니다.  
  
-   계속 통합된 인증을 사용 하려면 **sqljdbc_auth.dll**를 지정 하면 **integratedSecurity = true** 연결 속성 (및 필요에 따라 **authenticationScheme = NativeAuthentication**).  
  
-   지정 하는 경우 **authenticationScheme = JavaKerberos** 도 지정 하지 않으면 **integratedSecurity = true**를 무시 합니다 **authenticationScheme** 연결 속성을 검색할 사용자 이름 및 암호 자격 증명 연결 문자열에 필요 합니다.  
  
 데이터 원본을 사용하여 연결을 만들 때 setAuthenticationScheme을 사용하여 프로그래밍 방식으로 인증 체계를 설정하고 필요에 따라 **setServerSpn**을 사용하여 Kerberos 연결에 대해 SPN을 설정할 수 있습니다.  
  
 Kerberos 인증 com.microsoft.sqlserver.jdbc.internals.KerbAuthentication을 지원하기 위해 새로운 로거가 추가되었습니다. 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요.  
  
 다음 지침은 Kerberos 구성에 도움이 될 것입니다.  
  
1.  설정할 **AllowTgtSessionKey** Windows 레지스트리에서 1입니다. 자세한 내용은 [Windows Server 2003의 Kerberos 프로토콜 레지스트리 항목 및 KDC 구성 키](http://support.microsoft.com/kb/837361)를 참조하십시오.  
  
2.  Kerberos 구성(UNIX 환경에서 krb5.conf)이 사용자 환경의 올바른 영역과 KDC를 가리키는지 확인하십시오.  
  
3.  kinit을 사용하거나 도메인에 로그인하여 TGT 캐시를 초기화합니다.  
  
4.  **authenticationScheme=JavaKerberos**를 사용하는 응용 프로그램이 Windows Vista 또는 Windows 7 운영 체제에서 실행될 때는 표준 사용자 계정을 사용해야 합니다. 그러나 관리자 계정에서 응용 프로그램을 실행하는 경우 관리자 권한을 사용하여 응용 프로그램을 실행해야 합니다.  
  
> [!NOTE]  
>  serverSpn 연결 특성은 Microsoft JDBC Driver 4.2 이상에서만 지원됩니다.  
  
## <a name="service-principal-names"></a>서비스 사용자 이름  
 SPN(서비스 사용자 이름)은 클라이언트가 서비스 인스턴스를 고유하게 식별하는 이름입니다.  
  
 **serverSpn** 연결 속성을 사용하여 SPN을 지정하거나, 드라이버에서 자동으로 빌드(기본값)하도록 할 수 있습니다.  이 속성은 “MSSQLSvc/fqdn:port\@REALM” 형식이 될 수 있습니다. 여기서 fqdn은 정규화된 도메인 이름이고, port는 포트 번호이며, REALM은 대문자로 표시된 SQL Server의 Kerberos 영역입니다.  이 속성의 realm 부분은 Kerberos 구성의 기본 영역이 서버의 영역과 동일한 경우 선택 사항이며 기본적으로 포함되어 있지 않습니다.  Kerberos 구성의 기본 영역이 서버의 영역과 다른 상호 영역 인증 시나리오를 지원하려면 serverSpn 속성으로 SPN을 설정해야 합니다.  
  
 예를 들어 프로그램 SPN 같습니다: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ 합니다. CORP. CONTOSO.COM "  
  
 SPN(서비스 사용자 이름)에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SQL Server에서 Kerberos 인증을 사용하는 방법](http://support.microsoft.com/kb/319723)  
  
-   [SQL Server에서 Kerberos 사용](http://go.microsoft.com/fwlink/?LinkId=207814)  

> [!NOTE]  
> 6.2.0 교차 영역 Kerberos의 적절 한 사용에 대 한 JDBC 드라이버의 릴리스 전에 명시적으로 설정 해야 합니다 **serverSpn**합니다.
>
> 6.2.0부터 릴리스에서 드라이버를 빌드할 수는 **serverSpn** 교차 영역 Kerberos를 사용 하는 경우에 기본적으로 합니다. 하나를 사용할 수 있지만 **serverSpn** 명시적으로 너무 합니다. 
  
## <a name="creating-a-login-module-configuration-file"></a>로그인 모듈 구성 파일 만들기  
 선택적으로 Kerberos 구성 파일을 지정할 수 있습니다. 구성 파일을 지정하지 않은 경우 다음 설정이 적용됩니다.  
  
 Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
  
 IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;  
  
 로그인 모듈 구성 파일을 만들기로 결정했으면 파일은 다음 형식을 따라야 합니다.  
  
```  
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```  
  
 로그인 구성 파일은 하나 이상의 항목으로 구성되며, 각 항목은 특정 응용 프로그램에 사용해야 하는 기본 인증 기술을 지정합니다. 예:  
  
```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```  
  
 따라서 각 로그인 모듈 구성 파일 항목은 이름과 하나 이상의 LoginModule 관련 항목으로 구성되며, 각 LoginModule 관련 항목은 세미콜론으로 끝나고 LoginModule 관련 항목의 전체 그룹은 중괄호로 묶입니다. 각 구성 파일 항목은 세미콜론으로 끝납니다.  
  
 로그인 모듈 구성 파일에 지정된 설정을 사용하여 드라이버가 Kerberos 자격 증명을 얻을 수 있도록 하면서 기존 자격 증명을 사용할 수 있습니다. 이것은 응용 프로그램이 둘 이상의 사용자 자격 증명을 사용하여 연결을 만들어야 할 때 유용할 수 있습니다.  
  
 드라이버는 지정된 로그인 모듈을 사용하여 로그인을 시도하기 전에 사용 가능한 경우 기존 자격 증명을 사용하려고 시도합니다. 따라서 특정 컨텍스트에서 코드를 실행하기 위해 Subject.doAs 메서드를 사용할 때 Subject.doAs 호출에 전달된 자격 증명을 사용하여 연결이 만들어집니다.  
  
 자세한 내용은 [JAAS 로그인 구성 파일](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) 및 [Krb5LoginModule 클래스](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)를 참조하십시오.  

 Microsoft JDBC Driver 6.2부터 연결 속성 jaasConfigurationName를 사용 하 여 로그인 모듈 구성 파일의 이름을 전달할 수 있습니다, 그리고 이렇게 하면 각 연결에는 자체 로그인 구성을 가질 수 있습니다.
 
## <a name="creating-a-kerberos-configuration-file"></a>Kerberos 구성 파일 만들기  
 Kerberos 구성 파일에 대한 자세한 내용은 [Kerberos 요구 사항](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)을 참조하십시오.  
  
 이것은 샘플 도메인 구성 파일입니다. 여기서 YYYY 및 ZZZZ는 해당 사이트의 도메인 이름입니다.  
  
```  
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  
  
[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  
  
[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  
  
        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  
  
```  
  
## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>도메인 구성 파일 및 로그인 모듈 구성 파일 활성화  
 -Djava.security.krb5.conf를 사용하여 도메인 구성 파일을 활성화할 수 있습니다. 사용 하 여 로그인 모듈 구성 파일을 설정할 수 있습니다 **-Djava.security.auth.login.config**합니다.  
  
 예를 들어, 응용 프로그램을 시작할 때 다음 명령줄을 사용할 수 있습니다.  
  
```  
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  
  
```  
  
## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Kerberos를 통해 SQL Server에 액세스할 수 있는지 확인  
 SQL Server Management Studio에서 다음 쿼리 실행:  
  
 **sys.dm_exec_connections에서 auth_scheme 선택 있는 세션 id =\@\@spid**  
  
 이 쿼리를 실행하는 데 필요한 권한이 있는지 확인하십시오.  

## <a name="constrained-delegation"></a>제한된 위임
Microsoft JDBC Driver 6.2 부터는 드라이버는 Kerberos 제한 위임을 지원 합니다. 위임 된 자격 증명 org.ietf.jgss.GSSCredential 개체 변수로 전달 될 수 있습니다, 그리고 연결할 드라이버에서 이러한 자격 증명이 사용 됩니다. 

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>사용자 이름 및 암호를 사용 하 여 Kerberos 연결
Microsoft JDBC Driver 6.2 부터는 드라이버는 Kerberos 연결의 보안 주체 이름 및 암호를 사용 하 여 전달 된 연결 문자열에 설정할 수 있습니다. 
```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```
Username 속성 영역을 사용자가 krb5.conf 파일에서 설정 default_realm에 속한 경우 필요 하지 않습니다. 때 `userName` 하 고 `password` 와 함께 설정 됩니다 `integratedSecurity=true;` 및 `authenticationScheme=JavaKerberos;` 연결 속성 설정 된 사용자 이름 값 Kerberos 주체와 함께 제공 된 암호를 사용 하 여 합니다.
 
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
