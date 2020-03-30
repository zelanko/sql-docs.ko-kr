---
title: sql_variant 데이터 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025837"
---
# <a name="using-sql_variant-data-type"></a>Sql_variant 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

JDBC 드라이버는 버전 6.3.0부터 sql_variant 데이터 형식을 지원합니다. sql_variant는 테이블 반환 매개 변수 및 BulkCopy와 같은 기능을 사용하는 경우에도 지원됩니다(관련 제한 사항은 이 페이지의 뒷부분에 설명). 일부 데이터 형식은 sql_variant 데이터 형식에 저장할 수 없습니다. sql_variant 지원 데이터 형식 목록은 SQL Server [설명서](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)를 참조하세요.

##  <a name="populating-and-retrieving-a-table"></a>테이블 채우기 및 검색:
다음과 같은 sql_variant 열이 포함된 테이블이 있다고 가정합니다.

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

문을 사용하여 값을 삽입할 샘플 스크립트:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

준비된 문을 사용하여 값을 삽입합니다.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

전달되는 데이터의 기본 형식을 알고 있으면 각각의 setter를 사용할 수 있습니다. 예를 들어 정수 값을 삽입할 때는 `preparedStatement.setInt()`를 사용할 수 있습니다.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

테이블에서 값을 읽을 수 있도록 각각의 getter를 사용할 수 있습니다. 예를 들어 서버에서 오는 값을 알고 있는 경우 `getInt()` 또는 `getString()` 메서드를 사용할 수 있습니다.    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>sql_variant로 저장 프로시저 사용:   
다음과 같은 저장 프로시저가 있습니다.     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
출력 매개 변수 등록이 필요합니다.

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>sql_variant 제한 사항:
- TVP를 사용하여 sql_variant에 저장된 `datetime`/`smalldatetime`/`date` 값으로 테이블을 채울 때는 ResultSet의 `getDateTime()`/`getSmallDateTime()`/`getDate()` 호출이 작동하지 않고 다음 예외가 발생합니다.
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    해결 방법: `getString()` 또는 `getObject()`를 대신 사용합니다. 
    
- TVP를 사용하여 테이블을 채우고 sql_variant에서 null 값을 보내는 방법은 지원되지 않으며 예외가 발생합니다.
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
