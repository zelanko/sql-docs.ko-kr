---
description: useFmtOnly를 통해 ParameterMetaData 검색
title: useFmtOnly를 통해 ParameterMetaData 검색 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: ad8f30b236ca9d4fe8a134db3e1726aaeb17a2d3
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727464"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>useFmtOnly를 통해 ParameterMetaData 검색
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft JDBC Driver for SQL Server에는 서버에서 매개 변수 메타데이터를 쿼리하는 다른 방법인 **useFmtOnly**가 포함되어 있습니다. 이 기능은 드라이버 버전 7.4에 처음 도입되었으며 `sp_describe_undeclared_parameters`의 알려진 문제에 대한 해결 방법으로 필요합니다.
  
  드라이버는 기본적으로 저장 프로시저 `sp_describe_undeclared_parameters`를 사용하여 매개 변수 메타데이터를 쿼리합니다. 드라이버가 대부분의 경우 매개 변수 메타데이터 검색에 권장되는 방법이기 때문입니다. 그러나 현재 다음과 같은 사용 사례에서는 저장 프로시저 실행이 실패합니다.
  
-   Always Encrypted 열
  
-   임시 테이블과 테이블 변수에 대해
  
-   보기 
  
  이러한 사용 사례를 위해 제안된 솔루션은 사용자의 SQL 쿼리를 매개 변수 및 테이블 대상에 대해 구문 분석한 다음 `FMTONLY`를 사용하도록 설정하여 `SELECT` 쿼리를 실행하는 것입니다. 다음 코드 조각은 이 기능을 시각화하는 데 도움이 됩니다.
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>기능 설정/해제 
 **useFmtOnly** 기능은 기본적으로 해제되어 있습니다. 사용자는 `useFmtOnly=true`를 지정하여 연결 문자열을 통해 이 기능을 사용하도록 설정할 수 있습니다. 예: `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`
 
 또는 `SQLServerDataSource`를 통해 이 기능을 사용할 수 있습니다.
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 이 기능은 문 수준에서도 사용할 수 있습니다. 사용자는 `PreparedStatement.setUseFmtOnly(boolean)`를 통해 기능을 설정/해제할 수 있습니다.
> [!NOTE]  
>  드라이버는 연결 수준 속성보다 문 수준 속성을 우선적으로 처리합니다.

## <a name="using-the-feature"></a>기능 사용
  이 기능이 사용하도록 설정되면 드라이버는 내부적으로 매개 변수 메타데이터를 쿼리할 때 `sp_describe_undeclared_parameters` 대신 새 기능을 사용하여 시작합니다. 최종 사용자에게 필요한 추가 작업은 없습니다.
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  이 기능은 `SELECT/INSERT/UPDATE/DELETE` 쿼리만 지원합니다. 쿼리는 지원되는 4개 키워드 중 하나 또는 [공통 테이블 식](../../t-sql/queries/with-common-table-expression-transact-sql.md?view=sql-server-2017)으로 시작하고 그 뒤에 지원되는 쿼리 중 하나가 이어져야 합니다. 공통 테이블 식 내 매개 변수는 지원되지 않습니다.

## <a name="known-issues"></a>알려진 문제
  이 기능에는 현재 SQL 구문 분석 논리의 결함으로 인해 발생하는 몇 가지 문제가 있습니다. 이러한 문제는 이 기능에 대한 향후 업데이트에서 해결될 수 있으며, 아래에 해결 방법 제안과 함께 설명되어 있습니다.
  
A. '전방 선언' 별칭 사용
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. 테이블에 공유 열 이름이 있을 때 모호한 열 이름
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. 매개 변수를 사용하여 하위 쿼리에서 선택(SELECT)
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. SET 절의 하위 쿼리
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>참고 항목  
 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)  
  
