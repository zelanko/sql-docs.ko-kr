---
title: MSSQL JDBC Driver에 대 한 일괄 삽입 작업에 대량 복사 API 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 028caf1bf69c7e361ea7e4445c192c1fc1adf437
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004140"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>일괄 처리 삽입 작업에 대량 복사 API 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 용 Microsoft JDBC Driver 7.0은 Azure Data Warehouse에 대 한 batch 삽입 작업용 대량 복사 API 사용을 지원 합니다. 이 기능을 사용 하면 사용자가 일괄 처리 삽입 작업을 실행할 때 아래에서 대량 복사 작업을 수행할 수 있습니다. 드라이버는 일반 일괄 삽입 작업을 사용 하 여 드라이버와 동일한 데이터를 삽입 하는 동안 성능을 향상 시키는 것을 목표로 합니다. 이 드라이버는 일반적인 일괄 삽입 작업 대신 대량 복사 API를 활용 하 여 사용자의 SQL 쿼리를 구문 분석 합니다. 다음은 batch 삽입 기능에 대량 복사 API를 사용 하도록 설정 하는 다양 한 방법 및 제한 사항 목록입니다. 또한이 페이지에는 사용량 및 성능 증가를 보여 주는 작은 샘플 코드도 포함 되어 있습니다.

이 기능은 java.sql.preparedstatement 및 callablestatement의 `executeBatch()`  &  `executeLargeBatch()` api에만 적용 됩니다.

## <a name="pre-requisites"></a>필수 구성 요소

일괄 삽입을 위해 대량 복사 API를 사용 하려면 두 가지 필수 구성 요소가 있습니다.

* 서버는 Azure 데이터 웨어하우스 여야 합니다.
* 쿼리는 insert 쿼리 여야 합니다. 쿼리에는 주석이 포함 될 수 있지만 쿼리는이 기능을 적용 하려면 INSERT 키워드를 사용 하 여 시작 해야 합니다.

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>일괄 삽입을 위한 대량 복사 API 사용

일괄 삽입을 위해 대량 복사 API를 사용 하도록 설정 하는 방법에는 세 가지가 있습니다.

### <a name="1-enabling-with-connection-property"></a>1. 연결 속성을 사용 하도록 설정

연결 문자열에 **Use대량 Copyforbatchinsert = true** 를 추가 하면이 기능을 사용할 수 있습니다.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. SQLServerConnection 개체에서 Setuse대량 Copyforbatchinsert () 메서드 사용

**SQLServerConnection** 를 호출 하면이 기능을 사용할 수 있습니다.

SQLServerConnection는 **Use대량** copyforbatchinsert 연결 속성에 대 한 현재 값을 검색 **합니다.**

**Use대량 Copyforbatchinsert** 의 값은 초기화 시 각 java.sql.preparedstatement 일정 하 게 유지 됩니다. **SQLServerConnection** 에 대 한 후속 호출은 해당 값과 관련 하 여 이미 생성 된 java.sql.preparedstatement에 영향을 주지 않습니다.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. SQLServerDataSource 개체에서 Setuse대량 Copyforbatchinsert () 메서드 사용

위와 비슷하며 SQLServerDataSource를 사용 하 여 SQLServerConnection 개체를 만듭니다. 두 방법 모두 동일한 결과를 얻을 수 있습니다.

## <a name="known-limitations"></a>알려진 제한 사항

현재이 기능에 적용 되는 제한 사항이 있습니다.

* 매개 변수가 없는 값 (예: `INSERT INTO TABLE VALUES (?, 2`)을 포함 하는 Insert 쿼리는 지원 되지 않습니다. 와일드 카드 (?)는이 함수에 대해 유일 하 게 지원 되는 매개 변수입니다.
* Insert SELECT 식이 포함 된 insert 쿼리 (예: `INSERT INTO TABLE SELECT * FROM TABLE2`)는 지원 되지 않습니다.
* 여러 값 식이 포함 된 Insert 쿼리 (예: `INSERT INTO TABLE VALUES (1, 2) (3, 4)`)는 지원 되지 않습니다.
* OPTION 절이 뒤에 오는 Insert 쿼리는 여러 테이블과 조인 되거나 그 다음에 다른 쿼리를 사용 하 여 지원 되지 않습니다.
* 대량 복사 API `MONEY` `SMALLMONEY` `DATE` 의제한`GEOGRAPHY` 사항으로 인해,,,,,,, 및 데이터 형식은 현재이를 지원 하지 않습니다. `DATETIME` `DATETIMEOFFSET` `SMALLDATETIME` `TIME` `GEOMETRY` 기능과.

"SQL server" 관련 오류로 인해 쿼리가 실패 하는 경우 드라이버는 오류 메시지를 기록 하 고 batch insert의 원래 논리에 대체 합니다.

## <a name="example"></a>예제

다음은 (일반 vs 대량 복사 API) 시나리오 모두에서 1000 개 행의 Azure DW에 대해 일괄 삽입 작업에 대 한 사용 사례를 보여 주는 예제 코드입니다.

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

결과:

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
