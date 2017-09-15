---
title: "Kerberos를 사용 하 여 통합 인증을 SQL Server에 연결 하는 데 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f26a429563aaf5c079c45b064b4723cb19cada90
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Kerberos 통합 인증을 사용하여 SQL Server에 연결
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  부터는 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], 응용 프로그램에서 사용할 수는 **authenticationScheme** 유형 4 Kerberos 통합된 인증을 사용 하 여 데이터베이스에 연결 하려고 한다는 것을 나타내기 위해 연결 속성입니다. 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md) 연결 속성에 대 한 자세한 내용은 합니다. Kerberos에 대 한 자세한 내용은 참조 하십시오. [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758)합니다.  
  
 Java와 함께 통합된 인증을 사용 하는 경우 **Krb5LoginModule**를 사용 하 여 모듈을 구성할 수 있습니다 [Krb5LoginModule 클래스](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)합니다.  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] IBM Java Vm에 대해 다음 속성을 설정 합니다.  
  
-   **useDefaultCcache = true**  
  
-   **moduleBanner = false**  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 다른 모든 Java Vm에 대 한 다음 속성을 설정 합니다.  
  
-   **useTicketCache = true**  
  
-   **doNotPrompt = true**  
  
## <a name="remarks"></a>주의  
 이전에 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], 응용 프로그램에서 통합된 인증 (Kerberos 또는 NTLM을 사용 하 여, 사용 하지 않는에 따라)를 지정할 수를 사용 하 여는 **integratedSecurity** 연결 속성 및 참조 하 여 ** sqljdbc_auth.dll**에 설명 된 대로 [연결 URL 작성](../../connect/jdbc/building-the-connection-url.md)합니다.  
  
 부터는 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], 응용 프로그램에서 사용할 수는 **authenticationScheme** Kerberos를 사용 하 여 데이터베이스에 연결 하려고 한다는 것을 나타내기 위해 연결 속성 통합 순수한 Java Kerberos를 사용 하 여 인증 구현:  
  
-   통합된 인증에 사용 하 여 원하는 경우 **Krb5LoginModule**를 지정 해야는 **integratedSecurity = true** 연결 속성입니다. 지정 해야 합니다 다음는 **authenticationScheme JavaKerberos =** 연결 속성입니다.  
  
-   통합된 인증을 사용 하 여 계속 하려면 **sqljdbc_auth.dll**, 지정 **integratedSecurity = true** 연결 속성 (및 필요에 따라 **authenticationScheme = NativeAuthentication**).  
  
-   지정 하는 경우 **authenticationScheme JavaKerberos =** 도 지정 하지 않으면 **integratedSecurity = true**, 드라이버에서 무시 된 **authenticationScheme** 연결 속성 증명을 연결 문자열에 사용자 이름 및 암호 자격 증명을 찾습니다.  
  
 Datasource를 사용 하 여 연결을 만들를 프로그래밍 방식으로 때 setAuthenticationScheme를 사용 하 여 인증 체계를 설정 하 고 (선택 사항) 사용 하 여 Kerberos 연결에 대 한 SPN을 설정할 수 **setServerSpn**합니다.  
  
 Kerberos 인증 com.microsoft.sqlserver.jdbc.internals.KerbAuthentication을 지원하기 위해 새로운 로거가 추가되었습니다. 자세한 내용은 참조 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)합니다.  
  
 다음 지침은 Kerberos 구성에 도움이 될 것입니다.  
  
1.  설정 **AllowTgtSessionKey** Windows 용 레지스트리에서 1입니다. 자세한 내용은 참조 [Kerberos 프로토콜 레지스트리 항목 및 KDC 구성 키 Windows Server 2003에서](http://support.microsoft.com/kb/837361)합니다.  
  
2.  Kerberos 구성(UNIX 환경에서 krb5.conf)이 사용자 환경의 올바른 영역과 KDC를 가리키는지 확인하십시오.  
  
3.  kinit을 사용하거나 도메인에 로그인하여 TGT 캐시를 초기화합니다.  
  
4.  응용 프로그램을 사용 하는 경우 **authenticationScheme JavaKerberos =** 운영 체제는 Windows Vista 또는 Windows 7에서 실행 되며, 표준 사용자 계정을 사용 해야 합니다. 그러나 관리자 계정에서 응용 프로그램을 실행하는 경우 관리자 권한을 사용하여 응용 프로그램을 실행해야 합니다.  
  
> [!NOTE]  
>  ServerSpn 연결 특성에서 Microsoft JDBC Driver 4.2 이상 에서만 지원 됩니다.  
  
## <a name="service-principal-names"></a>서비스 사용자 이름  
 SPN(서비스 사용자 이름)은 클라이언트가 서비스 인스턴스를 고유하게 식별하는 이름입니다.  
  
 사용 하 여 SPN을 지정할 수 있습니다는 **serverSpn** 연결 속성을 단순히 있습니다 (기본값)에 대 한 빌드 드라이버 되도록 허용 합니다.  이 속성의 형태로: "MSSQLSvc/fqdn:port@REALM" 여기서 fqdn은 정규화 된 도메인 이름, 포트는 포트 번호 및 REALM은 대문자로의 SQL Server의 Kerberos 영역입니다.  이 속성의 realm 부분은 Kerberos 구성의 기본 영역이 서버의 영역과 동일한 경우 선택 사항이며 기본적으로 포함되어 있지 않습니다.  Kerberos 구성의 기본 영역이 서버의 영역과 다른 상호 영역 인증 시나리오를 지원하려면 serverSpn 속성으로 SPN을 설정해야 합니다.  
  
 예를 들어 프로그램 SPN 같습니다: "MSSQLSvc/some-server.zzz.corp.contoso.com:1433@ZZZZ.CORP.CONTOSO.COM"  
  
 SPN(서비스 사용자 이름)에 대한 자세한 내용은 다음을 참조하십시오.  
  
-   [SQL Server에서 Kerberos 인증을 사용 하는 방법](http://support.microsoft.com/kb/319723)  
  
-   [SQL Server와 함께 Kerberos를 사용 하 여](http://go.microsoft.com/fwlink/?LinkId=207814)  

> [!NOTE]  
> 명시적으로 설정 해야 6.2.0 교차 영역 Kerberos의 적절 한 사용에 대 한 JDBC 드라이버의 릴리스 전에 **serverSpn**합니다.
>
> 6.2.0 현재 릴리스의 경우 드라이버는 만들 수는 **serverSpn** 교차 영역 Kerberos를 사용 하는 경우에 기본적으로 합니다. 하나를 사용할 수 있지만 **serverSpn** 명시적으로 너무 합니다. 
  
## <a name="creating-a-login-module-configuration-file"></a>로그인 모듈 구성 파일 만들기  
 선택적으로 Kerberos 구성 파일을 지정할 수 있습니다. 구성 파일을 지정하지 않은 경우 다음 설정이 적용됩니다.  
  
 Sun JVM  
 com.sun.security.auth.module.krb5loginmodule에 useTicketCache = true;  
  
 IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule에 useDefaultCcache 필요한 = true;  
  
 로그인 모듈 구성 파일을 만들기로 결정했으면 파일은 다음 형식을 따라야 합니다.  
  
```  
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```  
  
 로그인 구성 파일은 하나 이상의 항목으로 구성되며, 각 항목은 특정 응용 프로그램에 사용해야 하는 기본 인증 기술을 지정합니다. 예:  
  
```  
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```  
  
 따라서 각 로그인 모듈 구성 파일 항목은 이름과 하나 이상의 LoginModule 관련 항목으로 구성되며, 각 LoginModule 관련 항목은 세미콜론으로 끝나고 LoginModule 관련 항목의 전체 그룹은 중괄호로 묶입니다. 각 구성 파일 항목은 세미콜론으로 끝납니다.  
  
 로그인 모듈 구성 파일에 지정된 설정을 사용하여 드라이버가 Kerberos 자격 증명을 얻을 수 있도록 하면서 기존 자격 증명을 사용할 수 있습니다. 이것은 응용 프로그램이 둘 이상의 사용자 자격 증명을 사용하여 연결을 만들어야 할 때 유용할 수 있습니다.  
  
 드라이버는 지정된 로그인 모듈을 사용하여 로그인을 시도하기 전에 사용 가능한 경우 기존 자격 증명을 사용하려고 시도합니다. 따라서 특정 컨텍스트에서 코드를 실행하기 위해 Subject.doAs 메서드를 사용할 때 Subject.doAs 호출에 전달된 자격 증명을 사용하여 연결이 만들어집니다.  
  
 자세한 내용은 참조 [JAAS 로그인 구성 파일](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) 및 [Krb5LoginModule 클래스](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)합니다.  

 Microsoft JDBC 드라이버 6.2부터, 각 연결에는 자체 로그인 구성을 사용 하면이 연결 속성 jaasConfigurationName를 사용 하 여 로그인 모듈 구성 파일의 이름을 전달할 수 있습니다.
 
## <a name="creating-a-kerberos-configuration-file"></a>Kerberos 구성 파일 만들기  
 Kerberos 구성 파일에 대 한 자세한 내용은 참조 [Kerberos 요구 사항](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)합니다.  
  
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
 -Djava.security.krb5.conf를 사용하여 도메인 구성 파일을 활성화할 수 있습니다. 로그인 모듈 구성 파일을 사용 하도록 설정할 수 **-Djava.security.auth.login.config**합니다.  
  
 예를 들어, 응용 프로그램을 시작할 때 다음 명령줄을 사용할 수 있습니다.  
  
```  
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  
  
```  
  
## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Kerberos를 통해 SQL Server에 액세스할 수 있는지 확인  
 SQL Server Management Studio에서 다음 쿼리 실행:  
  
 **sys.dm_exec_connections에서 auth_scheme를 선택 합니다. 여기서 session_id = @@spid**  
  
 이 쿼리를 실행하는 데 필요한 권한이 있는지 확인하십시오.  

## <a name="constrained-delegation"></a>제한 된 위임
Microsoft JDBC 드라이버 6.2부터, 드라이버는 Kerberos 제한 위임을 지원 합니다. 위임 된 자격 증명 org.ietf.jgss.GSSCredential 개체에 전달 될 수 있습니다, 그리고 드라이버 연결을 설정 하려면 이러한 자격 증명을 사용 합니다. 

```
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>사용자 이름 및 암호를 사용 하 여 Kerberos 연결
Microsoft JDBC 드라이버 6.2부터, 드라이버는 Kerberos 연결의 보안 주체 이름 및 암호를 사용 하 여 전달 된 연결 문자열에 설정할 수 있습니다. 
```
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```
Username 속성 영역을 사용자 krb5.conf 파일에서 설정 default_realm에 속한 경우 필요 하지 않습니다. 때 `userName` 및 `password` 와 함께 설정 `integratedSecurity=true;` 및 `authenticationScheme=JavaKerberos;` 속성, 연결 설정 된 사용자 이름의 값으로 Kerberos 보안 주체와 함께 제공 된 암호를 사용 합니다.
 
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

