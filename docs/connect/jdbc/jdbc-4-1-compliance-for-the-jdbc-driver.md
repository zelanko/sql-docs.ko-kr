---
title: JDBC 드라이버의 JDBC 4.1 준수 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f087fd40-8451-478e-b465-43112c711515
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 501b5a6ad21fa9b5e6078e27547b612b9fba9fd6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924648"
---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>JDBC 드라이버의 JDBC 4.1 준수
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  SQL Server용 Microsoft JDBC Driver 4.2 이전 버전은 Java Database Connectivity API 4.0 사양을 준수합니다. 4\.2 릴리스 이전 버전에는 이 섹션이 적용되지 않습니다.  
  
 Java Database Connectivity API 4.1 사양은 다음과 같은 API 메서드를 통해 SQL Server용 Microsoft JDBC Driver 4.2에서 지원됩니다.  
  
 **SQLServerConnection 클래스**  
  
|새 메서드|Description|JDBC 드라이버 구현|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|SQL Server에 대한 열린 연결을 종료합니다.|java.sql.Connection 인터페이스에 설명된 대로 구현됩니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)을 참조하세요.|  
|void setSchema(String schema)|현재 연결에 대한 스키마를 설정합니다.|SQL Server는 현재 세션에 대한 스키마 설정을 지원하지 않습니다. 이 메서드가 호출될 경우 드라이버는 자동으로 경고 메시지를 기록합니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)을 참조하세요.|  
|String getSchema()|현재 연결에 대한 스키마 이름을 반환합니다.|SQL Server에서 현재 연결에 대한 스키마 설정을 지원하지 않으므로 드라이버는 사용자의 기본 스키마를 대신 반환합니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)을 참조하세요.|  
  
 **SQLServerDatabaseMetaData 클래스**  
  
|새 메서드|Description|JDBC 드라이버 구현|  
|----------------|-----------------|--------------------------------|  
|boolean generatedKeyAlwaysReturned()|드라이버에서 생성된 키 검색을 지원하므로 true를 반환합니다.|java.sql에서 설명된 대로 구현됩니다. DatabaseMetaData 인터페이스입니다. 자세한 내용은 [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html)를 참조하세요.|  
|ResultSet getPseudoColumns(String catalog, String schemaPattern,String tableNamePattern,String columnNamePattern)|의사/숨겨진 열에 대한 설명을 검색합니다.|SQL Server에는 의사 열에 대한 공식 개념이 없으므로 빈 결과 집합을 반환합니다. 자세한 내용은 [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html)를 참조하세요.|  
  
 **SQLServerStatement 클래스**  
  
|새 메서드|Description|JDBC 드라이버 구현|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|모든 종속 결과 집합을 닫으면 이 문이 닫히도록 지정합니다.|java.sql.Statement 인터페이스에 설명된 대로 구현됩니다. 자세한 내용은 [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)를 참조하세요.|  
|boolean isCloseOnCompletion()|모든 종속 결과 집합을 닫으면 이 문도 닫히는지 여부를 나타내는 값을 반환합니다.|java.sql.Statement 인터페이스에 설명된 대로 구현됩니다. 자세한 내용은 [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)를 참조하세요.|  
  
 Java Database Connectivity API 4.1 사양은 다음과 같은 기능을 통해 SQL Server용 Microsoft JDBC Driver 4.2에서 지원됩니다.  
  
|새 기능|Description|  
|-----------------|-----------------|  
|새 이스케이프 함수<br /><br /> 제한된 행 반환 이스케이프|부분적으로 지원됨<br /><br /> 이스케이프 구문: LIMIT \<rows> [OFFSET <row_offset>](using-sql-escape-sequences.md).|  
  
 Java Database Connectivity API 4.1 사양은 다음과 같은 데이터 형식 매핑을 통해 SQL Server용 Microsoft JDBC Driver 4.2에서 지원됩니다.  
  
|데이터 형식 매핑|Description|  
|------------------------|-----------------|  
|이제 새로운 데이터 형식 매핑이 PreparedStatement.setObject() 및 PreparedStatement.setNull() 메서드에서 지원됩니다.|1. 새로운 Java와 JDBC 간 형식 매핑<br /><br /> (a) java.math.BigInteger와 JDBC BIGINT<br /><br /> (b) java.util.Date 및 java.util.Calendar와 JDBC TIMESTAMP<br /><br /> 2. 새로운 데이터 형식 변환:<br /><br /> (a) java.math.BigInteger를 CHAR, VARCHAR, LONGVARCHAR 및 BIGINT로 변환<br /><br /> (b) java.util.Date 및 java.util.Calendar를 CHAR, VARCHAR, LONGVARCHAR, DATE, TIME 및 TIMESTAMP로 변환<br /><br /> 자세한 내용은 JDBC 4.1 사양을 참조하세요.|  
  
  
