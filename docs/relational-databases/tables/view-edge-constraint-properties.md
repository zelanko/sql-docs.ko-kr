---
title: 에지 제약 조건 속성 보기 | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server], attributes
- displaying edge constraint attributes
- viewing edge constraint attributes
ms.assetid: b0e57cb7-9b26-4b96-b76a-1f59f5f498c5
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 129d61ddf42a159dbeba74a168d10dac72094b3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790681"
---
# <a name="view-edge-constraint-properties"></a>에지 제약 조건 속성 보기
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 에지 제약 조건 속성 [!INCLUDE[noversion](../../includes/ssnoversion-md.md)]를 볼 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **특정 테이블의 외래 키 특성을 보려면:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-foreign-key-attributes-of-a-relationship-in-a-specific-table"></a>특정 테이블의 관계에 대한 외래 키 특성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 이 예제에서는 tempdb 데이터베이스에 있는 에지 테이블 `bought`의 모든 에지 제약 조건 및 해당 속성을 반환합니다.  
    
    ```sql
    USE TEMPDB
    GO
    -- CREATE node and edge tables
    CREATE TABLE Customer
      (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
      )
    AS NODE
    GO

    CREATE TABLE Supplier
      (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
      )
    AS NODE
    GO

    CREATE TABLE Product 
      (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
      ) 
    AS NODE
    GO
    -- CREATE edge table with edge constraints.
    CREATE TABLE bought
      (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
      )
    AS EDGE
    GO
    
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
    WHERE EC.parent_object_id = object_id('bought')
    ```  
  
 자세한 내용은 [sys.edge_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraints-transact-sql.md) 및 [sys.edge_constraint_clauses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraint-clauses-transact-sql.md)을 참조하세요.  
  
###  <a name="TsqlExample"></a>  
