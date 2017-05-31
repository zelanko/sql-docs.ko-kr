---
title: "열 이름 바꾸기(데이터베이스 엔진) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], names
- renaming columns
- column names [SQL Server]
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e02a5d26a0a04d5afa1c4ddfcc9c06c503b6bd2c
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="rename-columns-database-engine"></a>열 이름 바꾸기(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블 열의 이름을 바꿀 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 열 이름을 바꿉니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 열 이름을 변경해도 해당 열에 대한 참조 이름은 자동으로 바뀌지 않습니다. 이름을 변경한 열을 참조하는 개체는 수동으로 수정해야 합니다. 예를 들어 테이블 열의 이름을 변경하고 이 열이 트리거에서 참조되는 경우 트리거를 수정하여 새로운 열 이름을 적용해야 합니다. [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 를 사용하여 이 개체에 종속된 개체를 나열한 다음 개체의 이름을 변경할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 개체에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-column-using-object-explorer"></a>개체 탐색기를 사용하여 열 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 열 이름을 바꾸려는 테이블을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다.  
  
3.  새 열 이름을 입력합니다.  
  
#### <a name="to-rename-a-column-using-table-designer"></a>테이블 디자이너를 사용하여 열 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 열 이름을 바꾸려는 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
2.  **열 이름**아래에서 변경하려는 이름을 선택하고 새 이름을 입력합니다.  
  
3.  **파일** 메뉴에서 **저장***table name*을 클릭합니다.  
  
> [!NOTE]  
>  **열 속성** 탭에서 열 이름을 변경할 수도 있습니다. 이름을 변경하려는 열을 선택하고 **이름**에 새 이름을 입력합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **열 이름을 바꾸려면**  
  
#### <a name="to-rename-a-column"></a>열 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예에서는 `TerritoryID` 테이블의 `Sales.SalesTerritory` 열 이름을 `TerrID`로 변경합니다. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
    GO  
    ```  
  
 자세한 내용은 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)을 참조하세요.  
  
  
