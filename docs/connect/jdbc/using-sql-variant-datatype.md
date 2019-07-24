---
title: Sql_variant 데이터 형식 사용 | Microsoft Docs
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
ms.openlocfilehash: 662362a692742d206902a0cf23aff63a3ba89df9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916177"
---
# <a name="using-sqlvariant-data-type"></a>Sql_variant 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

버전 6.3.0 JDBC 드라이버는 sql_variant 데이터 형식을 지원 합니다. Sql_variant는이 페이지 뒷부분에서 언급 한 몇 가지 제한 사항이 있는 테이블 반환 매개 변수 및 대량 복사와 같은 기능을 사용 하는 경우에도 지원 됩니다. 모든 데이터 형식을 sql_variant 데이터 형식으로 저장할 수 있는 것은 아닙니다. Sql_variant를 사용 하는 지원 되는 데이터 형식의 목록을 보려면 SQL Server [문서](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)를 확인 하세요.

##  <a name="populating-and-retrieving-a-table"></a>테이블 채우기 및 검색:
하나의 테이블에 sql_variant 열이 있는 테이블이 있다고 가정 합니다.

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

문을 사용 하 여 값을 삽입 하는 샘플 스크립트:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

준비 된 문을 사용 하 여 값을 삽입 합니다.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

전달 되는 데이터의 기본 형식을 알고 있으면 해당 setter를 사용할 수 있습니다. 예를 들어 `preparedStatement.setInt()` 정수 값을 삽입할 때를 사용할 수 있습니다.

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

테이블에서 값을 읽을 수 있도록 각 getter를 사용할 수 있습니다. 예를 들어 `getInt()` 서버 `getString()` 에서 들어오는 값을 알고 있는 경우 또는 메서드를 사용할 수 있습니다.    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>Sql_variant와 함께 저장 프로시저 사용:   
다음과 같은 저장 프로시저를 포함 합니다.     

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
- TVP를 사용 하 여 sql_variant에 저장 된 `datetime` `date` 값으로 / `getSmallDateTime()` `getDateTime()` / `smalldatetime` / 테이블을 채울 때를 / 호출`getDate()` 합니다. ResultSet이 작동 하지 않고 다음 예외를 throw 합니다.
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    해결 방법: `getString()` 대신 `getObject()` 또는를 사용 합니다. 
    
- TVP를 사용 하 여 테이블을 채우고 sql_variant에서 null 값을 보내는 것은 지원 되지 않으며 예외를 throw 합니다.
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
