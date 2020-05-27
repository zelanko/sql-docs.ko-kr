---
title: JDBC 드라이버 API 참조 | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04cbe39698a99fbde43043b70bb9b1f0e5887f58
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977004"
---
# <a name="jdbc-driver-api-reference"></a>JDBC 드라이버 API 참조

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 Java 프로그래밍 코드 내에서 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하고 조작하는 데 사용할 수 있는 API를 제공합니다.



### <a name="javadocio-website-is-primary"></a>JavaDoc.io가 기본 웹 사이트

Microsoft JDBC API 참조 설명서는 JavaDoc.io 웹 사이트에서 볼 수 있도록 호스트됩니다. JavaDoc.io는 이제 JDBC 참조 설명서에 대한 기본 웹 사이트입니다. JavaDoc.io에서 다음 직접 링크를 통해 JDBC 참조 설명서를 이용할 수 있습니다.

- [https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/](https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/)

JavaDoc.io에는 버전 6.0부터 JDBC 참조 설명서가 있습니다.

#### <a name="only-legacy-jdbc-documentation-is-here-on-docs"></a>레거시 JDBC 설명서는 여기 Docs에서만 제공

새 릴리스에 대해 JDBC 클래스를 업데이트할 때 여기 **https://docs.microsoft.com/sql/connect/jdbc/reference/** 에서는 JDBC API 참조 설명서 문서가 더 이상 업데이트되지 않습니다. 그러나 여기에 있는 문서에는 JDBC 버전 4.1 및 4.2에 대한 모든 참조가 포함됩니다.

JDBC 버전 6.0 및 일부 이후 버전에 대한 설명서도 여기에 있습니다. 그러나 버전 6.0 이상은 JavaDoc.io 웹 사이트를 사용하세요.



### <a name="important-notes"></a>중요 사항

> [!NOTE]  
>  JDBC 드라이버를 사용하는 방법에 대한 개념 정보는 [JDBC 드라이버 개요](../../../connect/jdbc/overview-of-the-jdbc-driver.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  JDBC 4.1 및 4.2 준수를 지원하려면 SQL Server용 Microsoft JDBC Driver 4.2 이상을 사용하세요. Microsoft JDBC Driver 4.1 및 4.0 이전 릴리스에서는 JDBC 4.1 또는 4.2에 도입된 새로운 메서드가 지원되지 않습니다.  
>   
>  JDBC 4.1 준수에 대한 API 세부 정보는 이 섹션에서 제공하지 않습니다. [JDBC 드라이버의 JDBC 4.1 준수](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)를 참조하세요.  
>   
>  JDBC 4.2 준수에 대한 API 세부 정보는 이 섹션에서 제공하지 않습니다. [JDBC 드라이버의 JDBC 4.2 준수](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)를 참조하세요.  
>   
>  SQL Server용 Microsoft JDBC Driver 4.2부터 사용할 수 있는 대량 복사 기능에 대한 API 세부 정보는 이 섹션에서 제공하지 않습니다. [JDBC 드라이버에서 대량 복사 사용](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)을 참조하세요.  
>   
>  이 섹션에는 SQL Server용 Microsoft JDBC Driver 6.0부터 사용할 수 있는 Always Encrypted에 대한 API 세부 정보는 없습니다. [JDBC 드라이버에 대해 Always Encrypted API 참조](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)를 참조  
>   
>  이 섹션에는 Microsoft JDBC Driver 6.0 for SQL Server부터 사용할 수 있는 테이블 반환 매개 변수 사용에 대한 API 세부 정보는 없습니다. [테이블 반환 매개 변수 사용](../../../connect/jdbc/using-table-valued-parameters.md) 참조  
>   
>  Microsoft JDBC Driver 6.4에서는 JDK 7.0, 8.0 및 9.0을 사용한 컴파일이 지원됩니다.  
>   
>  Microsoft JDBC Driver 6.2에서는 JDK 7.0 및 8.0을 사용한 컴파일이 지원됩니다.  
>   
>  Microsoft JDBC Driver 6.0 및 4.2에서는 JDK 5.0, 6.0, 7.0 및 8.0을 사용한 컴파일이 지원됩니다.  
>   
>  Microsoft JDBC Driver 4.1에서는 JDK 5.0, 6.0 및 7.0을 사용한 컴파일을 지원합니다.  



## <a name="interfaces"></a>인터페이스  
  
|인터페이스 이름|Description|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement 인터페이스](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|입력 및 출력 매개 변수와 함께 호출할 저장 프로시저 이름을 지정할 수 있도록 합니다.|  
|[ISQLServerConnection 인터페이스](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 대한 JDBC 연결을 나타냅니다.|  
|[SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|[ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결에 관련된 속성의 목록을 나타냅니다.|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|JDBC의 준비된 문 기능에 대한 기본 구현을 나타냅니다.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|JDBC 결과 집합을 나타냅니다.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|JDBC 문 기능의 기본 구현을 나타냅니다.|
| &nbsp; | &nbsp; |


  
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
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 경우와 관련된 속성 목록을 나타냅니다.|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|JNDI(Java Naming and Directory Interface)의 데이터 원본을 구체화하기 위한 개체 팩터리를 나타냅니다.|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|JDBC 드라이버를 나타냅니다. 이 클래스에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하고 JDBC 드라이버에 대한 정보를 얻기 위한 메서드가 포함되어 있습니다.|  
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
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|내부적으로 사용되는 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 개체에 대한 팩터리를 나타냅니다.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|XA 분산 트랜잭션 관리를 위한 XAResource를 나타냅니다.|
| &nbsp; | &nbsp; |



## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../../connect/jdbc/overview-of-the-jdbc-driver.md)

