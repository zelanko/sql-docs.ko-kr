---
title: Kerberos 통합 인증을 사용하여 SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 894da21c079b776524c07cab8b8f223bae769aee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916228"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>Kerberos 통합 인증을 사용하여 SQL Server에 연결

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]부터 애플리케이션에서 유형 4 Kerberos 통합 인증을 사용하여 데이터베이스에 연결한다는 것을 나타내기 위해 **authenticationScheme** 연결 속성을 사용할 수 있습니다. 연결 속성에 대 한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md) 을 참조 하세요. Kerberos에 대 한 자세한 내용은 [Microsoft kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)를 참조 하십시오.

Java **Krb5LoginModule**과 함께 통합 인증을 사용하면 [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)를 사용하여 모듈을 구성할 수 있습니다.

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 IBM Java VM에 대해 다음 속성을 설정합니다.

- **useDefaultCcache = true**
- **moduleBanner = false**

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 다른 모든 Java VM에 대해 다음 속성을 설정합니다.

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Remarks

이전 버전에서는 응용 프로그램이 다음을 참조 하 여 통합 인증 (사용할 수 있는 경우에 따라 Kerberos 또는 NTLM을 **사용 하는** )을 지정할 수 있습니다. [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 연결 URL [작성에설명 된 **sqljdbc_auth**.](../../connect/jdbc/building-the-connection-url.md)

[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]부터 애플리케이션에서는 순수한 Java Kerberos 구현을 사용하는 Kerberos 통합 인증을 사용하여 데이터베이스에 연결한다는 것을 나타내기 위해 **authenticationScheme** 연결 속성을 사용할 수 있습니다.

- **Krb5LoginModule**를 사용 하 여 통합 인증을 사용 하려는 경우에는 **계속 연결 속성** 을 지정 해야 합니다. 그런 다음 **Authenticationscheme = JavaKerberos** connection 속성도 지정 합니다.

- **Sqljdbc_auth**와 함께 통합 인증을 계속 사용 **하려면 연결 속성** (및 선택적으로 **authenticationscheme = NativeAuthentication**)을 지정 하면 됩니다.

- **Authenticationscheme = JavaKerberos** 을 지정 하지만 지 속성 **atedsecurity = true**를 지정 하지 않으면 드라이버는 **authenticationscheme** 연결 속성을 무시 하 고 사용자 이름 및 암호를 찾을 것으로 간주 됩니다. 연결 문자열의 자격 증명입니다.

데이터 원본을 사용하여 연결을 만들 때 **setAuthenticationScheme**을 사용하여 프로그래밍 방식으로 인증 체계를 설정하고 필요에 따라 **setServerSpn**을 사용하여 Kerberos 연결에 대해 SPN을 설정할 수 있습니다.

Kerberos 인증 com.microsoft.sqlserver.jdbc.internals.KerbAuthentication을 지원하기 위해 새로운 로거가 추가되었습니다. 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요.

다음 지침은 Kerberos 구성에 도움이 될 것입니다.

1. Windows의 레지스트리에서 **AllowTgtSessionKey** 을 1로 설정 합니다. 자세한 내용은 [Windows Server 2003의 Kerberos 프로토콜 레지스트리 항목 및 KDC 구성 키](https://support.microsoft.com/kb/837361)를 참조하십시오.
2. Kerberos 구성(UNIX 환경에서 krb5.conf)이 사용자 환경의 올바른 영역과 KDC를 가리키는지 확인하십시오.
3. kinit을 사용하거나 도메인에 로그인하여 TGT 캐시를 초기화합니다.
4. **authenticationScheme=JavaKerberos**를 사용하는 애플리케이션이 Windows Vista 또는 Windows 7 운영 체제에서 실행될 때는 표준 사용자 계정을 사용해야 합니다. 그러나 관리자 계정에서 애플리케이션을 실행하는 경우 관리자 권한을 사용하여 애플리케이션을 실행해야 합니다.

> [!NOTE]  
> serverSpn 연결 특성은 Microsoft JDBC Driver 4.2 이상에서만 지원됩니다.

## <a name="service-principal-names"></a>서비스 사용자 이름

SPN(서비스 사용자 이름)은 클라이언트가 서비스 인스턴스를 고유하게 식별하는 이름입니다.

**serverSpn** 연결 속성을 사용하여 SPN을 지정하거나, 드라이버에서 자동으로 빌드(기본값)하도록 할 수 있습니다. 이 속성은 "MSSQLSvc/fqdn:port\@REALM" 양식이 될 수 있습니다. 여기서 fqdn은 정규화된 도메인 이름이고, port는 포트 번호이며, REALM은 대문자로 표시된 SQL Server의 Kerberos 영역입니다. 이 속성의 realm 부분은 Kerberos 구성의 기본 영역이 서버의 영역과 동일한 경우 선택 사항이며 기본적으로 포함되어 있지 않습니다. Kerberos 구성의 기본 영역이 서버의 영역과 다른 상호 영역 인증 시나리오를 지원하려면 serverSpn 속성으로 SPN을 설정해야 합니다.

예를 들어 SPN은 "MSSQLSvc/ZZZZ: 1433:1433\@"과 같습니다. C. CONTOSO.COM "

SPN(서비스 사용자 이름)에 대한 자세한 내용은 다음을 참조하십시오.

- [SQL Server에서 Kerberos 인증을 사용하는 방법](https://support.microsoft.com/kb/319723)

- [SQL Server에서 Kerberos 사용](https://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> JDBC 드라이버 릴리스 6.2 이전에는 영역 간 Kerberos를 적절히 사용 하려면 **Serverspn**을 명시적으로 설정 해야 합니다.
>
> 6\.2 릴리스를 기준으로, 드라이버는 교차 영역 Kerberos를 사용 하는 경우에도 기본적으로 **Serverspn** 을 빌드할 수 있습니다. 하지만 **Serverspn** 을 명시적으로 사용할 수도 있습니다.

## <a name="creating-a-login-module-configuration-file"></a>로그인 모듈 구성 파일 만들기

선택적으로 Kerberos 구성 파일을 지정할 수 있습니다. 구성 파일을 지정하지 않은 경우 다음 설정이 적용됩니다.

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

로그인 모듈 구성 파일을 만들기로 결정했으면 파일은 다음 형식을 따라야 합니다.

```java
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

로그인 모듈 구성 파일에 지정된 설정을 사용하여 드라이버가 Kerberos 자격 증명을 얻을 수 있도록 하면서 기존 자격 증명을 사용할 수 있습니다. 애플리케이션에서 둘 이상의 사용자 자격 증명을 사용하여 연결을 만들어야 하는 경우에 이것이 유용할 수 있습니다.

드라이버는 지정된 로그인 모듈을 사용하여 로그인을 시도하기 전에 사용 가능한 경우 기존 자격 증명을 사용하려고 시도합니다. 따라서 특정 컨텍스트에서 코드를 실행하기 위해 `Subject.doAs` 메서드를 사용할 때 `Subject.doAs` 호출에 전달된 자격 증명을 사용하여 연결이 만들어집니다.

자세한 내용은 [JAAS 로그인 구성 파일](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html) 및 [Krb5LoginModule 클래스](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html)를 참조하십시오.

Microsoft JDBC Driver 6.2 부터는 연결 속성 `jaasConfigurationName`을 사용 하 여 로그인 모듈 구성 파일의 이름을 선택적으로 전달할 수 있습니다. 이렇게 하면 각 연결에 고유한 로그인 구성이 포함 됩니다.

## <a name="creating-a-kerberos-configuration-file"></a>Kerberos 구성 파일 만들기

Kerberos 구성 파일에 대한 자세한 내용은 [Kerberos 요구 사항](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)을 참조하십시오.

이것은 샘플 도메인 구성 파일이고, 여기서 YYYY 및 ZZZZ는 도메인 이름입니다.

```ini
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

-Djava.security.krb5.conf를 사용하여 도메인 구성 파일을 활성화할 수 있습니다. **-** D c o. p. t o n. t o n.

예를 들어 다음 명령을 사용 하 여 응용 프로그램을 시작할 수 있습니다.

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>Kerberos를 통해 SQL Server에 액세스할 수 있는지 확인

SQL Server Management Studio에서 다음 쿼리 실행:

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

이 쿼리를 실행하는 데 필요한 권한이 있는지 확인하십시오.

## <a name="constrained-delegation"></a>제한된 위임

Microsoft JDBC Driver 6.2부터 드라이버는 Kerberos 제한 된 위임을 지원 합니다. 위임 된 자격 증명을 GSSCredential 개체로 전달할 수 있습니다. 이러한 자격 증명은 드라이버에서 연결을 설정 하는 데 사용 됩니다.

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>보안 주체 이름 및 암호를 사용 하는 Kerberos 연결

Microsoft JDBC Driver 6.2부터 드라이버는 연결 문자열에 전달 된 사용자 이름 및 암호를 사용 하 여 Kerberos 연결을 설정할 수 있습니다.

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

사용자 이름 속성은 사용자가 krb5.conf 파일의 default_realm 집합에 속하는 경우 영역을 요구 하지 않습니다. `userName` `integratedSecurity=true;` 및가 및 속성과`authenticationScheme=JavaKerberos;` 함께 설정 된 경우 제공 된 암호와 함께 사용자 이름 값을 Kerberos 주체로 설정 하 여 연결을 설정 합니다. `password`

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>동일한 도메인의 Unix 컴퓨터에서 Kerberos 인증 사용

이 가이드에서는 Kerberos가 제대로 설치 되어 있다고 가정 합니다. Kerberos 인증을 사용 하 여 Windows 컴퓨터에서 다음 코드를 실행 하 여 앞서 언급 한이 true 인지 확인 합니다. 이 코드는 성공 하면 "인증 체계: KERBEROS"를 콘솔에 출력 합니다. 제공 된 외부에는 추가 런타임 플래그, 종속성 또는 드라이버 설정이 필요 하지 않습니다. 성공적인 연결을 확인 하기 위해 Linux에서 동일한 코드 블록을 실행할 수 있습니다.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. 서버와 동일한 도메인에 클라이언트 컴퓨터를 가입 시킵니다.
2. 필드 기본 Kerberos 티켓 위치를 설정 합니다. 이는 환경 변수를 `KRB5CCNAME` 설정 하 여 가장 편리 하 게 수행할 수 있습니다.
3. 새 Kerberos 티켓을 생성 하거나 기본 Kerberos 티켓 위치에 기존 항목을 배치 하 여 Kerberos 티켓을 가져옵니다. 티켓을 생성 하려면 터미널을 사용 하 고 "USER" 및 " `kinit USER@DOMAIN.AD` 도메인을 통해 티켓을 초기화 하면 됩니다. AD "는 각각 주 서버와 도메인입니다. 예: `kinit SQL_SERVER_USER03@MICROSOFT.COM` 티켓은 기본 티켓 위치 또는 `KRB5CCNAME` 경로 (설정 된 경우)에 생성 됩니다.
4. 터미널에 암호를 입력 하 라는 메시지가 표시 되 면 암호를 입력 합니다.
5. Via `klist` 에서 티켓의 자격 증명을 확인 하 고 자격 증명을 인증에 사용 하려는 자격 증명 인지 확인 합니다.
6. 위의 샘플 코드를 실행 하 고 Kerberos 인증에 성공 했는지 확인 합니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
