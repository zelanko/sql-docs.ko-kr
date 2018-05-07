---
title: JDBC 드라이버에 대 한 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.openlocfilehash: 1ec71defcba0a6f122d3c3ff9a098e163f07079c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC 드라이버에 대 한 릴리스 정보
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>SQL Server 용 Microsoft JDBC Driver 6.4의 업데이트
SQL Server 용 Microsoft JDBC 드라이버 6.4 JDBC 사양 4.1 및 4.2와 완벽 하 게 호환 됩니다. 6.4 패키지에 포함 된 jar Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어 6.4 패키지에서 mssql-jdbc-6.4.0.jre8.jar 파일은 Java 8에서 사용 되는 것이 좋습니다. 

**JDK 9에 대 한 지원**  
  
Java 개발 키트 (JDK) 버전 9.0 JDK 8.0 및 7.0 외에도 지원 합니다.
  
**JDBC 4.3 규정 준수**  
  
4.1 및 4.2 외에도 Java 데이터베이스 연결 API 4.3 사양에 대 한 지원. JDBC 4.3 API 메서드가 추가 되었지만 아직 구현 되지 않았습니다. 자세한 내용은 [JDBC 드라이버에 대 한 JDBC 4.3 준수](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)합니다.
 
**새 연결 속성 추가: sslProtocol**

사용자가 TLS 프로토콜 키워드를 지정할 수 있는 새 연결 속성이 추가 되었습니다. 가능한 값은: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2"입니다. 참조 [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) 대 한 자세한 내용은 합니다.

**연결 속성을 사용 되지 않음: fipsProvider**

연결 속성이 "fipsProvider" 허용 된 연결 속성 목록에서 제거 됩니다. 세부 정보를 보려면 [여기](https://github.com/Microsoft/mssql-jdbc/pull/460)합니다.

**사용자 지정 TrustManager 지정 하기 위한 추가 연결 속성**

드라이버는 이제 trustManagerClass"추가" 및 "trustManagerConstructorArg" 연결 속성을 사용 하는 사용자 지정 TrustManager 지정을 지원 합니다. 따라서 JVM 환경에 대 한 전역 설정을 수정 하지 않고 연결 단위로에서 트러스트 하는 인증서 집합의 동적 지정 수 있습니다.

**Datetime/smallDatetime 테이블 반환 매개 변수 (TVP)에 대 한 지원 추가**

테이블 반환 매개 변수 (TVP)를 사용 하는 경우 드라이버는 이제 DATETIME 및 SMALLDATETIME 데이터 형식을 지원 합니다.

**Sql_variant 데이터 형식에 대 한 지원 추가**

JDBC 드라이버는 이제 SQL Server에서 사용 되는 sql_variant 데이터 형식을 지원 합니다. Sql_variant 제한 아래 테이블 반환 매개 변수 (TVP) 및 BulkCopy와 같은 기능으로 지원 됩니다.

1. 날짜 값에 대 한: sql_variant 열에 저장 된 datetime/smalldatetime/날짜 값이 포함 된 테이블을 채우기 위한 TVP를 사용할 때 결과 집합에서 getDateTime()/getSmallDateTime()/getDate() 메서드를 호출 작동 하지 않으며 다음 예외가 throw 됩니다.
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    해결 방법: "getString()" 또는 "getobject ()" 메서드를 대신 사용 합니다.

2. SQL Variant 된 TVP를 사용 하 여 null 값

TVP를 sql_variant 열 형식으로 NULL 값을 보내고 테이블을 채우는 데 사용 하는 경우 열 형식이 sql_variant 인 TVP에 있는 NULL 값을 삽입가 지원 되지 않으므로 현재 예외가 발생 합니다.

**준비 된 문을 구현 메타 데이터 캐싱**

JDBC 드라이버 성능 향상을 위한 준비 된 문의 메타 데이터 캐싱을 구현 했습니다. 드라이버는 이제 "disableStatementPooling" 및 "statementPoolingCacheSize" 연결 속성을 사용 하 여 드라이버에서 문 준비에 대 한 메타 데이터를 캐시를 지원합니다. 이 기능은 기본적으로 해제되어 있습니다. 자세한 내용은 [여기](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

**Linux/Mac에서 AAD 통합 인증에 대 한 지원 추가**

JDBC 드라이버는 이제 Azure Active Directory 통합 인증 모든 지원 운영 체제 (Windows/Linux/Mac) kerberos 인증도 지원합니다. 또는 Windows 운영 체제에서 사용자가 인증할 수 sqljdbc_auth.dll와 합니다.

**업데이트 ADAL4J 버전 1.4.0**

JDBC 드라이버 버전 1.4.0 azure-active directory-라이브러리-에-java (ADAL4J)에 해당 maven 종속성을 업데이트 했습니다. 종속성에 대 한 자세한 내용은 참조 [여기](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>SQL Server 용 Microsoft JDBC Driver 6.2의 업데이트
SQL Server 용 Microsoft JDBC 드라이버 6.2 JDBC 사양 4.1 및 4.2와 완벽 하 게 호환 됩니다. 6.0 패키지에 포함 된 jar Java 버전 호환성에 따라 이름이 지정 됩니다. 예를 들어 6.2 패키지에서 mssql-jdbc-6.2.1.jre8.jar 파일은 Java 8에서 사용 되는 것이 좋습니다. 

> [!NOTE]  
>  2017 년 6 월 29에 발표 JDBC 6.2 RTW에서 메타 데이터 캐싱 개선에 문제가 발견 되었습니다. 향상 롤백된 및에서 2017 년 7 월 17에 새 jar (6.2.1 버전) 발표 된는 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), 및 [Maven 중앙](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)합니다. 6.2.1를 사용 하 여 프로젝트를 업데이트 하십시오 jar를 해제 합니다. 참조 하십시오 [릴리스 정보](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) 내용을 확인 합니다.

**Linux 용 azure Active Directory (AAD) 지원**

사용자 이름/암호 및 액세스 토큰 메서드를 통해 AAD 인증을 사용 하 여 Azure SQL 데이터베이스에 Linux 응용 프로그램에 연결 합니다.

**연방 정보 FIPS (Processing Standard) Jvm을 사용 하도록 설정**

JDBC 드라이버에서 Jvm federal 표준 및 규정 준수를 충족 하기 위해 FIPS 140 호환성 모드에서 실행 하는 이제 사용할 수 있습니다. 

**Kerberos 인증의 향상 된 기능** 

현재 JDBC 드라이버에 대 한 지원을가지고 있습니다. 
* Kerberos 구성 수정 되거나 새 토큰 또는 keytab 검색할 수 없습니다 안 여기서 응용 프로그램에 대 한 사용자/암호 메서드. Kerberos 인증을 허용 하는 SQL Server에 인증 하기 위해이 메서드를 사용할 수 있습니다. 
* 상호 영역 인증 서버 SPN을 명시적으로 설정 하지 않고 Kerberos 통합 인증을 사용 합니다. 드라이버는 이제 자동으로 계산 영역 제공 되지 않은 경우에 합니다.
* Kerberos 제한 위임을 사용 하 여 데이터 원본을 통해 GSS 자격 증명 개체와 사용자 자격 증명을 가장합니다. 이 가장 된 자격 증명 Kerberos 연결에 사용 됩니다. 

**추가 된 시간 제한**

JDBC 드라이버는 이제 구성 가능한 시간 제한은 다음과 변경할 수 있습니다 응용 프로그램의 요구 사항에 따라 지원 합니다. 
* 쿼리 시간 제한 시간 초과 되기 전에 대기 하는 시간 (초) 수를 제어 하는 쿼리를 실행할 때 발생 합니다. 
* 소켓에서 시간 초과가 발생 하기 전 시간 (밀리초)의 수를 지정 하려면 소켓 제한 시간은 읽기 하거나 적용 합니다. 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>SQL Server 용 Microsoft JDBC Driver 6.1의 업데이트

SQL Server 용 Microsoft JDBC 드라이버 6.1 JDBC 사양 4.1 및 4.2와 완벽 하 게 호환 됩니다. 이 JDBC 드라이버의 오픈 소스 초기 릴리스 하며 Java 버전 호환성에 해당 하는 mssql-jdbc-6.1.0.jre8.jar mssql-jdbc-6.1.0.jre7.jar 파일을 포함 합니다. 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>SQL Server 용 Microsoft JDBC Driver 6.0의 업데이트

SQL Server 용 Microsoft JDBC Driver 6.0 JDBC 사양 4.1 및 4.2와 완벽 하 게 호환 됩니다. 6.0 패키지에 포함 된 jar 자신의 준수 JDBC API 버전에 따라 이름이 지정 됩니다. 예를 들어 6.0 패키지에서 sqljdbc42.jar 파일은 JDBC API 4.2 규격입니다. 마찬가지로, sqljdbc41.jar 파일 JDBC API 4.1와 호환 됩니다.

오른쪽 sqljdbc42.jar 또는 sqljdbc41.jar을 보장 하려면 다음 코드 줄을 실행 합니다. 출력은 하는 경우 "드라이버 버전: 6.0.7507.100", JDBC 드라이버 6.0 패키지를 포함 합니다.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **항상 암호화**  
  
 SQL Server 2016에서는 중요 한 데이터는 SQL Server 인스턴스를 일반 텍스트로 표시 되지 않습니다 보장 하는 새로운 보안 기능이 최근에 발표 된 상시 암호화 기능을 지원 합니다. 항상 암호화는 SQL Server에서 일반 텍스트 값이 아니라 암호화된 데이터만 처리하도록 응용 프로그램의 데이터를 투명하게 암호화하여 작동합니다. SQL 인스턴스 또는 호스트 컴퓨터가 손상 된 경우에 공격자가 얻을 수 있는 된 중요 한 데이터의 암호 텍스트입니다. 자세한 내용은 [상시 암호화와 JDBC 드라이버를 사용 하 여](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)합니다.  
  
 **다국어 도메인 이름 IDN)**  
  
 서버 이름에 대한 IDN(다국어 도메인 이름) 지원입니다. 자세한 내용은에 국제 도메인 이름 사용 하 여를 참조 하십시오.는 [JDBC 드라이버의 국제 기능](../../connect/jdbc/international-features-of-the-jdbc-driver.md) 페이지.  
  
 **매개 변수가 있는 쿼리**  
  
 이제 하위 쿼리 및/또는 조인과 같은 복합 쿼리를 위해 준비된 문을 사용하여 매개 변수 메타데이터를 검색할 수 있도록 지원합니다. 이러한 향상 기능은 SQL Server 2012 및 최신 버전을 사용하는 경우에만 사용할 수 있습니다.  
  
 **Azure Active Directory (AAD)**  
  
 AAD 인증은 Azure SQL 데이터베이스 v 12에 대 한 연결 메커니즘 AAD에서 id를 사용 합니다. AAD 인증을 사용 하 여 중앙에서 데이터베이스 사용자 및 SQL Server 인증 하는 대신 id를 관리 하 합니다. JDBC Driver 6.0을 사용 하면 Azure SQL DB에 연결 하는 데 JDBC 연결 문자열에서 AAD 자격 증명을 지정할 수 있습니다.  인증 속성을 참조는 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md) 페이지.  
  
 **테이블 반환 매개 변수**  
  
 테이블 반환 매개 변수는 쉽게 데이터 처리를 위한 여러 번 왕복 하거나 특수 한 서버측 논리를 요구 하지 않고 SQL Server 클라이언트 응용 프로그램에서 데이터의 여러 행을 마샬링할 수 있는 방법을 제공 합니다. 클라이언트 응용 프로그램에서 데이터 행을 캡슐화 하 고 서버는 단일 매개 변수가 있는 명령에는 데이터를 전송에 테이블 반환 매개 변수를 사용할 수 있습니다. 들어오는 데이터 행은 다음 작동 될 수 있는에 TRANSACT-SQL을 사용 하 여 테이블 변수에 저장 됩니다. 자세한 내용은 [Using Table-Valued 매개 변수](../../connect/jdbc/using-table-valued-parameters.md)합니다.  
  
 **AlwaysOn 가용성 그룹 (AG)**  
  
 드라이버는 이제 AlwaysOn 가용성 그룹에 대 한 투명 한 연결을 지원합니다. 빠르게 드라이버는 서버 인프라의 현재 AlwaysOn 토폴로지를 검색 하 고 투명 하 고 현재 활성 서버에 연결 합니다.  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>SQL Server용 Microsoft JDBC Driver 4.2 이상의 업데이트  
SQL Server 용 Microsoft JDBC Driver 4.2는 JDBC 사양 4.1 및 4.2 완벽 하 게 준수 합니다. 4.2 패키지에 포함 된 jar 자신의 준수 JDBC API 버전에 따라 이름이 지정 됩니다. 예를 들어 4.2 패키지에서 sqljdbc42.jar 파일은 JDBC API 4.2 규격입니다. 마찬가지로, sqljdbc41.jar 파일 JDBC API 4.1와 호환 됩니다.

오른쪽 sqljdbc42.jar 또는 sqljdbc41.jar을 보장 하려면 다음 코드 줄을 실행 합니다. 출력은 하는 경우 "드라이버 버전: 4.2.6420.100", JDBC Driver 4.2 패키지.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **JDK 8 지원**  
  
 JDK 7.0, 6.0 및 5.0 외에도 JDK(Java Development Kit) 버전 8.0을 지원합니다.  
  
 **JDBC 4.1 및 4.2 준수**  
  
 4.0 외에도 Java Database Connectivity API 4.1 및 4.2 사양을 지원합니다. 자세한 내용은 [JDBC 드라이버에 대 한 JDBC 4.1 준수](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) 및 [JDBC 드라이버의 JDBC 4.2 준수](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)합니다.  
  
 **대량 복사**  
  
 대량 복사 기능은 SQL Server 데이터베이스의 테이블이나 뷰에 많은 양의 데이터를 신속하게 복사하는 데 사용됩니다. 자세한 내용은 [JDBC 드라이버를 사용 하 여 대량 복사를 사용 하 여](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)합니다.  
  
 **XA 트랜잭션 롤백 옵션**  
  
 준비되지 않은 트랜잭션의 기존 자동 롤백에 대해 새로운 제한 시간 옵션이 추가되었습니다. 세부 정보를 참조 하십시오. [XA 트랜잭션 이해](../../connect/jdbc/understanding-xa-transactions.md)합니다.  
  
 **새 Kerberos 보안 주체 연결 속성**  
  
 Kerberos 연결을 유연하게 하는 새 연결 속성이 추가되었습니다. 세부 정보를 참조 하십시오. [Kerberos 통합 인증을 사용 하려면 SQL Server에 연결](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)합니다.  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>SQL Server용 Microsoft JDBC Driver 4.1 이상의 업데이트  
 **JDK 7 지원**  
  
 JDK 6.0 및 5.0 외에도 JDK(Java Development Kit) 버전 7.0을 지원합니다.  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium JDBC 드라이버 6.4, 6.0, 4.2 및 4.1 응용 프로그램에 대 한 지원 되지 않습니다  
  
 Microsoft JDBC Driver 6.4, 6.0, 4.2 및 4.1 SQL Server 응용 프로그램에 대 한 Itanium 컴퓨터에서 실행 되도록 지원 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

