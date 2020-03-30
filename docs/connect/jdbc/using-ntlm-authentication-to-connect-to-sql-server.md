---
title: NTLM 인증을 사용하여 SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
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
ms.openlocfilehash: 2fab4794544ada07e0bf5e690da35b72ad6b7421
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69026098"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>NTLM 인증을 사용하여 SQL Server에 연결

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 애플리케이션이 NTLM v2 인증을 사용하여 데이터베이스에 연결한다는 것을 나타내기 위해 **authenticationScheme** 연결 속성을 사용할 수 있습니다. 

NTLM 인증에는 다음 속성도 사용됩니다.

- **domain = domainName**(선택 사항)
- **user = userName**
- **password = password**
- **integratedSecurity = true**

**domain** 이외에 다른 속성은 필수입니다. **NTLM** authenticationScheme 속성이 사용될 때 이 중 하나라도 누락되는 경우 드라이버가 오류를 throw합니다. 

연결 속성에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요. Microsoft NTLM 인증 프로토콜에 대한 자세한 내용은 [Microsoft NTLM](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm)을 참조하세요.

## <a name="remarks"></a>설명

[네트워크 보안: LAN 관리자 인증 수준](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)에서 NTLM 인증의 동작을 제어하는 SQL Server 설정에 대한 설명을 확인합니다. 

## <a name="logging"></a>로깅

NTLM 인증 com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication을 지원하기 위해 새로운 로거가 추가되었습니다. 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요.

## <a name="datasource"></a>DataSource

데이터 원본을 사용하여 연결을 만들 때 **setAuthenticationScheme**, **setDomain** 및 **setServerSpn**(선택 사항)을 사용하여 NTLM 속성을 프로그래밍 방식으로 설정할 수 있습니다.

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

**serverSpn** 연결 속성을 사용하여 SPN을 지정하거나, 드라이버에서 자동으로 빌드(기본값)하도록 할 수 있습니다. 이 속성은 "MSSQLSvc/fqdn:port\@REALM"과 같은 형식으로 지정할 수 있습니다. 여기서 fqdn은 정규화된 도메인 이름이고, port는 포트 번호이며, REALM은 대문자로 표시된 SQL Server의 영역입니다. 기본 영역이 서버의 영역과 동일하므로 이 속성의 영역 부분은 선택 사항입니다.

예를 들어 SPN은 다음과 같을 수 있습니다. "MSSQLSvc/some-server.zzz.corp.contoso.com:1433"

SPN(서비스 사용자 이름)에 대한 자세한 내용은 다음을 참조하십시오.

- [클라이언트 연결의 SPN(서비스 사용자 이름) 지원](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> serverSpn 연결 특성은 Microsoft JDBC Driver 4.2 이상에서만 지원됩니다.

> JDBC 드라이버 6.2 이전의 릴리스에서는 **serverSpn**을 명시적으로 설정해야 합니다. 6\.2 릴리스부터는 **Serverspn** 을 명시적으로 사용할 수는 있지만 기본적으로 드라이버는 **Serverspn** 을 빌드할 수 있습니다.

## <a name="security-risks"></a>보안 위험

NTLM 프로토콜은 보안 위험을 야기하는 다양한 취약성이 있는 구 인증 프로토콜입니다. 상대적으로 약한 암호화 체계를 기반으로 하며 다양한 공격에 취약합니다. 이는 훨씬 더 안전하고 권장되는 Kerberos로 대체되었습니다. NTLM 인증은 안전한 신뢰할 수 있는 환경에서만 사용하거나 Kerberos를 사용할 수 없는 경우에만 사용해야 합니다.

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 원래 v1 프로토콜보다 몇 가지 보안 기능이 향상된 NTLM v2만 지원합니다. 또한 확장된 보호를 사용하도록 설정하거나 향상된 보안을 위해 SSL 암호화를 사용하는 것이 좋습니다. 

확장된 보호를 사용하도록 설정하는 방법에 대한 자세한 내용은 다음을 참조하세요.

- [확장된 보호를 사용하여 데이터베이스 엔진에 연결](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

SSL 암호화를 사용하여 연결하는 방법에 대한 자세한 내용은 다음을 참조하세요.

- [SSL 암호화를 사용한 연결](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 7\.4 릴리스의 경우 확장된 보호와 암호화를 **모두** 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 SQL Server에 연결](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
