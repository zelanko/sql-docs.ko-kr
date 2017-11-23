---
title: "JDBC 드라이버 API 참조 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: "46"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1b58f4cd68ecafeec1c92ce42c92bfb5f29961a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="jdbc-driver-api-reference"></a>JDBC 드라이버 API 참조
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 제공 하는 API Java 내에서 사용할 수 있는 프로그래밍 코드에 연결 하 고 상호 작용 한 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
> [!NOTE]  
>  JDBC 드라이버를 사용 하는 방법에 대 한 개념 정보를 참조 하십시오. [JDBC 드라이버 개요](../../../connect/jdbc/overview-of-the-jdbc-driver.md)합니다.  
  
> [!IMPORTANT]  
>  JDBC 4.1 및 4.2 준수 지원에 대 한 Microsoft JDBC Driver 4.2 (또는 이상)를 사용 하 여 SQL Server에 대 한 합니다. Microsoft JDBC Driver 4.1 및 4.0 이전 릴리스에서는 JDBC 4.1 또는 4.2에 도입된 새로운 메서드가 지원되지 않습니다.  
>   
>  JDBC 4.1 준수에 대한 API 세부 정보는 이 섹션에서 제공하지 않습니다. 참조 [JDBC 4.1 준수 JDBC 드라이버에 대 한](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)합니다.  
>   
>  JDBC 4.2 준수에 대한 API 세부 정보는 이 섹션에서 제공하지 않습니다. 참조 [JDBC 4.2 JDBC 드라이버에 대 한 준수](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)합니다.  
>   
>  이 섹션에는 SQL Server 용 Microsoft JDBC Driver 4.2부터 사용할 수 있는 대량 복사에 대 한 API 세부 정보를 찾을 수 없습니다. 참조 [대량 복사를 사용 하 여 JDBC 드라이버와 함께](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)합니다.  
>   
>  이 섹션에는 상시 암호화, SQL Server 용 Microsoft JDBC Driver 6.0부터 사용할 수에 대 한 API 세부 정보를 찾을 수 없습니다. 참조 [상시 암호화는 JDBC 드라이버에 대 한 API 참조](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  이 섹션에는 Using Table-Valued 매개 변수를 사용할 수 있는 SQL Server 용 Microsoft JDBC Driver 6.0부터에 대 한 API 세부 정보를 찾을 수 없습니다. 참조 [테이블 반환 매개 변수를 사용 하 여](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.0 및 JDK 5.0, 6.0, 7.0 및 8.0을 사용한 컴파일을 4.2 지원 합니다.  
>   
>  Microsoft JDBC Driver 4.1에서는 JDK 5.0, 6.0 및 7.0을 사용한 컴파일을 지원합니다.  
>   
>  Microsoft JDBC Driver 4.0에서는 JDK 5.0 및 6.0을 사용한 컴파일이 지원됩니다.  
  
## <a name="interfaces"></a>인터페이스  
  
|인터페이스 이름|Description|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement 인터페이스](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|입력 및 출력 매개 변수와 함께 호출할 저장 프로시저 이름을 지정할 수 있도록 합니다.|  
|[ISQLServerConnection 인터페이스](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|JDBC 연결을 나타내며는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|에 연결 하는 데 관련 된 속성 목록을 나타냅니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 사용 하 여 데이터베이스를 [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|JDBC의 준비된 문 기능에 대한 기본 구현을 나타냅니다.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|JDBC 결과 집합을 나타냅니다.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|JDBC 문 기능의 기본 구현을 나타냅니다.|  
  
## <a name="classes"></a>클래스  
  
|클래스 이름|Description|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|microsoft.sql.DateTimeOffset 형식의 개체를 나타냅니다.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|BLOB(Binary Large Object)을 나타냅니다.|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|ISQLServerCallableStatement를 구현합니다.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|CLOB(Character Large Binary Object)을 나타냅니다.|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|ISQLServerConnection을 구현합니다.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|연결 풀 관리자를 위한 실제 데이터베이스 연결을 나타냅니다.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|데이터베이스의 메타데이터를 나타냅니다.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|에 연결 하는 데 관련 된 속성 목록을 나타냅니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 사용 하 여 데이터베이스를 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|JNDI(Java Naming and Directory Interface)의 데이터 원본을 구체화하기 위한 개체 팩터리를 나타냅니다.|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|JDBC 드라이버를 나타냅니다. 이 클래스에 연결 하기 위한 메서드를 포함 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터베이스, JDBC 드라이버에 대 한 정보를 얻기 위한 합니다.|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|실패하거나 완료되지 않은 SQL 문 실행을 나타냅니다.|  
|[SQLServerNClob 클래스](../../../connect/jdbc/reference/sqlservernclob-class.md)|국가별 문자 집합을 사용하여 CLOB(Character Large Binary Object)을 나타냅니다.|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|준비된 문 매개 변수의 메타데이터를 나타냅니다.|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|연결 풀의 실제 데이터베이스 연결을 나타냅니다.|  
|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|ISQLServerPreparedStatement를 구현합니다.|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|지역화된 오류 문자열 리소스를 나타냅니다. 이 클래스는 내부 전용입니다.|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|ISQLServerResultSet을 구현합니다.|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|결과 집합에 포함된 열의 메타데이터를 나타냅니다.|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|트랜잭션에서 롤백할 수 있는 검사점을 나타냅니다.|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|ISQLServerStatement를 구현합니다.|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|분산(XA) 트랜잭션에 참여할 수 있는 JDBC 연결을 나타냅니다.|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|에 대 한 팩터리를 나타내는 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 내부적으로 사용 되는 개체입니다.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|XAResource 나타냅니다 XA에 대 한 분산 트랜잭션 관리 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
