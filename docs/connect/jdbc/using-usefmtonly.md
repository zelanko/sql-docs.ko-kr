---
title: UseFmtOnly를 통해 ParameterMetaData 검색 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
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
ms.openlocfilehash: 29ee2c5c22baf77b6994a440f1d9d442ba2b812a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894095"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>UseFmtOnly를 통해 ParameterMetaData 검색
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  SQL Server 용 Microsoft JDBC Driver에는 **useFmtOnly**서버에서 매개 변수 메타 데이터를 쿼리 하는 다른 방법이 포함 되어 있습니다. 이 기능은 드라이버 버전 7.4에 처음 도입 되었으며의 `sp_describe_undeclared_parameters`알려진 문제에 대 한 해결 방법으로 필요 합니다.
  
  이 드라이버는 주로 저장 프로시저 `sp_describe_undeclared_parameters` 를 사용 하 여 매개 변수 메타 데이터를 쿼리 합니다 .이는 대부분의 경우 매개 변수 메타 데이터 검색에 권장 되는 방법입니다. 그러나 저장 프로시저를 실행 하는 작업은 현재 다음과 같은 사용 사례에서 실패 합니다.
  
-   Always Encrypted 열에 대해
  
-   임시 테이블과 테이블 변수에 대해
  
-   보기에 대해 
  
  이러한 사용 사례에 대 한 제안 된 솔루션은 사용자의 SQL 쿼리를 매개 변수 및 테이블 대상에 대해 구문 분석 `SELECT` 한 다음 `FMTONLY` enabled를 사용 하 여 쿼리를 실행 하는 것입니다. 다음 코드 조각은 기능을 시각화 하는 데 도움이 됩니다.
  
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
 기능 **useFmtOnly** 는 기본적으로 해제 되어 있습니다. 사용자는를 지정 `useFmtOnly=true`하 여 연결 문자열을 통해이 기능을 사용 하도록 설정할 수 있습니다. 예를 들어 `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`을 참조하십시오.
 
 또는를 통해 `SQLServerDataSource`이 기능을 사용할 수 있습니다.
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
 
 이 기능은 문 수준 에서도 사용할 수 있습니다. 사용자는를 통해 `PreparedStatement.setUseFmtOnly(boolean)`기능을 설정/해제할 수 있습니다.
> [!NOTE]  
>  드라이버는 연결 수준 속성에 대해 문 수준 속성의 우선 순위를 지정 합니다.

## <a name="using-the-feature"></a>기능 사용
  사용 하도록 설정 되 면 드라이버는 내부적으로 매개 변수 메타 데이터를 `sp_describe_undeclared_parameters` 쿼리할 때 대신 새 기능을 사용 하 여 시작 합니다. 최종 사용자에 게 필요한 추가 작업은 없습니다.
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
>  이 기능은 쿼리만 지원 `SELECT/INSERT/UPDATE/DELETE` 합니다. 쿼리는 지원 되는 키워드 4 개 또는 [공통 테이블 식](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017) 중 하나로 시작 하 고 그 다음에 지원 되는 쿼리 중 하나를 사용 하 여 시작 해야 합니다. 공통 테이블 식 내의 매개 변수는 지원 되지 않습니다.

## <a name="known-issues"></a>알려진 문제
  이 기능에는 현재 SQL 구문 분석 논리의 결함으로 인해 발생하는 몇 가지 문제가 있습니다. 이러한 문제는이 기능에 대 한 향후 업데이트에서 해결 될 수 있으며, 아래에는 해결 방법 제안과 함께 설명 되어 있습니다.
  
1\. ' 전방 선언 ' 별칭 사용
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

2\. 테이블에 공유 열 이름이 있는 경우의 열 이름이 모호 합니다.
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. 매개 변수가 있는 하위 쿼리에서 선택
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

## <a name="see-also"></a>관련 항목:  
 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
