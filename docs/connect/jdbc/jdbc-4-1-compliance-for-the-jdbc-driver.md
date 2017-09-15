---
title: "JDBC 4.1 준수 JDBC 드라이버에 대 한 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f087fd40-8451-478e-b465-43112c711515
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8221755d220caec5588c8ed1343e360799b82694
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>JDBC 드라이버의 JDBC 4.1 준수
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  SQL Server용 Microsoft JDBC Driver 4.2 이전 버전은 Java Database Connectivity API 4.0 사양을 준수합니다. 4.2 릴리스 이전 버전에는 이 섹션이 적용되지 않습니다.  
  
 Java Database Connectivity API 4.1 사양은 다음과 같은 API 메서드를 통해 SQL Server용 Microsoft JDBC Driver 4.2에서 지원됩니다.  
  
 **SQLServerConnection 클래스**  
  
|새 메서드|Description|JDBC 드라이버 구현|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|SQL Server에 대한 열린 연결을 종료합니다.|java.sql.Connection 인터페이스에 설명된 대로 구현됩니다. 자세한 내용은 참조 [java.sql.Connection](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)합니다.|  
|void setSchema(String schema)|현재 연결에 대한 스키마를 설정합니다.|SQL Server는 현재 세션에 대한 스키마 설정을 지원하지 않습니다. 이 메서드가 호출될 경우 드라이버는 자동으로 경고 메시지를 기록합니다. 자세한 내용은 참조 [java.sql.Connection](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)합니다.|  
|String getSchema()|현재 연결에 대한 스키마 이름을 반환합니다.|SQL Server에서 현재 연결에 대한 스키마 설정을 지원하지 않으므로 드라이버는 사용자의 기본 스키마를 대신 반환합니다. 자세한 내용은 참조 [java.sql.Connection](http://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)합니다.|  
  
 **SQLServerDatabaseMetaData 클래스**  
  
|새 메서드|Description|JDBC 드라이버 구현|  
|----------------|-----------------|--------------------------------|  
|boolean generatedKeyAlwaysReturned()|드라이버에서 생성된 키 검색을 지원하므로 true를 반환합니다.|java.sql에서 설명된 대로 구현됩니다. DatabaseMetaData 인터페이스입니다. 자세한 내용은 참조 하십시오. [java.sql.DatabaseMetaData](http://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html)합니다.|  
|ResultSet getPseudoColumns(String catalog, String schemaPattern,String tableNamePattern,String columnNamePattern)|의사/숨겨진 열에 대한 설명을 검색합니다.|SQL Server에는 의사 열에 대한 공식 개념이 없으므로 빈 결과 집합을 반환합니다. 자세한 내용은 참조 하십시오. [java.sql.DatabaseMetaData](http://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html)합니다.|  
  
 **SQLServerStatement 클래스**  
  
|새 메서드|Description|JDBC 드라이버 구현|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|모든 종속 결과 집합을 닫으면 이 문이 닫히도록 지정합니다.|java.sql.Statement 인터페이스에 설명된 대로 구현됩니다. 자세한 내용은 참조 하십시오. [java.sql.Statement](http://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)합니다.|  
|boolean isCloseOnCompletion()|모든 종속 결과 집합을 닫으면 이 문도 닫히는지 여부를 나타내는 값을 반환합니다.|java.sql.Statement 인터페이스에 설명된 대로 구현됩니다. 자세한 내용은 참조 하십시오. [java.sql.Statement](http://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)합니다.|  
  
 Java Database Connectivity API 4.1 사양은 다음과 같은 기능을 통해 SQL Server용 Microsoft JDBC Driver 4.2에서 지원됩니다.  
  
|새 기능|Description|  
|-----------------|-----------------|  
|새 이스케이프 함수<br /><br /> 제한된 행 반환 이스케이프|부분적으로 지원됨<br /><br /> 이스케이프 구문을: 제한 \<행 > [< row_offset > 오프셋]<br /><br /> 이스케이프 구문은 두 가지 요소로 구성되어 있습니다. 필수 요소인 ‘rows’는 반환할 행 수를 지정하고 선택적 요소인 'row_offset'은 행 반환을 시작하기 전에 건너뛸 행 수를 지정합니다.<br /><br /> 드라이버는 LIMIT 대신 ‘TOP’를 사용하도록 쿼리를 변환하여 필수 요소만 지원합니다. SQL Server는 'LIMIT'를 지원하지 않습니다.<br /><br /> SQL Server에는 선택적 요소인 'row_offset'을 지원하는 기본 제공 구문이 없으므로 이 요소를 사용할 경우 드라이버에서 예외가 throw됩니다.<br /><br /> 자세한 내용은 참조 [SQL 이스케이프 시퀀스를 사용 하 여](https://msdn.microsoft.com/en-us/library/ms378045.aspx)합니다.|  
  
 Java Database Connectivity API 4.1 사양은 다음과 같은 데이터 형식 매핑을 통해 SQL Server용 Microsoft JDBC Driver 4.2에서 지원됩니다.  
  
|데이터 형식 매핑|Description|  
|------------------------|-----------------|  
|이제 새로운 데이터 형식 매핑이 PreparedStatement.setObject() 및 PreparedStatement.setNull() 메서드에서 지원됩니다.|1. 새로운 Java와 JDBC 간 형식 매핑<br /><br /> (a) java.math.BigInteger와 JDBC BIGINT<br /><br /> (b) java.util.Date 및 java.util.Calendar와 JDBC TIMESTAMP<br /><br /> 2. 새로운 데이터 형식 변환:<br /><br /> (a) java.math.BigInteger를 CHAR, VARCHAR, LONGVARCHAR 및 BIGINT로 변환<br /><br /> (b) java.util.Date 및 java.util.Calendar를 CHAR, VARCHAR, LONGVARCHAR, DATE, TIME 및 TIMESTAMP로 변환<br /><br /> 자세한 내용은 JDBC 4.1 사양을 참조하세요.|  
  
  
