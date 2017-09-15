---
title: "Java EE 지원 이해 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b878069cb0ddf04d4c8c743795f876b00fef23dc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-java-ee-support"></a>Java EE 지원 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  다음 섹션에서는 문서 방법을 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] Java Platform, Enterprise Edition (Java EE) 및 JDBC 3.0 선택적 API 기능에 대 한 지원을 제공 합니다. 도움말 시스템에서 제공하는 원본 코드 예제는 이러한 기능을 살펴보는 데 유용합니다.  
  
 먼저 Java 환경(JDK, JRE)에 javax.sql 패키지가 포함되어 있는지 확인하십시오. 이 패키지는 선택적 API를 사용하는 JDBC 응용 프로그램에 필요합니다. JDK 1.5 이상 버전에는 이미 이 패키지가 포함되어 있으므로 별도로 설치할 필요가 없습니다.  
  
## <a name="driver-name"></a>드라이버 이름  
 드라이버 클래스 이름은 **com.microsoft.sqlserver.jdbc.SQLServerDriver**합니다. JDBC 드라이버 4.0, 4.1, 4.2 및 6.0에 대 한 드라이버는 sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar 또는 sqljdbc42.jar 파일에 포함 됩니다. JDBC 드라이버 6.2에 대 한 드라이버 mssql-jdbc-6.2.1.jre7.jar 또는 mssql-jdbc-6.2.1.jre8.jar에 포함 되어 있습니다.
  
 클래스 이름은 JDBC DriverManager 클래스를 사용 하 여 드라이버를 로드할 때마다 사용 됩니다. 또한 드라이버 구성에 드라이버 클래스 이름을 지정해야 하는 경우에도 항상 사용됩니다. 예를 들어 Java EE 응용 프로그램 서버에서 데이터 원본을 구성하려면 드라이버 클래스 이름을 입력해야 할 수도 있습니다.  
  
## <a name="data-sources"></a>데이터 원본  
 JDBC 드라이버는 Java EE/JDBC 3.0 데이터 원본을 지원합니다. JDBC 드라이버 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스에 의해 구현 됩니다 **com.microsoft.sqlserver.jdbc.SQLServerXADataSource**합니다.  
  
### <a name="datasource-names"></a>데이터 원본 이름  
 데이터 원본을 사용하여 데이터베이스 연결을 만들 수 있습니다. 다음 표에서는 JDBC 드라이버에 사용할 수 있는 데이터 원본에 대해 설명합니다.  
  
|데이터 원본 유형|클래스 이름 및 설명|  
|---------------|--------------------------|  
|DataSource|com.microsoft.sqlserver.jdbc.SQLServerDataSource <br/> <br/> 풀링되지 않는 데이터 원본입니다.|  
|ConnectionPoolDataSource|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource <br/> <br/> JAVA EE 응용 프로그램 서버 연결 풀을 구성하기 위한 데이터 원본입니다. 일반적으로 응용 프로그램이 JAVA EE 응용 프로그램 서버 내에서 실행되는 경우에 사용됩니다.|  
|XADataSource|com.microsoft.sqlserver.jdbc.SQLServerXADataSource <br/> <br/> JAVA EE XA 데이터 원본을 구성하기 위한 데이터 원본입니다. 일반적으로 응용 프로그램이 JAVA EE 응용 프로그램 서버와 XA 트랜잭션 관리자 내에서 실행되는 경우에 사용됩니다.|  
  
### <a name="data-source-properties"></a>데이터 원본 속성  
 모든 데이터 원본은 기본 드라이버의 속성 집합과 연관된 속성을 설정하고 가져오는 기능을 지원합니다.  
  
 예:  
  
 `setServerName("localhost");`  
  
 `setDatabaseName("AdventureWorks");`  
  
 다음은 데이터 원본을 사용하여 응용 프로그램이 연결되는 방법을 보여 줍니다.  
  
```  
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 데이터 원본 속성에 대 한 자세한 내용은 참조 [데이터 원본 속성을 설정](../../connect/jdbc/setting-the-data-source-properties.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

