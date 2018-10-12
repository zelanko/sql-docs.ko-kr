---
title: 에지 제약 조건 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2018
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
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 160de04e9b8fbe83e8a771f5622f4f6103a8c7bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845601"
---
# <a name="create-edge-constraints"></a>에지 제약 조건 만들기
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

   [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 에지 제약 조건을 정의할 수 있습니다. 
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   에지 제약 조건은 그래프 에지 테이블에서만 정의할 수 있습니다. 
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  

### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>새 에지 테이블에 에지 제약 조건을 만들려면
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 이 예제는 **bought** 에지 테이블에 에지 제약 조건을 만듭니다.  
  
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
 ```  

### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>기존 에지 테이블에 에지 제약 조건을 추가하려면 
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 이 예제에서는 ALTER TABLE을 사용하여 **bought** 에지 테이블에 에지 제약 조건을 추가합니다.
  
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
        PurchaseCount INT
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product)
 GO
 ```  

### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>추가 에지 제약 조건 절을 사용하여 기존 에지 테이블에 새 에지 제약 조건 만들기
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 이 예제에서는 ALTER TABLE을 사용하여 **bought** 에지 테이블에 추가 에지 제약 조건 절을 통해 새 에지 제약 조건을 추가합니다.
  
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
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO

 -- User ALTER TABLE to create a new edge constraint.
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  
 *EC_BOUGHT1* 제약 조건에는 2개의 에지 제약 조건 절이 있습니다. 하나는 **Customer**를 **Product**에 연결하는 절이고 다른 하나는 **Supplier**를 **Product**에 연결하는 절입니다. 이러한 두 절은 따로 적용됩니다. 즉, 지정된 에지가 에지 테이블에서 허용되려면 이러한 두 절 중 하나를 만족해야 합니다. 



### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>새 에지 제약 조건 절을 사용하여 기존 에지 테이블에 새 에지 제약 조건 만들기
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여넣고 **실행**을 클릭합니다. 이 예제에서는 ALTER TABLE을 사용하여 **bought** 에지 테이블에 새 에지 제약 조건 절을 통해 새 에지 제약 조건을 추가합니다.
  
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
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product)
 GO
 ```  

 이 예제에서는 **bought** 에지 테이블에 별도의 두 에지 제약 조건 *EC_BOUGHT* 및 *EC_BOUGHT1*을 만들었습니다. 이러한 두 에지 제약 조건은 서로 다른 에지 제약 조건 절을 포함합니다. 에지 테이블에 둘 이상의 에지 제약 조건이 지정될 경우 지정된 에지가 에지 테이블에서 허용되려면 **모든** 에지 테이블을 만족해야 합니다. 에지가 *EC_BOUGHT* 및 *EC_BOUGHT1*을 둘 다 만족할 수는 없으므로 **bought** 에지 테이블은 비어 있어야 합니다. 

 이 에지 테이블에 성공적으로 삽입하려면 에지 제약 조건 중 하나를 삭제하거나 두 조건을 모두 삭제한 후 두 에지 제약 조건 절이 있는 새 에지 제약 조건을 만들어야 합니다. 

 ```sql
 USE TEMPDB
 GO
 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO
 
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1
 GO
 
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  

 이제 지정된 에지가 **bought** 에지에서 허용되려면 *EC_BOUGHT_NEW* 제약 조건의 에지 제약 조건 절 중 하나를 만족하면 됩니다. 따라서 유효한 **Customer**를 **Product**에 연결하거나 **Supplier**를 **Product**에 연결하려고 하는 모든 에지가 허용됩니다. 
