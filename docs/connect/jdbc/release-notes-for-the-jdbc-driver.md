---
title: JDBC 드라이버에 대 한 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10f14eedb1a74f74cb1ee055a247a96671224ce0
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662465"
---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC 드라이버에 대한 릴리스 정보

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-70-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver 7.0의 업데이트

SQL Server 용 Microsoft JDBC Driver 7.0 JDBC API 사양 4.2 완벽 하 게 호환 됩니다. 7.0 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어 10 Java를 사용 하 여 mssql-jdbc-7.0.0.jre10.jar 파일 7.0 패키지에서 사용할 해야 합니다.

### <a name="support-for-jdk-10"></a>JDK 10 지원

SQL Server 용 Microsoft JDBC Driver 7.0 사용 하 여 개발 키트 (JDK (Java) 버전 10.0 JDK 1.8 외에도 호환 됩니다. 이 업데이트는 또한 드라이버의 ' 자동-모듈-이름 '으로 노출 `com.microsoft.sqlserver.jdbc` 해당 매니페스트 파일을 통해.

### <a name="support-for-spatial-datatypes"></a>공간 데이터 형식에 대한 지원

SQL Server 용 Microsoft JDBC Driver 7.0에는 이제 SQL Server 공간 데이터 형식 'Geography' 및 '기 하 도형'에 대 한 지원을 제공합니다. 공간 데이터 형식 Api 및 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [여기](../../connect/jdbc/use-spatial-datatypes.md)합니다.

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3에서 도입된 java.sql.Connection API beginRequest() 및 endRequest()에 대한 구현

이제 구현 SQL Server 용 Microsoft JDBC 드라이버 7.0 `beginRequest()` 하 고 `endRequest()` 에서 Api `java.sql.Connection` 클래스입니다. 이러한 Api는 JDBC 4.3 사양 및 JDK 9를 사용 하 여 도입 되었습니다. 이러한 Api의 드라이버의 구현에 대 한 자세한 내용은 참조 하세요. [여기](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)합니다.

### <a name="support-for-sql-data-discovery-and-classification"></a>‘SQL 데이터 검색 및 분류’ 지원

SQL Server 용 Microsoft JDBC Driver 7.0이이 기능을 지 원하는 모든 대상 데이터베이스를 사용 하 여 'SQL 데이터 검색 및 분류' 기능에 대 한 지원을 제공 합니다. 드라이버는 이제 노출 `SQLServerResultSet.getSensitivityClassification()` Api 인출된 결과 집합에서이 정보를 추출 합니다.

JDBC 드라이버를 사용 하 여이 기능을 사용 하는 방법에 대 한 자세한 내용은 샘플을 참조 하세요 [여기](../../connect/jdbc/data-discovery-classification-sample.md)합니다.

### <a name="added-new-connection-property-usebulkcopyforbatchinsert"></a>새 연결 속성을 추가 합니다: useBulkCopyForBatchInsert

SQL Server 용 Microsoft JDBC Driver 7.0에서는 새 연결 속성을 'useBulkCopyForBatchInsert' 에서만 지원 됩니다 **Azure Data Warehouse**합니다.

이 속성은 **비활성화** 하 여 기본 및 Azure Data Warehouse에 데이터를 금액 큰 푸시할 때 사용자 응용 프로그램의 성능을 향상 하는 데 사용할 수 있습니다. 이 속성을 사용 하면 사용자가 제공한 데이터를 사용 하 여 대량 복사 작업으로 전환 일괄 삽입 작업의 동작을 변경 합니다. 이 속성 및 해당 제한 사항에 대 한 자세한 내용은 참조 [여기](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)합니다.

### <a name="added-new-connection-property-cancelquerytimeout"></a>새 연결 속성을 추가 합니다: cancelQueryTimeout

새 연결 속성을 소개 하는 SQL Server 용 Microsoft JDBC Driver 7.0 `cancelQueryTimeout`, 취소 하려면 `queryTimeout` 에 `java.sql.Connection` 및 `java.sql.Statement` 개체입니다.

### <a name="added-azure-key-vault-provider-constructors"></a>추가 Azure Key Vault 공급자 생성자

SQL Server 용 Microsoft JDBC Driver 7.0 이전에 제거한 생성자에 대 한 다시 도입 되었습니다 `SQLServerColumnEncryptionAzureKeyVaultProvider`를 통해 구현 되는 사용자 지정 메서드를 사용 하 여 허용 되는 인증 `SQLServerKeyVaultAuthenticationCallback` 액세스 토큰을 가져올 수 있습니다.

새 생성자를 정의 아래:

```java
/* This constructor is added to provide backwards compatibility with 6.0
* version of the driver. It is marked deprecated for removal in next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New Constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-adal4j-version-to-160"></a>1.6.0으로 업데이트 된 ADAL4J 버전

SQL Server 용 Microsoft JDBC Driver 7.0 버전 1.6.0 azure-activedirectory-라이브러리-에-java (ADAL4J) 해당 maven 종속성을 업데이트 했습니다. 종속성에 대한 자세한 내용은 [여기](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)를 참조하세요.

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver 6.4의 업데이트

SQL Server 용 Microsoft JDBC Driver 6.4 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. 6.4 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어 Java 8 사용 하 여 6.4 패키지에서 mssql-jdbc-6.4.0.jre8.jar 파일을 사용 해야 합니다.

### <a name="support-for-jdk-9"></a>JDK 9 지원

JDK 8.0 및 7.0 외에도 JDK(Java Development Kit) 버전 9.0을 지원합니다.

### <a name="jdbc-43-compliance"></a>JDBC 4.3 준수

4.1 및 4.2 외에도 Java Database Connectivity API 4.3 사양을 지원합니다. JDBC 4.3 API 메서드 추가 되었지만 아직 구현 되지 않았습니다. 자세한 내용은 [JDBC Driver의 JDBC 4.3 준수](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)를 참조하세요.

### <a name="added-new-connection-property-sslprotocol"></a>새 연결 속성을 추가 합니다: sslProtocol

사용자가 TLS 프로토콜 키워드를 지정할 수 있는 새 연결 속성을 추가 합니다. 가능한 값은: "TLSv1.2", "TLSv1.1", "TLSv1", "TLS"입니다. 참조 [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) 세부 정보에 대 한 합니다.

### <a name="deprecated-connection-property-fipsprovider"></a>연결 속성을 사용 되지 않음: fipsProvider

연결 속성 "fipsProvider" 허용 된 연결 속성의 목록에서 제거 됩니다. 세부 정보를 보려면 [여기](https://github.com/Microsoft/mssql-jdbc/pull/460)합니다.

### <a name="added-connection-properties-for-specifying-custom-trustmanager"></a>사용자 지정 TrustManager를 지정 하기 위한 추가 연결 속성

드라이버는 이제 trustManagerClass"추가" 및 "trustManagerConstructorArg" 연결 속성을 사용 하 여 사용자 지정 trustmanager를 지원 합니다. 따라서 동적 JVM 환경에 대 한 전역 설정을 수정 하지 않고 연결 별로에서 신뢰할 수 있는 인증서 집합을 지정 합니다.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters-tvp"></a>Datetime/smallDatetime 테이블 반환 매개 변수 (TVP)에 대 한 지원 추가

드라이버는 이제 TVP(테이블 반환 매개 변수)를 사용할 때 DATETIME 및 SMALLDATETIME 데이터 형식을 지원합니다.

### <a name="added-support-for-sqlvariant-datatype"></a>Sql_variant 데이터 형식에 대 한 지원 추가

JDBC 드라이버는 이제 SQL Server를 사용 하 여 사용할 sql_variant 데이터 형식이 지원 합니다. Sql_variant 제한 아래 테이블 반환 매개 변수 (TVP) 사용 하 여 BulkCopy 등의 기능을 사용 하 여 지원 됩니다.

1. 날짜 값에 대 한: sql_variant 열에 저장 하는 datetime/smalldatetime/날짜 값이 포함 된 테이블을 채우기 위한 TVP를 사용할 때 결과 집합에서 getDateTime()/getSmallDateTime()/getDate() 메서드를 호출 작동 하지 않습니다 하 고 다음 예외를 throw 합니다.  `java java.lang.String cannot be cast to java.sql.Timestamp` 해결 방법: "getstring ()" 또는 "getobject ()" 메서드를 대신 사용 합니다.

2. null 값에 대한 SQL VARIANT로 TVP 사용

TVP를 사용 하 여 테이블을 채우고 sql_variant 열 형식으로 NULL 값을 전송 하는, 하는 경우 TVP에 열 형식이 sql_variant 인을 사용 하 여 삽입 NULL 값이 현재 지원 되지 예외가 발생할 수 있습니다.

### <a name="implemented-prepared-statement-metadata-caching"></a>준비 된 문을 구현 메타 데이터 캐싱

JDBC 드라이버 성능 향상을 위한 준비 된 문 메타 데이터 캐싱이 구현 했습니다. 드라이버는 이제 "disableStatementPooling" 및 "statementPoolingCacheSize" 연결 속성을 사용 하 여 드라이버에서 문 준비에 대 한 메타 데이터를 캐시를 지원합니다. 이 기능은 기본적으로 해제되어 있습니다. 자세한 내용은 [여기](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)를 참조하세요.

### <a name="added-support-for-aad-integrated-authentication-on-linuxmac"></a>Linux/Mac에서 AAD 통합 인증에 대 한 지원 추가

또한 JDBC Driver는 이제 지원되는 모든 운영 체제(Windows/Linux/Mac)에서 Kerberos를 사용하여 Azure Active Directory 통합 인증을 지원합니다. 또는 Windows 운영 체제에서 사용자가 인증할 수 sqljdbc_auth.dll을 사용 하 여 합니다.

### <a name="updated-adal4j-version-to-140"></a>업데이트 된 ADAL4J 버전 1.4.0

JDBC 드라이버 버전 1.4.0 azure-activedirectory-라이브러리-에-java (ADAL4J) 해당 maven 종속성을 업데이트 했습니다. 종속성에 대한 자세한 내용은 [여기](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)를 참조하세요.

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver 6.2의 업데이트

SQL Server 용 Microsoft JDBC Driver 6.2 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. 6.2 패키지에 jar이 Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어, 6.2 패키지에서 mssql-jdbc-6.2.2.jre8.jar 파일은 Java 8 사용 하 여 사용할 것이 좋습니다.

> [!NOTE]  
> 2017 년 6 월 29 일에 릴리스된 JDBC 6.2 RTW 메타 데이터 캐싱 개선 문제가 발견 되었습니다. 향상 된 롤백되고 새 jar (버전 6.2.1)는 2017 년 7 월 17 일에 발표 된 합니다. 
>
> Azure Key Vault 종속 라이브러리 버전 1.0.0로 업그레이드 하는 또 다른 개선 사항은 만들었고 새 jar (버전 6.2.2)는 2017 년 10 월 19 일에 발표 된 합니다.
>
> 에 JDBC Driver 6.2에 최신 업데이트를 다운로드 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=852460)를 [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), 및 [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)합니다. 6.2.2를 사용 하 여 프로젝트를 업데이트 하십시오 jar을 릴리스 합니다. 에 대 한 릴리스 정보를 확인 하세요 [v6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) 하 고 [v6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) 대 한 자세한 내용은 합니다.

### <a name="azure-active-directory-aad-support-for-linux"></a>Linux 용 azure Active Directory (AAD) 지원

Linux 응용 프로그램 사용자 이름/암호 및 액세스 토큰 방법 사용 하 여 AAD 인증을 사용 하 여 Azure SQL Database에 연결 합니다.

### <a name="federal-information-processing-standard-fips-enabled-jvms"></a>처리 표준 FIPS (Federal Information) Jvm을 사용 하도록 설정

JDBC 드라이버에서 Jvm federal 및 규정 준수를 충족 하기 위해 FIPS 140 호환성 모드에서 실행 되는 이제 사용할 수 있습니다.

### <a name="kerberos-authentication-improvements"></a>Kerberos 인증 기능 향상

JDBC 드라이버는 이제에 대 한 지원이 있습니다.

- 여기서 Kerberos 구성을 수정할 수 없거나 새 토큰 또는 키를 검색할 수 없습니다 응용 프로그램에 대 한 사용자/암호 메서드. 이 메서드는만 Kerberos 인증을 허용 하는 SQL Server 인증에 사용할 수 있습니다.
- Kerberos 통합 인증을 사용 하 여 명시적으로 서버 SPN을 설정 하지 않고 상호 영역 인증 합니다. 드라이버는 이제 자동으로 계산 영역 답변이 제공 하는 경우에 합니다.
- Kerberos 제한 위임을 허용 하 여 데이터 원본을 통해 GSS 자격 증명 개체와 사용자 자격 증명을 가장합니다. 이 가장 된 자격 증명 Kerberos 연결에 사용 됩니다.

### <a name="added-timeouts"></a>추가 된 시간 제한

JDBC 드라이버는 이제 구성 가능한 시간을 변경할 수 있습니다 응용 프로그램의 요구 사항에 따라 지원 합니다.

- 쿼리를 실행 하는 경우 시간 초과가 발생 하기 전에 대기할 시간 (초) 수를 제어 하는 쿼리 제한 시간입니다.
- 소켓에서 시간 초과가 발생 하기 전에 대기할 시간을 밀리초 단위로 읽거나 허용 되도록 소켓 시간이 초과 되었습니다.

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver 6.1의 업데이트

SQL Server 용 Microsoft JDBC Driver 6.1 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. 이 JDBC 드라이버의 최초 오픈 소스 릴리스 하며 Java 버전 호환성에 해당 하는 mssql-jdbc-6.1.0.jre8.jar mssql-jdbc-6.1.0.jre7.jar 파일을 포함 합니다.

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver 6.0의 업데이트

SQL Server 용 Microsoft JDBC Driver 6.0 4.1 및 4.2 JDBC 사양을 완벽 하 게 호환 됩니다. Jar 6.0 패키지에는 JDBC API 버전을 사용 하 여 호환성에 따라 이름이 지정 됩니다. 예를 들어, sqljdbc42.jar 6.0 패키지에서 파일이 JDBC API 4.2 규격을 준수 합니다. 마찬가지로, sqljdbc41.jar 파일 API 용 JDBC 4.1 준수 됩니다.

오른쪽 sqljdbc42.jar 또는 sqljdbc41.jar을 보장 하려면 다음 코드 줄을 실행 합니다. 출력은 하는 경우 "드라이버 버전: 6.0.7507.100", JDBC 드라이버 6.0 패키지 있습니다.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>항상 암호화

SQL Server 인스턴스에서 중요한 데이터가 결코 일반 텍스트로 표시되지 않도록 하는 새로운 보안 기능인 SQL Server 2016의 최근에 출시된 상시 암호화 기능을 지원합니다. 항상 암호화는 SQL Server에서 일반 텍스트 값이 아니라 암호화된 데이터만 처리하도록 응용 프로그램의 데이터를 투명하게 암호화하여 작동합니다. SQL 인스턴스 또는 호스트 머신이 손상된 경우에도 공격자가 얻을 수 있는 것은 중요한 데이터의 암호 텍스트뿐입니다. 자세한 내용은 [Always Encrypted와 JDBC Driver 사용](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)을 참조하세요.

### <a name="internationalized-domain-name-idn"></a>IDN(다국어 도메인 이름)

서버 이름에 대한 IDN(다국어 도메인 이름) 지원입니다. 세부 정보를 사용 하 여 국제 도메인 이름에 대 한 참조를 [JDBC 드라이버의 국가별 기능](../../connect/jdbc/international-features-of-the-jdbc-driver.md) 페이지입니다.

### <a name="parameterized-query"></a>매개 변수가 있는 쿼리(parameterized query)

이제 하위 쿼리 및/또는 조인과 같은 복합 쿼리를 위해 준비된 문을 사용하여 매개 변수 메타데이터를 검색할 수 있도록 지원합니다. 이러한 향상 기능은 SQL Server 2012 및 최신 버전을 사용하는 경우에만 사용할 수 있습니다.

### <a name="azure-active-directory-aad"></a>AAD(Azure Active Directory)

AAD 인증을 사용 하면 Azure SQL Database v12에 연결 하는 장치가 AAD에서 id를 사용 합니다. 중앙에서 데이터베이스 사용자의 ID를 관리할 수 있는 AAD 인증은 SQL Server 인증 대신으로도 사용할 수 있습니다. JDBC Driver 6.0을 사용하면 JDBC 연결 문자열에서 Azure SQL DB에 연결할 AAD 자격 증명을 지정할 수 있습니다. 세부 정보는 인증 속성에 대 한 참조를 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md) 페이지입니다.

### <a name="table-valued-parameters"></a>테이블 반환 매개 변수

테이블 반환 매개 변수를 사용하면 데이터를 처리하는 데 여러 번 왕복하거나 서버 측 특수 논리를 설정하지 않고도 데이터의 여러 행을 클라이언트 응용 프로그램에서 SQL Server로 쉽게 마샬링할 수 있습니다. 또한 테이블 반환 매개 변수를 사용하면 클라이언트 응용 프로그램에서 데이터 행을 캡슐화하고 매개 변수가 있는 단일 명령으로 데이터를 서버에 보낼 수 있습니다. 들어오는 데이터 행은 다음 작동할 수 있는에서 TRANSACT-SQL을 사용 하 여 테이블 변수에 저장 됩니다. 자세한 내용은 참조 하세요 [Using Table-Valued 매개 변수](../../connect/jdbc/using-table-valued-parameters.md)합니다.

### <a name="alwayson-availability-groups-ag"></a>AlwaysOn AG(가용성 그룹)

드라이버는 이제 AlwaysOn 가용성 그룹에 대 한 투명 한 연결을 지원합니다. 또한 서버 인프라의 현재 AlwaysOn 토폴로지를 신속히 검색하여 현재 활성 서버에 투명하게 연결됩니다.

## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>SQL Server용 Microsoft JDBC Driver 4.2 이상의 업데이트

SQL Server 용 Microsoft JDBC Driver 4.2는 JDBC 사양 4.1 및 4.2 완벽 하 게 호환 됩니다. 4.2 패키지의 jar JDBC API 버전을 사용 하 여 호환성에 따라 이름이 지정 됩니다. 예를 들어, sqljdbc42.jar 4.2 패키지에서 파일이 JDBC API 4.2 규격을 준수 합니다. 마찬가지로, sqljdbc41.jar 파일 API 용 JDBC 4.1 준수 됩니다.

오른쪽 sqljdbc42.jar 또는 sqljdbc41.jar을 보장 하려면 다음 코드 줄을 실행 합니다. 출력은 하는 경우 "드라이버 버전: 4.2.6420.100", JDBC Driver 4.2 패키지를 포함 합니다.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>JDK 8 지원

JDK 7.0, 6.0 및 5.0 외에도 JDK(Java Development Kit) 버전 8.0을 지원합니다.

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 및 4.2 준수

4.0 외에도 Java Database Connectivity API 4.1 및 4.2 사양을 지원합니다. 자세한 내용은 참조 하세요 [JDBC 드라이버의 JDBC 4.1 준수](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) 하 고 [JDBC 드라이버의 JDBC 4.2 준수](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)합니다.

### <a name="bulk-copy"></a>대량 복사

대량 복사 기능은 SQL Server 데이터베이스의 테이블이나 뷰에 많은 양의 데이터를 신속하게 복사하는 데 사용됩니다. 자세한 내용은 [JDBC Driver에서 대량 복사 사용](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)을 참조하세요.

### <a name="xa-transaction-rollback-option"></a>XA 트랜잭션 롤백 옵션

준비되지 않은 트랜잭션의 기존 자동 롤백에 대해 새로운 제한 시간 옵션이 추가되었습니다. 자세한 내용은 참조 하세요 [XA 트랜잭션 이해](../../connect/jdbc/understanding-xa-transactions.md)합니다.

### <a name="new-kerberos-principal-connection-property"></a>새 Kerberos 보안 주체 연결 속성

Kerberos 연결을 유연하게 하는 새 연결 속성이 추가되었습니다. 자세한 내용은 [Kerberos 통합 인증을 사용하여 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)을 참조하세요.

## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>SQL Server용 Microsoft JDBC Driver 4.1 이상의 업데이트

### <a name="support-for-jdk-7"></a>JDK 7 지원

JDK 6.0 및 5.0 외에도 JDK(Java Development Kit) 버전 7.0을 지원합니다.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4, 6.0, 4.2 및 4.1 응용 프로그램에서 Itanium이 지원되지 않음

SQL Server 응용 프로그램용 Microsoft JDBC Driver 6.4, 6.0, 4.2 및 4.1은 Itanium 컴퓨터에서 실행할 수 없습니다.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)
