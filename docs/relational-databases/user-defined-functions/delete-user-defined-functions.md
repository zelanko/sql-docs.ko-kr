---
description: 사용자 정의 함수 삭제
title: 사용자 정의 함수 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 839a4f9e6cbba0b3ac1e966de7cf63ef6dd21c59
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466724"
---
# <a name="delete-user-defined-functions"></a>사용자 정의 함수 삭제
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 다음을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 사용자 정의 함수를 삭제할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 사용자 정의 함수를 삭제하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   데이터베이스에 이 함수를 참조하고 SCHEMABINDING을 사용하여 만든 Transact-SQL 함수나 뷰가 있는 경우 또는 해당 함수를 참조하는 계산 열, CHECK 제약 조건 또는 DEFAULT 제약 조건이 있는 경우 함수를 삭제할 수 없습니다.  
  
-   이 함수를 참조하고 인덱싱된 계산 열이 있는 경우 함수를 삭제할 수 없습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 함수가 속한 스키마에 대한 ALTER 권한 또는 함수에 대한 CONTROL 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-user-defined-function"></a>사용자 정의 함수를 삭제하려면  
  
1.  수정할 함수가 포함된 데이터베이스 옆의 더하기 기호를 클릭합니다.  
  
2.  **프로그래밍 기능** 폴더 옆의 더하기 기호를 클릭합니다.  
  
3.  수정할 함수가 포함된 폴더 옆의 더하기 기호를 클릭합니다.  
  
    -   테이블 반환 함수  
  
    -   스칼라 반환 함수  
  
    -   Aggregate 함수  
  
4.  삭제할 함수를 마우스 오른쪽 단추로 클릭하고 **삭제** 를 선택합니다.  
  
5.  **개체 삭제** 대화 상자에서 **확인** 을 클릭합니다.  

    > [!IMPORTANT]  
    >  **개체 삭제** 대화 상자에서 **종속성 표시** 를 클릭하여 _function\_name_**종속성** 대화 상자를 엽니다. 이 대화 상자에는 해당 함수에 종속된 모든 개체와 해당 함수가 종속된 모든 개체가 표시됩니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-user-defined-function"></a>사용자 정의 함수를 삭제하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- creates function called "Sales.ufn_SalesByStore"  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 자세한 내용은 [DROP FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)을 참조하세요.  
  
  
