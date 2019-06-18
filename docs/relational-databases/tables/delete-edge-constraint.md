---
title: 에지 제약 조건 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing edge constraint
- deleting edge constraint, deleting connection constraint
- SQL Graph
- graph edge constraints
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3761d9e8507eb7051fe7a6cc39b83abfa091566d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62515887"
---
# <a name="delete-edge-constraints"></a>에지 제약 조건 삭제
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)]에서 에지 제약 조건을 삭제할 수 있습니다. 
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **기본 키를 삭제하려면**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 테이블에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-an-edge-constraint"></a>에지 제약 조건을 삭제하려면
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 먼저 에지 제약 조건의 이름을 식별한 후 해당 제약 조건을 삭제합니다.  
  
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

    CREATE TABLE Product 
    (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
    ) AS NODE
    GO

    CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE
    GO
    
    -- Return the name of edge constraint.
    SELECT name  
    FROM sys.edge_constraints  
    WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
    GO  

    -- Delete the primary key constraint.  
    ALTER TABLE bought
    DROP CONSTRAINT EC_BOUGHT
    GO
    ```  
  
 자세한 내용은 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [sys.edge_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraints-transact-sql.md) 및 [ssys.edge_constraint_clauses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraint-clauses-transact-sql.md)을 참조하세요.
  
###  <a name="TsqlExample"></a>  
