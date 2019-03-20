---
title: JDBC 드라이버에 대 한 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3335e474819d43854bc3cf59158d04a78649c130
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57974362"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Microsoft JDBC Driver에 대 한 릴리스 정보

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 릴리스를 나열 합니다 _SQL Server 용 Microsoft JDBC Driver_합니다. 각 릴리스 버전에 대 한 변경 내용은 명명 되 고 설명 합니다.

## <a name="721"></a>7.2.1

### <a name="compliance"></a>호환성

2019년 2월 11일

| 규정 준수 변경 | 세부 정보 |
| :---------------- | :------ |
| JDBC 드라이버 7.2에 대 한 최신 업데이트를 다운로드 합니다. | &bull; &nbsp; [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 사양 4.2를 사용 하 여 완벽 하 게 준수 합니다. | 7.2 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다.<br/><br/>예를 들어, 7.2 패키지에서 mssql-jdbc-7.2.1.jre11.jar 파일 11 Java와 함께 사용할 해야 합니다. |
| JDK 1.8 외에도 JDK(Java Development Kit) 버전 11.0을 지원합니다. | SQL Server 용 Microsoft JDBC Driver 7.2 사용 하 여 개발 키트 (JDK (Java) 버전 11.0 JDK 1.8 외에도 호환 됩니다. |
| &nbsp; | &nbsp; |

> [!NOTE]
> 2019 년 1 월 31 일에 릴리스된 JDBC 7.2 릴리스를 웹 (RTW) 드라이버의 구문 분석 하는 SQL 문 사용 하 여 문제를 찾을 수 있습니다. 변경 내용이 롤백 되었습니다. 새 jar (버전 7.2.1)는 2019 년 2 월 11 일에 발표 된 하며
>
> 7.2.1를 사용 하 여 프로젝트를 업데이트 jar을 릴리스 합니다. 자세한 내용은 릴리스 정보를 볼 [7.2.1 GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1)합니다.

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Active Directory _관리 서비스 Id_ (MSI) 인증

| MSI 변경 | 세부 정보 |
| :--------- | :------ |
| Active Directory Service Identity MSI (관리) 인증 모드를 지원합니다. | 이 인증 모드를 "Identity" 기능 사용에 대 한 지원을 사용 하 여 Azure 리소스에 적용 됩니다.<br/><br/>양쪽의 시스템 Identities MSI (관리)을 가져오려고 드라이버가 지 원하는 **accessToken** 에 대 한 보안 연결을 설정 합니다. |
| 자세한 내용과이 인증 모드를 사용 하도록 샘플 응용 프로그램입니다. | [Azure Active Directory 인증을 사용하여 연결](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>소개 _Open 서비스 게이트웨이 Initiative_ (OSGi) 지원

| OSGi 변경 | 세부 정보 |
| :---------- | :------ |
| **DataSourceFactory** 구현을 추가 합니다. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **활성기** 구현을 추가 합니다. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>소개 _SQLServerError_ Api

| 오류 API 변경 | 세부 정보 |
| :--------------- | :------ |
| SQLServerError API를 도입 합니다. | 서버에서 생성 된 오류에 대 한 추가 세부 정보를 검색 하려면 Api getter입니다.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 추가 정보 | [오류 처리](../../connect/jdbc/handling-errors.md)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>업데이트된 _ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)_ 버전: 1.6.3

| ADAL4J 변경 | 세부 정보 |
| :------------ | :------ |
| ADAL4J에 대 한 해당 Maven 종속성 1.6.3 버전으로 업데이트 합니다. | &nbsp; |
| 소개 _AutoRest에 대 한 Java 클라이언트 런타임_ Maven 종속성 1.6.5 버전으로 합니다. | &nbsp; |
| 추가 정보 | [SQL Server용 Microsoft JDBC Driver의 기능 종속성](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>업데이트할 _Java 용 Microsoft Azure 키 자격 증명 모음 SDK_, 버전 1.2.0

| 키 자격 증명 모음 SDK 변경 | 세부 정보 |
| :------------------- | :------ |
| Maven 종속성 업데이트 _Java 용 Microsoft Azure 키 자격 증명 모음 SDK_ 버전 1.2.0으로 합니다. | &nbsp; |
| _Key Vault WebKey용 Microsoft Azure SDK_를 Maven 종속성(버전 1.2.0.)을 소개합니다. | &nbsp; |
| 추가 정보 | [SQL Server용 Microsoft JDBC Driver의 기능 종속성](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

| 알려진 문제 | 세부 정보 |
| :----------- | :------ |
| 일부 경우에는 매개 변수가 있는 쿼리. | 이 문제를 해결 하려면 2019 년 2 월 될 v7.2.1, 7.2 버전의 업데이트 출시 됩니다. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

SQL Server 용 Microsoft JDBC Driver 7.0 JDBC API 사양 4.2 완벽 하 게 호환 됩니다. 7.0 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어 10 Java를 사용 하 여 mssql-jdbc-7.0.0.jre10.jar 파일 7.0 패키지에서 사용할 해야 합니다.

### <a name="support-for-jdk-10"></a>JDK 10 지원

SQL Server 용 Microsoft JDBC Driver 7.0 사용 하 여 개발 키트 (JDK (Java) 버전 10.0 JDK 1.8 외에도 호환 됩니다. 이 업데이트에도 드라이버의 노출 `Automatic-Module-Name` 으로 `com.microsoft.sqlserver.jdbc` 해당 매니페스트 파일을 통해.

### <a name="support-for-spatial-datatypes"></a>공간 데이터 형식 지원

SQL Server 용 Microsoft JDBC Driver 7.0은 이제 SQL Server 공간 데이터 형식에 대해 Geography 및 Geometry 지원을 제공합니다. 공간 데이터 형식 Api 및 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [공간 데이터 형식을 사용 하 여](../../connect/jdbc/use-spatial-datatypes.md)입니다.

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3에서 도입된 java.sql.Connection API beginRequest() 및 endRequest()에 대한 구현

이제 구현 SQL Server 용 Microsoft JDBC 드라이버 7.0 `beginRequest()` 하 고 `endRequest()` 에서 Api를 `java.sql.Connection` 클래스입니다. 이러한 Api는 JDBC 4.3 사양 및 JDK 9를 사용 하 여 도입 되었습니다. 이러한 Api의 드라이버의 구현에 대 한 자세한 내용은 참조 하세요. [JDBC 드라이버의 JDBC 4.3 준수](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)합니다.

### <a name="support-for-sql-data-discovery-and-classification"></a>SQL 데이터 검색 및 분류 지원

SQL Server 용 Microsoft JDBC Driver 7.0 SQL 데이터 검색 및이 기능을 지 원하는 모든 대상 데이터베이스를 사용 하 여 분류에 대 한 지원을 제공 합니다. 드라이버는 이제 노출 `SQLServerResultSet.getSensitivityClassification()` 페치된에서이 정보를 추출 하는 Api `ResultSet`합니다.

JDBC 드라이버를 사용 하 여이 기능을 사용 하는 방법에 대 한 자세한 내용은에서 샘플을 참조 하세요 [SQL 데이터 검색 및 분류](../../connect/jdbc/data-discovery-classification-sample.md)합니다.

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>추가 연결 속성: useBulkCopyForBatchInsert

새 연결 속성을 소개 하는 SQL Server 용 Microsoft JDBC Driver 7.0 `useBulkCopyForBatchInsert`합니다. 이 속성은 Azure SQL Data Warehouse에 대해서만 지원 됩니다.

이 속성은 기본적으로 비활성화 됩니다. Azure SQL Data Warehouse로 많은 양의 데이터를 푸시하는 경우 사용자 응용 프로그램의 성능 향상을 위해 사용할 수 있습니다. 이 속성을 사용 하면 사용자가 제공한 데이터를 사용 하 여 대량 복사 작업으로 전환 하는 일괄 처리 삽입 작업의 동작을 변경 합니다. 이 속성 및 해당 제한 사항에 대 한 자세한 내용은 참조 하세요. [일괄 처리에 대 한 대량 복사 API를 사용 하 여 삽입 작업](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)합니다.

### <a name="added-connection-property-cancelquerytimeout"></a>추가 연결 속성: cancelQueryTimeout

새 연결 속성을 소개 하는 SQL Server 용 Microsoft JDBC Driver 7.0 `cancelQueryTimeout`, 취소 하려면 `queryTimeout` 온 `java.sql.Connection` 및 `java.sql.Statement` 개체.

### <a name="added-azure-key-vault-provider-constructors"></a>추가 된 Azure Key Vault Provider 생성자

SQL Server 용 Microsoft JDBC Driver 7.0 이전에 제거한 생성자에 대 한 다시 도입 되었습니다 `SQLServerColumnEncryptionAzureKeyVaultProvider`합니다. 통해 구현 된 사용자 지정 메서드를 통해 인증을 허용 하기 `SQLServerKeyVaultAuthenticationCallback` 액세스 토큰을 가져올 수 있습니다.

다음 정의 포함 하는 새 생성자:

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>업데이트된 "ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)" 버전: 1.6.0

SQL Server 용 Microsoft JDBC Driver 7.0 버전 1.6.0으로 "Microsoft Azure Active Directory 인증 라이브러리 (ADAL4J) Java에 대 한"에 대 한 해당 Maven 종속성을 업데이트 했습니다. 종속성에 대 한 자세한 내용은 참조 하세요. [SQL Server 용 Microsoft JDBC Driver의 종속성 기능](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)합니다.

## <a name="64"></a>6.4

SQL Server 용 Microsoft JDBC Driver 6.4 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. 6.4 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어 Java 8 사용 하 여 6.4 패키지에서 mssql-jdbc-6.4.0.jre8.jar 파일을 사용 해야 합니다.

### <a name="support-for-jdk-9"></a>JDK 9 지원

드라이버는 JDK 버전 9.0 JDK 8.0 및 7.0 외에도 지원합니다.

### <a name="jdbc-43-compliance"></a>JDBC 4.3 준수

드라이버는 4.1 및 4.2 외에도 Java Database Connectivity API 4.3 사양을 지원합니다. JDBC 4.3 API 메서드 추가 되었지만 아직 구현 되지 않았습니다. 자세한 내용은 [JDBC Driver의 JDBC 4.3 준수](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)를 참조하세요.

### <a name="added-connection-property-sslprotocol"></a>추가 연결 속성: sslProtocol

새 연결 속성을 TLS 프로토콜 키워드를 지정할 수 있도록 합니다. 가능한 값은: "TLS", "TLSv1", "TLSv1.1" 및 "TLSv1.2"입니다. 자세한 내용은 참조 하세요 [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)합니다.

### <a name="deprecated-connection-property-fipsprovider"></a>연결 속성을 사용 되지 않음: fipsProvider

연결 속성 `fipsProvider` 허용 된 연결 속성의 목록에서 제거 됩니다. 자세한 내용은 참조는 관련 [GitHub 끌어오기 요청](https://github.com/Microsoft/mssql-jdbc/pull/460)합니다.

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>사용자 지정 TrustManager를 지정 하기 위한 추가 연결 속성

이제는 사용자 지정 trustmanager를 사용 하 여 지원 추가 드라이버 `trustManagerClass` 고 `trustManagerConstructorArg` 연결 속성입니다. Java 가상 머신 (JVM) 환경에 대 한 전역 설정을 수정 하지 않고 각 연결 단위로 신뢰할 수 있는 인증서 집합을 동적으로 지정할 수 있습니다.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>테이블 반환 매개 변수의 datetime/smallDatetime에 대 한 지원 추가

드라이버는 이제 데이터 형식이 `datetime` 고 `smallDatetime` 테이블 반환 매개 변수 (Tvp)를 사용 하는 경우.

### <a name="added-support-for-the-sqlvariant-datatype"></a>Sql_variant 데이터 형식에 대 한 지원 추가

JDBC Driver에서는 이제 `sql_variant` SQL Server와 함께 사용 될 데이터 형식입니다. `sql_variant` Tvp 다음 제한 사항이 있는 대량 복사 등의 기능을 사용 하 여 데이터 형식이 지원 됩니다.

* **날짜 값**: 

  TVP를 사용 하는 포함 된 테이블을 채우는 데는 경우 `datetime`, `smalldatetime`, 또는 `date` 에 저장 된 값을 `sql_variant` 열에서 호출 합니다 `getDateTime()`, `getSmallDateTime()`, 또는 `getDate()` 메서드 결과 집합에서 작동 하지 않습니다 및 다음 예외가 throw 됩니다.

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  사용 하 여이 문제를 해결 합니다 `getString()` 또는 `getObject()` 메서드 대신 합니다.

* **null 값에 대한 sql_variant로 TVP 사용**:
  
  테이블을 채우고 NULL 값을 보낼 TVP를 사용 하는 경우는 `sql_variant` 열 형식 예외가 발생 합니다. 열 형식을 사용 하 여 NULL 값을 삽입할 `sql_variant` TVP 현재 지원 되지 않습니다.

### <a name="implemented-prepared-statement-metadata-caching"></a>준비 된 문 메타 데이터 캐싱이 구현

JDBC 드라이버는 성능 향상을 위한 준비 된 문 메타 데이터 캐싱이 구현 했습니다. 드라이버는 이제 사용 하 여에서 준비 된 문 메타 데이터 캐싱 `disableStatementPooling` 고 `statementPoolingCacheSize` 연결 속성입니다. 이 기능은 기본적으로 해제되어 있습니다. 자세한 내용은 [JDBC 드라이버에 대 한 문 메타 데이터 캐싱 준비](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)합니다.

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Linux/Mac에서 Azure AD 통합 인증에 대 한 지원 추가

또한 JDBC Driver는 이제 지원되는 모든 운영 체제(Windows, Linux, Mac)에서 Kerberos를 사용하여 Azure AD(Azure Active Directory) 통합 인증을 지원합니다. 또는 Windows 운영 체제에서는 사용자 sqljdbc_auth.dll을 사용 하 여 인증할 수 있습니다.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>업데이트된 "ADAL4J(Java용 Microsoft Azure Active Directory 인증 라이브러리)" 버전: 1.4.0

JDBC 드라이버 버전 1.4.0 "Microsoft Azure Active Directory 인증 라이브러리 (ADAL4J) Java에 대 한"에 대 한 해당 Maven 종속성을 업데이트 했습니다. 종속성에 대 한 자세한 내용은 참조 하세요. [SQL Server 용 Microsoft JDBC Driver의 종속성 기능](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)합니다.

## <a name="62"></a>6.2

SQL Server 용 Microsoft JDBC Driver 6.2 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. 6.2 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어, 6.2 패키지에서 mssql-jdbc-6.2.2.jre8.jar 파일을 사용 하 여 Java 8 사용 하 여 좋습니다.

> [!NOTE]  
> 2017 년 6 월 29 일에 릴리스된 JDBC 6.2 RTW 메타 데이터 캐싱 개선 문제가 발견 되었습니다. 향상 된 롤백되고 새 jar (버전 6.2.1)는 2017 년 7 월 17 일에 발표 된 합니다. 
>
> 향상 된 또 다른 Azure Key Vault 종속 라이브러리 버전을 1.0.0, 업그레이드 및 새 jar (버전 6.2.2)는 2017 년 10 월 19 일에 발표 된 합니다.
>
> JDBC Driver 6.2에 대 한 최신 업데이트를 다운로드 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=852460)하십시오 [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), 및 [Maven Central](https://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). 6.2.2를 사용 하 여 프로젝트를 업데이트 하십시오 jar을 릴리스 합니다. 자세한 내용은 릴리스 정보를 볼 [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) 하 고 [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)합니다.

### <a name="azure-ad-support-for-linux"></a>Linux 용 azure AD 지원

사용자 이름/암호 및 액세스 토큰 방법 사용 하 여 Azure AD 인증을 사용 하 여 Azure SQL Database로 Linux 응용 프로그램을 연결 합니다.

### <a name="fips-enabled-jvms"></a>FIPS 사용 Jvm

JDBC 드라이버 federal 준수 정책에 맞게 처리 표준 FIPS (Federal Information) 140 호환성 모드에서 실행 되는 Jvm에 이제 사용할 수 있습니다.

### <a name="kerberos-authentication-improvements"></a>Kerberos 인증 기능 향상

JDBC 드라이버는 이제에 대 한 지원이 있습니다.

- Kerberos 구성을 수정할 수 없습니다 또는 새 토큰 또는 키를 검색할 수 없습니다는 응용 프로그램에 대 한 사용자/암호 메서드. Kerberos 인증만 허용 하는 SQL Server 인스턴스를 인증 하기 위해이 메서드를 사용할 수 있습니다.
- 서버 SPN을 명시적으로 설정 하지 않고 Kerberos 통합 인증을 사용 하는 상호 영역 인증 합니다. 드라이버는 이제 자동으로 계산 영역 제공 되지 않는 경우에 합니다.
- Kerberos 제한 위임을 허용 하 여 데이터 원본을 통해 GSS 자격 증명 개체와 사용자 자격 증명을 가장합니다. 이 가장 된 자격 증명 Kerberos 연결에 사용 됩니다.

### <a name="added-timeouts"></a>추가 된 시간 제한

JDBC 드라이버는 이제 구성 가능한 시간을 지원합니다. 응용 프로그램의 요구 사항에 따라 변경할 수 있습니다.

- 쿼리를 실행 하는 경우 시간 초과가 발생 하기 전에 대기할 시간 (초) 수를 제어 하는 쿼리 제한 시간입니다.
- 소켓에서 시간 초과가 발생 하기 전에 대기할 시간을 밀리초 단위로 읽거나 허용 되도록 소켓 시간이 초과 되었습니다.

## <a name="61"></a>6.1

SQL Server 용 Microsoft JDBC Driver 6.1 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. 이것은 JDBC 드라이버의 초기 오픈 소스 릴리스입니다. Java 버전 호환성에 해당 하는 mssql-jdbc-6.1.0.jre8.jar 및 mssql-jdbc-6.1.0.jre7.jar 파일을 포함 합니다.

## <a name="60"></a>6.0

SQL Server 용 Microsoft JDBC Driver 6.0 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. Jar 6.0 패키지에는 JDBC API 버전을 사용 하 여 호환성에 따라 이름이 지정 됩니다. 예를 들어, sqljdbc42.jar 6.0 패키지에서 파일이 JDBC API 4.2 규격을 준수 합니다. 마찬가지로, sqljdbc41.jar 파일 API 용 JDBC 4.1 준수 됩니다.

오른쪽 sqljdbc42.jar 또는 sqljdbc41.jar 파일을 사용 했는지 확인을 하려면 다음 코드 줄을 실행 합니다. 출력은 하는 경우 "드라이버 버전: 6.0.7507.100", JDBC 드라이버 6.0 패키지 있습니다.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

드라이버는 SQL Server 2016에서 상시 암호화 기능을 지원합니다. 이 기능은 중요 한 데이터에서 SQL Server 인스턴스를 일반 텍스트로 적는 것을 확인 합니다. 항상 암호화는 SQL Server에서 일반 텍스트 값이 아니라 암호화된 데이터만 처리하도록 애플리케이션의 데이터를 투명하게 암호화하여 작동합니다. SQL Server 인스턴스 또는 호스트 머신이 손상된 경우에도 공격자가 얻을 수 있는 것은 중요한 데이터의 암호 텍스트뿐입니다. 자세한 내용은 [Always Encrypted와 JDBC Driver 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)을 참조하세요.

### <a name="internationalized-domain-names"></a>다국어 도메인 이름

드라이버는 서버 이름에 대 한 다국어 도메인 이름 (Idn)를 지원합니다. 자세한 내용은에서 "다국어 도메인 이름 사용"을 참조 합니다 [JDBC 드라이버의 국가별 기능](../../connect/jdbc/international-features-of-the-jdbc-driver.md) 문서.

### <a name="parameterized-queries"></a>매개 변수가 있는 쿼리

이제 드라이버는 하위 쿼리 및/또는 조인과 같은 복합 쿼리를 위해 준비된 문을 사용하여 매개 변수 메타데이터를 검색할 수 있도록 지원합니다. 이러한 향상 기능은 SQL Server 2012 및 최신 버전을 사용하는 경우에만 사용할 수 있습니다.

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 인증에 Azure AD에서 id를 사용 하 여 Azure SQL Database v12에 연결 하는 메커니즘입니다. 중앙에서 데이터베이스 사용자의 ID를 관리할 수 있는 Azure AD 인증은 SQL Server 인증 대신으로도 사용할 수 있습니다. 

Azure SQL Database에 연결할 JDBC 연결 문자열에서 Azure AD 자격 증명을 지정 하려면 JDBC Driver 6.0을 사용할 수 있습니다. 자세한 내용은에서 인증 속성을 참조를 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md) 문서.

### <a name="table-valued-parameters"></a>테이블 반환 매개 변수

TVP를 사용하면 데이터를 처리하는 데 여러 번 왕복하거나 서버 측 특수 논리를 설정하지 않고도 데이터의 여러 행을 클라이언트 애플리케이션에서 SQL Server로 쉽게 마샬링할 수 있습니다. 또한 TVP를 사용하면 클라이언트 애플리케이션에서 데이터 행을 캡슐화하고 매개 변수가 있는 단일 명령으로 데이터를 서버에 보낼 수 있습니다. 들어오는 데이터 행을 조작할 수 있습니다 다음 TRANSACT-SQL을 사용 하 여 테이블 변수에 저장 됩니다. 자세한 내용은 참조 하세요 [테이블 반환 매개 변수를 사용 하 여](../../connect/jdbc/using-table-valued-parameters.md)입니다.

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

드라이버는 이제 Always On 가용성 그룹에 대 한 투명 한 연결을 지원합니다. 또한 서버 인프라의 현재 Always On 토폴로지를 신속히 검색하여 현재 활성 서버에 투명하게 연결됩니다.

## <a name="42"></a>4.2

SQL Server 용 Microsoft JDBC Driver 4.2는 JDBC 사양 4.1 및 4.2와 완벽 하 게 준수 합니다. 4.2 패키지의 jar JDBC API 버전을 사용 하 여 호환성에 따라 이름이 지정 됩니다. 예를 들어, sqljdbc42.jar 4.2 패키지에서 파일이 JDBC API 4.2 규격을 준수 합니다. 마찬가지로, sqljdbc41.jar 파일 API 용 JDBC 4.1 준수 됩니다.

확인 오른쪽 sqljdbc42.jar 또는 sqljdbc41.jar 파일을 다음 코드 줄을 실행 해야 합니다. 출력은 하는 경우 "드라이버 버전: 4.2.6420.100", JDBC Driver 4.2 패키지를 포함 합니다.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>JDK 8 지원

드라이버는 JDK 8.0 외에도 JDK 7.0, 6.0 및 5.0 버전을 지원합니다.

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 및 4.2 준수

드라이버는 4.0 외에도 Java Database Connectivity API 4.1 및 4.2 사양을 지원합니다. 자세한 내용은 참조 하세요 [JDBC 드라이버의 JDBC 4.1 준수](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) 하 고 [JDBC 드라이버의 JDBC 4.2 준수](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)합니다.

### <a name="bulk-copy"></a>대량 복사

대량 복사 기능을 사용하여 SQL Server 데이터베이스의 테이블이나 뷰에 많은 양의 데이터를 신속하게 복사할 수 있습니다. 자세한 내용은 [JDBC Driver에서 대량 복사 사용](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)을 참조하세요.

### <a name="xa-transaction-rollback-option"></a>XA 트랜잭션 롤백 옵션

드라이버에 이제 준비되지 않은 트랜잭션의 기존 자동 롤백에 대해 새로운 제한 시간 옵션이 있습니다. 자세한 내용은 참조 하세요 [이해 XA 트랜잭션을](../../connect/jdbc/understanding-xa-transactions.md)합니다.

### <a name="new-kerberos-principal-connection-property"></a>새 Kerberos 보안 주체 연결 속성

드라이버는 새 연결 속성을 사용하여 Kerberos 연결을 유연하게 합니다. 자세한 내용은 [Kerberos 통합 인증을 사용하여 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)을 참조하세요.

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>JDK 7 지원

드라이버는 JDK 버전 7.0 JDK 6.0 및 5.0 외에도 지원합니다.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4, 6.0, 4.2 및 4.1 애플리케이션에서 Itanium이 지원되지 않음

SQL Server 애플리케이션용 Microsoft JDBC Driver 6.4, 6.0, 4.2 및 4.1은 Itanium 컴퓨터에서 실행할 수 없습니다.

## <a name="see-also"></a>관련 항목:

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)
