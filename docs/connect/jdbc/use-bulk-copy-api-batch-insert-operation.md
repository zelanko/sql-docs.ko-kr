---
title: MSSQL JDBC 드라이버에 대 한 일괄 삽입 작업에 대 한 대량 복사 API를 사용 하 여 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 347ce28dc28016f95de2795bd2f5e491dd29e2d8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802634"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>일괄 처리 삽입 작업에 대량 복사 API 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

대량 복사 API를 사용 하 여 Azure Data Warehouse에 대 한 일괄 처리 삽입 작업에 대 한 SQL Server 지원에 대 한 Microsoft JDBC Driver 7.0입니다. 이 기능을 사용 하면 일괄 처리 실행 작업을 삽입 하는 경우 아래에 있는 대량 복사 작업을 수행 하는 드라이버를 사용 하도록 설정 하려면 있습니다. 일반 일괄 처리를 사용 하 여 드라이버는 것 처럼 동일한 데이터를 삽입 하는 동안 성능 향상을 달성 하기 위해 드라이버 목표는 작업을 삽입 합니다. 드라이버에는 일반적인 일괄 삽입 작업 대신 대량 복사 API를 활용 하 여 사용자의 SQL 쿼리를 구문 분석 합니다. 일괄 처리에 대 한 대량 복사 API를 사용할 수 있도록 다양 한 방법으로 삽입 기능 뿐만 아니라 해당 제한 사항 목록과 같습니다. 이 페이지에는 또한 사용량과 성능 향상을 보여 주는 작은 샘플 코드를 포함 합니다.

이 기능은 에서만 PreparedStatement 및 CallableStatement의 적용할 `executeBatch()`  &  `executeLargeBatch()` Api.

## <a name="pre-requisites"></a>필수 구성 요소

일괄 처리 삽입에 대 한 대량 복사 API를 사용 하도록 설정 하려면 두 가지 필수 조건이 있습니다.

* 서버에 Azure Data Warehouse 있어야 합니다.
* 쿼리 삽입 쿼리를 해야 합니다. (쿼리 설명 있을 수 있지만 쿼리에 적용이이 기능에 대 한 INSERT 키워드를 사용 하 여 시작 해야 합니다).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>일괄 처리 삽입에 대 한 대량 복사 API를 사용 하도록 설정

일괄 처리 삽입에 대 한 대량 복사 API를 사용 하는 방법은 세 가지가 있습니다.

### <a name="1-enabling-with-connection-property"></a>1. 연결 속성을 사용 하 여 사용 하도록 설정

추가 **useBulkCopyForBatchInsert = true;** 문자열 연결에이 기능을 활성화 합니다.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. SQLServerConnection 개체에서 setUseBulkCopyForBatchInsert() 메서드를 사용 하 여 사용 하도록 설정

호출 **SQLServerConnection.setUseBulkCopyForBatchInsert(true)** 이 기능을 활성화 합니다.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** 에 대 한 현재 값을 가져옵니다 **useBulkCopyForBatchInsert** 연결 속성입니다.

에 대 한 값 **useBulkCopyForBatchInsert** 초기화 시 각 PreparedStatement 상수 유지 합니다. 후속 호출 **SQLServerConnection.setUseBulkCopyForBatchInsert()** 값 관련 하 여 이미 만들어진된 PreparedStatement 영향을 주지 것입니다.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. SQLServerDataSource 개체에서 setUseBulkCopyForBatchInsert() 메서드를 사용 하 여 사용 하도록 설정

위의 비슷하지만 SQLServerDataSource를 사용 하 여 SQLServerConnection 개체를 만듭니다. 두 방법 모두 동일한 결과를 얻을 수 있습니다.

## <a name="known-limitations"></a>알려진 제한 사항

현재이 기능에 적용 되는 이러한 제한 됩니다.

* 쿼리 매개 변수가 없는 값이 포함 된 삽입 (예를 들어 `INSERT INTO TABLE VALUES (?, 2`)), 지원 되지 않습니다. 와일드 카드 (?)는이 함수에 대해만 지원 되는 매개 변수입니다.
* 삽입 INSERT SELECT 식을 포함 하는 쿼리 (예를 들어 `INSERT INTO TABLE SELECT * FROM TABLE2`)를 사용할 수 없습니다.
* 삽입 쿼리는 다중 값 식 (예를 들어 `INSERT INTO TABLE VALUES (1, 2) (3, 4)`), 지원 되지 않습니다.
* OPTION 절 뒤에, 여러 테이블 조인 또는 다른 쿼리 뒤에 삽입 쿼리는 지원 되지 않습니다.
* 대량 복사 API의 제한으로 인해 `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`를 `DATETIMEOFFSET`를 `SMALLDATETIME`를 `TIME`를 `GEOMETRY`, 및 `GEOGRAPHY` 데이터 형식에는 현재이 지원 되지 않습니다 기능입니다.

비 인해 쿼리가 실패 하는 경우 "SQL server" 오류와 관련 된, 드라이버에 오류 메시지와 대체 (fallback) 일괄 처리 삽입에 대 한 원래 논리로 로그 됩니다.

## <a name="example"></a>예제

일괄 처리 삽입 작업을 Azure DW에 대해는 천 행의 두 (일반 및 대량 복사 API) 시나리오에 대 한 사용 사례를 보여 주는 예제 코드는 다음과 같습니다.

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
