---
title: Sql_variant 데이터 형식을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c004bc40ed0c85b82612be9069e1a53041c8095c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798584"
---
# <a name="using-sqlvariant-data-type"></a>Sql_variant 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

버전 6.3.0, JDBC 드라이버는 sql_variant 데이터 형식을 지원합니다. Sql_variant은 BulkCopy 테이블 반환 매개 변수 등의 기능을 사용 하 여 몇 가지 제한 사항이이 페이지 뒷부분에서 언급 하는 경우에 지원 됩니다. 일부 데이터 형식 sql_variant 데이터 형식에 저장할 수 있습니다. 목록은 지원 되는 데이터 형식 sql_variant로 SQL Server를 확인 [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)합니다.

##  <a name="populating-and-retrieving-a-table"></a>채우기 및 테이블을 검색 합니다.
가정 하나가 sql_variant 열이 있는 테이블에 있습니다.

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

문을 사용 하 여 값을 삽입 하는 샘플 스크립트:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

준비 된 문이 사용 하 여 삽입 값:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

전달 되는 데이터의 기본 형식을 알고 있는 경우 해당 setter는 사용할 수 있습니다. 예를 들어 `preparedStatement.setInt()` 정수 값을 삽입 하는 경우 사용할 수 있습니다.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

테이블에서 값을 읽기 위한 해당 getter는 사용할 수 있습니다. 예를 들어 `getInt()` 또는 `getString()` 방법을 알고 있는 경우 서버에서 제공 하는 값을 사용할 수 있습니다.    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>Sql_variant를 사용 하 여 저장된 프로시저를 사용 합니다.   
저장된 프로시저와 같은 필요 합니다.     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
출력 매개 변수를 등록 해야 합니다.

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sqlvariant"></a>Sql_variant의 제한 사항:
- 사용 하 여 테이블을 채우기 위한 TVP를 사용 하는 경우는 `datetime` / `smalldatetime` / `date` 값을 sql_variant에 저장 된 호출 `getDateTime()` / `getSmallDateTime()` / `getDate()` 에 ResultSet 작동 하지 않습니다 하 고 다음 예외를 throw 합니다.
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    해결 방법: 사용 `getString()` 또는 `getObject()` 대신 합니다. 
    
- 테이블을 채우기 위한 TVP를 사용 하 고 null 값을 sql_variant에 전송은 지원 되지 않으며 예외가 throw 됩니다.
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
