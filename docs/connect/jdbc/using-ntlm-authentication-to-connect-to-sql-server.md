---
title: NTLM 인증을 사용 하 여 SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: 11fe35e1dc90e32cac460b61fe8a6078c817b0ca
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894105"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>NTLM 인증을 사용 하 여 SQL Server에 연결

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

를 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 사용 하면 응용 프로그램에서 **authenticationscheme** 연결 속성을 사용 하 여 NTLM v2 인증을 사용 하 여 데이터베이스에 연결 하려고 함을 나타낼 수 있습니다. 

NTLM 인증에도 다음 속성이 사용 됩니다.

- **도메인 = 도메인 이름** 필드
- **사용자 = 사용자 이름**
- **password = password**
- **% = true**

**도메인**이외에 다른 속성은 필수 이며, **NTLM** authenticationscheme 속성을 사용할 때 누락 된 경우 드라이버에서 오류를 throw 합니다. 

연결 속성에 대 한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조 하세요. Microsoft NTLM 인증 프로토콜에 대 한 자세한 내용은 [MICROSOFT ntlm](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm)을 참조 하십시오.

## <a name="remarks"></a>Remarks

NTLM 인증의 동작을 제어 하는 SQL server 설정에 대 한 설명은 [네트워크 보안: LAN 관리자 인증 수준](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) 을 참조 하세요. 

## <a name="logging"></a>로깅

NTLM 인증 com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication을 지원하기 위해 새로운 로거가 추가되었습니다. 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요.

## <a name="datasource"></a>DataSource

데이터 원본을 사용 하 여 연결을 만들 때 **Setauthenticationscheme**, **setdomain**및 (선택 사항) **SETAUTHENTICATIONSCHEME**을 사용 하 여 NTLM 속성을 프로그래밍 방식으로 설정할 수 있습니다.

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>서비스 사용자 이름

SPN(서비스 사용자 이름)은 클라이언트가 서비스 인스턴스를 고유하게 식별하는 이름입니다.

**serverSpn** 연결 속성을 사용하여 SPN을 지정하거나, 드라이버에서 자동으로 빌드(기본값)하도록 할 수 있습니다. 이 속성은 "MSSQLSvc/fqdn:port\@REALM" 형식이 될 수 있습니다. 여기서 fqdn은 정규화된 도메인 이름이고, port는 포트 번호이며, REALM은 대문자로 표시된 SQL Server의 영역입니다. 기본 영역이 서버의 영역과 동일 하므로이 속성의 영역 부분은 선택 사항입니다.

예를 들어 SPN은 "MSSQLSvc/: 1433"과 같을 수 있습니다.

SPN(서비스 사용자 이름)에 대한 자세한 내용은 다음을 참조하십시오.

- [클라이언트 연결의 SPN(서비스 사용자 이름) 지원](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> serverSpn 연결 특성은 Microsoft JDBC Driver 4.2 이상에서만 지원됩니다.

> JDBC driver 6.2 릴리스 전에는 **Serverspn**을 명시적으로 설정 해야 합니다. 6\.2 릴리스부터는 **Serverspn** 을 명시적으로 사용할 수는 있지만 기본적으로 드라이버는 **Serverspn** 을 빌드할 수 있습니다.

## <a name="security-risks"></a>보안 위험

NTLM 프로토콜은 보안 위험을 야기 하는 다양 한 취약성이 있는 이전 인증 프로토콜입니다. 상대적으로 약한 암호화 체계를 기반으로 하며 다양 한 공격에 취약 합니다. 이는 훨씬 더 안전 하 고 권장 되는 Kerberos로 대체 되었습니다. NTLM 인증은 안전한 신뢰할 수 있는 환경 에서만 사용 하거나 Kerberos를 사용할 수 없는 경우에만 사용 해야 합니다.

는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 원래 v1 프로토콜 보다 몇 가지 보안 기능이 향상 된 NTLM v2만 지원 합니다. 또한 확장 된 보호를 사용 하도록 설정 하거나 향상 된 보안을 위해 SSL 암호화를 사용 하는 것이 좋습니다. 

확장 된 보호를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

- [확장된 보호를 사용하여 데이터베이스 엔진에 연결](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

SSL 암호화를 사용 하 여 연결 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

- [SSL 암호화를 사용한 연결](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 7\.4 릴리스의 경우 확장 된 보호와 암호화를 **모두** 사용 하도록 설정할 수 없습니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
