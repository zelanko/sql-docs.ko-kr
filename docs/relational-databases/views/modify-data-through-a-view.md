---
title: 뷰를 통해 데이터 수정 | Microsoft 문서
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb3c4075471394652fa5952fa60f8da9a367d834
ms.sourcegitcommit: 79d8912941d66abdac4e8402a5a742fa1cb74e6d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80550226"
---
# <a name="modify-data-through-a-view"></a>뷰를 통해 데이터 수정
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 SQL Server에서 기본 테이블의 데이터를 수정할 수 있습니다.  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)의 '업데이트할 수 있는 뷰' 섹션을 참조하세요.  
  
  
###  <a name="permissions"></a><a name="Permissions"></a> 권한  
 수행하는 동작에 따라 대상 테이블에 대한 UPDATE, INSERT 또는 DELETE 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-table-data-through-a-view"></a>뷰를 통해 테이블 데이터를 수정하려면  
  
1.  **개체 탐색기**에서 뷰가 포함된 데이터베이스를 확장한 다음 **뷰**를 확장합니다.  
  
2.  뷰를 마우스 오른쪽 단추로 클릭하고 **상위 200개의 행 편집**을 선택합니다.  
  
3.  수정될 행을 반환하기 위해 **SQL** 창에서 SELECT 문을 수정해야 할 수도 있습니다.  
  
4.  **결과** 창에서 변경하거나 삭제할 행을 찾습니다. 행을 삭제하려면 행을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다. 하나 이상의 열에서 데이터를 변경하려면 열에서 데이터를 수정합니다.  
  
    > **중요!!** 뷰가 여러 개의 기본 테이블을 참조하는 경우 행을 삭제할 수 없습니다. 단일 기본 테이블에 속하는 열만 업데이트할 수 있습니다.  
  
5.  행을 삽입하려면 행의 끝으로 스크롤하여 새 값을 삽입합니다.  

    > **중요!** 뷰가 여러 개의 기본 테이블을 참조하는 경우 행을 삽입할 수 없습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-update-table-data-through-a-view"></a>뷰를 통해 테이블 데이터를 업데이트하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 뷰 `StartDate` 의 열을 참조하여 특정 직원의 `EndDate` 및 `HumanResources.vEmployeeDepartmentHistory`열 값을 변경합니다. 이 뷰는 두 테이블에서 값을 반환합니다. 수정할 열이 하나의 기본 테이블에만 속해 있기 때문에 다음 문은 성공합니다.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    UPDATE HumanResources.vEmployeeDepartmentHistory  
    SET StartDate = '20110203', EndDate = GETDATE()   
    WHERE LastName = N'Smith' AND FirstName = 'Samantha';   
    GO  
    ```  
  
 자세한 내용은 [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)를 참조하세요.  
  
#### <a name="to-insert-table-data-through-a-view"></a>뷰를 통해 테이블 데이터를 삽입하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 뷰 `HumanResouces.Department` 의 관련 열을 지정하여 기본 테이블 `HumanResources.vEmployeeDepartmentHistory`에 새 행을 삽입합니다. 단일 기본 테이블의 열만 지정되고 기본 테이블의 다른 열에 기본값이 들어 있으므로 이 문은 성공합니다.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 자세한 내용은 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)를 참조하세요.  
  
  
