---
title: MSSQL JDBC 드라이버에 대한 일괄 처리 삽입 작업에 대량 복사 API 사용 | Microsoft Docs
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
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027102"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>일괄 처리 삽입 작업에 대량 복사 API 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server용 Microsoft JDBC Driver 7.0는 Azure Data Warehouse에 대한 일괄 처리 삽입 작업을 위해 대량 복사 API를 사용할 수 있도록 지원합니다. 사용자는 이 기능으로 일괄 처리 삽입 작업을 실행할 때 아래에서 대량 복사 작업을 수행할 수 있습니다. 드라이버의 목표는 드라이버에서 정규 일괄 처리 삽입 작업으로 할 때처럼 동일한 데이터를 삽입하면서 성능을 개선하는 데 있습니다. 드라이버는 일반적 일괄 처리 삽입 작업이 아닌 대량 복사 API를 활용하여 사용자의 SQL 쿼리를 구문 분석합니다. 아래에서는 일괄 처리 삽입 기능에 대량 복사 API를 사용 설정하는 방법과 관련 제한 사항의 목록을 소개합니다. 또한 이 페이지에는 사용량과 성능의 증가치를 보여주는 작은 샘플 코드도 포함되어 있습니다.

이 기능은 PreparedStatement와 CallableStatement의 `executeBatch()` & `executeLargeBatch()` API에만 사용할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

일괄 처리 삽입에 대량 복사 API를 사용하려면 두 가지 요소가 꼭 필요합니다.

* 먼저 서버는 Azure Data Warehouse여야 합니다.
* 쿼리는 삽입 쿼리여야 합니다. 쿼리에는 주석이 포함될 수 있지만, 이 기능을 적용하려면 쿼리가 INSERT 키워드로 시작해야 합니다.

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>일괄 처리 삽입 작업에 대량 복사 API 사용

일괄 처리 삽입에 대량 복사 API를 사용하는 방법으로는 세 가지가 있습니다.

### <a name="1-enabling-with-connection-property"></a>1. 연결 속성 사용 설정

**useBulkCopyForBatchInsert=true;** 를 연결 문자열로 추가하면 이 기능이 사용 설정됩니다.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. SQLServerConnection 개체의 setUseBulkCopyForBatchInsert() 메서드 사용 설정

**SQLServerConnection.setUseBulkCopyForBatchInsert(true)** 를 호출하면 이 기능이 사용 설정됩니다.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** 는 **useBulkCopyForBatchInsert** 연결 속성의 현재 값을 검색합니다.

**useBulkCopyForBatchInsert**의 값은 초기화 시 각각의 PreparedStatement에 대해 상수로 유지됩니다. **SQLServerConnection.setUseBulkCopyForBatchInsert()** 에 대한 후속 호출은 이미 생성된 PreparedStatement의 값에 영향을 미치지 않습니다.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. SQLServerDataSource 개체의 setUseBulkCopyForBatchInsert() 메서드 사용 설정

위와 비슷하지만 SQLServerDataSource를 사용하여 SQLServerConnection 개체를 만듭니다. 두 방법 모두 동일한 결과를 얻을 수 있습니다.

## <a name="known-limitations"></a>알려진 제한 사항

현재는 다음의 제한 사항이 이 기능에 적용됩니다.

* 매개 변수화되지 않은 값이 포함된 삽입 쿼리(예: `INSERT INTO TABLE VALUES (?, 2`))는 지원되지 않습니다. 와일드카드(?)만 이 기능에 대해 지원되는 매개 변수입니다.
* INSERT-SELECT 식이 포함된 삽입 쿼리(예: `INSERT INTO TABLE SELECT * FROM TABLE2`)는 지원되지 않습니다.
* 여러 VALUE 식이 포함된 삽입 쿼리(예: `INSERT INTO TABLE VALUES (1, 2) (3, 4)`)는 지원되지 않습니다.
* OPTION 절이 뒤에 오는 삽입 쿼리(여러 테이블과 조인됨)나 다른 쿼리가 뒤에 오는 삽입 쿼리는 지원되지 않습니다.
* 대량 복사 API의 제한 사항으로 인해 `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY`, `GEOGRAPHY` 데이터 형식은 현재 이 기능에 대해 지원되지 않습니다.

비"SQL Server" 관련 오류로 인해 쿼리가 실패하는 경우 드라이버는 오류 메시지를 로그하고 일괄 처리 삽입 작업의 원래 논리로 대체됩니다.

## <a name="example"></a>예제

아래에서는 1,000개 행의 Azure DW에 대한 일괄 처리 삽입 작업의 사용 사례를 일반 및 대량 복사 API 시나리오 모두에 대해 소개합니다.

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
