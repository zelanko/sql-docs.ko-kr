---
description: 그래프 에지 제약 조건
title: 그래프 에지 제약 조건 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current'
ms.openlocfilehash: 6f1075c6128ae040b3f2b0cb80c167d77aca89e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419027"
---
# <a name="edge-constraints"></a>에지 제약 조건

[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]

에지 제약 조건은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 그래프 데이터베이스의 에지 테이블에 데이터 무결성 및 특정 의미 체계를 적용하는 데 사용할 수 있습니다.

## <a name="edge-constraints"></a><a name="Connection"></a> 에지 제약 조건

그래프 기능의 첫 번째 릴리스에서 에지 테이블은 에지 엔드포인트에 대해 어떤 작업도 적용하지 않습니다. 즉, 그래프 데이터베이스의 에지는 해당 형식에 관계없이 노드를 다른 노드에 연결할 수 있습니다.

이 릴리스에서는 에지 테이블에 제약 조건을 추가할 수 있도록 하는 에지 제약 조건을 도입하여 특정 의미 체계를 적용하고 데이터 무결성을 유지할 수 있도록 합니다. 에지 제약 조건을 사용하여 새 에지를 에지 테이블에 추가하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 에지가 연결하려고 하는 노드가 적절한 노드 테이블에 있도록 합니다. 또한 노드가 에지에서 여전히 참조되면 노드를 삭제할 수 없도록 합니다.

### <a name="edge-constraint-clauses"></a>에지 제약 조건 절

각 에지 제약 조건은 하나 이상의 에지 제약 조건 절로 이루어집니다. 에지 제약 조건 절은 지정된 에지가 연결될 수 있는 FROM 및 TO 노드 쌍입니다.

그래프에 `Product` 및 `Customer` 노드가 있으며 `Bought` 에지를 사용하여 이러한 노드를 연결한다고 가정합니다. 에지 제약 조건 절은 FROM 및 TO 노드 쌍과 에지 방향을 지정합니다. 이 경우 에지 제약 조건 절은 `Customer` TO `Product`가 됩니다. 즉, `Customer`에서 `Product`로 이동하는 `Bought`를 삽입할 수 있습니다. `Product`에서 `Customer`로 이동하는 에지를 삽입하려고 하면 실패합니다.

- 에지 제약 조건 절은 에지 제약 조건이 적용되는 FROM 및 TO 노드 테이블 쌍을 포함합니다.
- 분리로 적용되는 에지 제약 조건당 여러 에지 제약 조건 절을 지정할 수 있습니다.
- 다중 에지 제약 조건이 단일 에지 테이블에 생성되면 에지는 허용되기 위해 모든 제약 조건을 만족해야 합니다.

### <a name="indexes-on-edge-constraints"></a>에지 제약 조건의 인덱스

에지 제약 조건을 만들어도 에지 테이블의 `$from_id` 및 `$to_id` 열에 해당 인덱스가 자동으로 생성되지 않습니다. `$from_id`에서 인덱스를 수동으로 만들 경우 지점 조회 쿼리 또는 OLTP 워크로드가 있으면 `$to_id` 쌍이 권장됩니다.

### <a name="on-delete-referential-actions-on-edge-constraints"></a>에지 제약 조건에 대한 ON DELETE 참조 동작
에지 제약 조건에 연계 동작을 사용하면 사용자는 지정된 에지가 연결되는 노드를 삭제할 때 데이터베이스 엔진이 수행하는 동작을 정의할 수 있습니다. 다음 참조 동작을 정의할 수 있습니다.  
*NO ACTION*   
연결된 에지가 있는 노드를 삭제하려고 하면 데이터베이스 엔진에서 오류를 발생시킵니다.  

*CASCADE*   
데이터베이스에서 노드를 삭제하면 연결하는 에지가 삭제됩니다.  

## <a name="working-with-edge-constraints"></a>에지 제약 조건 작업

[!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 에지 제약 조건을 정의할 수 있습니다. 에지 제약 조건은 그래프 에지 테이블에서만 정의할 수 있습니다. 에지 제약 조건을 만들거나, 삭제하거나, 수정하려면 테이블에 대한 **ALTER** 권한이 있어야합니다.

### <a name="create-edge-constraints"></a>에지 제약 조건 만들기

다음 예제에서는 기존 또는 새 테이블에 에지 제약 조건을 만드는 방법을 보여 줍니다.

#### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>새 에지 테이블에 에지 제약 조건을 만들려면

다음 예제에서는 **bought** 에지 테이블에 에지 제약 조건을 만듭니다.

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE NO ACTION
   )
   AS EDGE;
   ```

#### <a name="defining-referential-actions-on-a-new-edge-table"></a>새 에지 테이블에 대한 참조 동작 정의 

다음 예제에서는 **bought** 에지 테이블에 대해 에지 제약 조건을 만들고 ON DELETE CASCADE 참조 동작을 정의합니다. 

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE CASCADE
   )
   AS EDGE;
   ```

#### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>기존 에지 테이블에 에지 제약 조건을 추가하려면

이 예제에서는 ALTER TABLE을 사용하여 **bought** 에지 테이블에 에지 제약 조건을 추가합니다.

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY,
      , CustomerName VARCHAR(100)
   )
   AS NODE;
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product);
```  

#### <a name="create-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>추가 에지 제약 조건 절을 사용하여 기존 에지 테이블에 새 에지 제약 조건 만들기

다음 예제에서는 `ALTER TABLE` 명령을 사용하여 **bought** 에지 테이블에 추가 에지 제약 조건 절을 통해 새 에지 제약 조건을 추가합니다.
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
-- User ALTER TABLE to create a new edge constraint.
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product);
```  

앞의 예제에서 *EC_BOUGHT1* 제약 조건에는 2개의 에지 제약 조건 절이 있습니다. 하나는 **Customer**를 **Product**에 연결하는 절이고 다른 하나는 **Supplier**를 **Product**에 연결하는 절입니다. 이러한 두 절은 따로 적용됩니다. 즉, 지정된 에지가 에지 테이블에서 허용되려면 이러한 두 절 중 하나를 만족해야 합니다.

#### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>새 에지 제약 조건 절을 사용하여 기존 에지 테이블에 새 에지 제약 조건 만들기

다음 예제에서는 `ALTER TABLE` 명령을 사용하여 **bought** 에지 테이블에 새 에지 제약 조건 절을 통해 새 에지 제약 조건을 추가합니다.
  
 ```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT,
         CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product);
 ```  

앞의 예제에서는 **bought** 에지 테이블에 별도의 두 에지 제약 조건 *EC_BOUGHT* 및 *EC_BOUGHT1*을 만들었습니다. 이러한 두 에지 제약 조건은 서로 다른 에지 제약 조건 절을 포함합니다. 에지 테이블에 둘 이상의 에지 제약 조건이 지정될 경우 지정된 에지가 에지 테이블에서 허용되려면 **모든** 에지 테이블을 만족해야 합니다. 에지가 *EC_BOUGHT* 및 *EC_BOUGHT1*을 둘 다 만족할 수는 없으므로 **bought** 에지 테이블은 비어 있어야 합니다.

이 에지 테이블에 성공적으로 삽입하려면 에지 제약 조건 중 하나를 삭제하거나 두 조건을 모두 삭제한 후 두 에지 제약 조건 절이 있는 새 에지 제약 조건을 만들어야 합니다.

```sql
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product);
GO
```  

지정된 에지가 **bought** 에지에서 허용되려면 *EC_BOUGHT_NEW* 제약 조건의 에지 제약 조건 절 중 하나를 만족하면 됩니다. 따라서 유효한 **Customer**를 **Product**에 연결하거나 **Supplier**를 **Product**에 연결하려고 하는 모든 에지가 허용됩니다.

### <a name="delete-edge-constraints"></a>에지 제약 조건 삭제

다음 예제에서는 먼저 에지 제약 조건의 이름을 식별한 후 해당 제약 조건을 삭제합니다.  
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   ) AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE;
GO
-- Return the name of edge constraint.
SELECT name  
   FROM sys.edge_constraints  
   WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
GO  
-- Delete the primary key constraint.  
ALTER TABLE bought
DROP CONSTRAINT EC_BOUGHT;
```  

### <a name="modify-edge-constraints"></a>에지 제약 조건 수정

Transact-SQL을 사용하여 에지 제약 조건을 수정하려면 먼저 기존 에지 제약 조건을 삭제하고 새로운 정의를 사용하여 다시 만들어야 합니다.


### <a name="view-edge-constraints"></a>에지 제약 조건 보기

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.

이 예제에서는 tempdb 데이터베이스에 있는 에지 테이블 `bought`의 모든 에지 제약 조건 및 해당 속성을 반환합니다.  

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
   GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;

-- CREATE edge table with edge constraints.
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
   )
   AS EDGE;

-- Query sys.edge_constraints and sys.edge_constraint_clauses to view
-- edge constraint properties.
SELECT
   EC.name AS edge_constraint_name
   , OBJECT_NAME(EC.parent_object_id) AS edge_table_name
   , OBJECT_NAME(ECC.from_object_id) AS from_node_table_name
   , OBJECT_NAME(ECC.to_object_id) AS to_node_table_name
   , is_disabled
   , is_not_trusted
FROM sys.edge_constraints EC
   INNER JOIN sys.edge_constraint_clauses ECC
   ON EC.object_id = ECC.object_id
WHERE EC.parent_object_id = object_id('bought');
```  

## <a name="related-tasks"></a>관련 작업

[CREATE TABLE(SQL 그래프)](../../t-sql/statements/create-table-sql-graph.md)  
[ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  

SQL Server의 그래프 기술에 대한 자세한 내용은 [SQL Server 및 Azure SQL Database를 사용한 Graph 처리](../graphs/sql-graph-overview.md?view=sql-server-2017)를 참조하세요.

