---
title: 뷰 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e52ab35b0f75f80a6117995a353b66c320a5294
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085593"
---
# <a name="delete-views"></a>뷰 삭제
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 다음을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 뷰를 삭제할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   뷰를 삭제하면 해당 뷰의 정의 및 뷰에 대한 기타 정보가 시스템 카탈로그에서 삭제됩니다. 또한 해당 뷰에 대한 모든 권한도 삭제됩니다.  
  
-   `DROP TABLE` 을 사용하여 삭제된 테이블의 모든 뷰는 `DROP VIEW`를 사용하여 명시적으로 삭제되어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 SCHEMA에 대한 ALTER 권한 또는 OBJECT에 대한 CONTROL 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-delete-a-view-from-a-database"></a>데이터베이스에서 뷰를 삭제하려면  
  
1.  **개체 탐색기**에서 삭제할 뷰가 포함된 데이터베이스를 확장한 다음 **뷰** 폴더를 확장합니다.  
  
2.  삭제할 뷰를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
3.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  
  
    > [!IMPORTANT]  
    >  **개체 삭제** 대화 상자에서 **종속성 표시** 를 클릭하여 *view_name***종속성** 대화 상자를 엽니다. 이 대화 상자에는 해당 뷰에 종속된 모든 개체와 해당 뷰가 종속된 모든 개체가 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-delete-a-view-from-a-database"></a>데이터베이스에서 뷰를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 지정된 뷰가 이미 존재하는 경우에만 해당 뷰를 삭제합니다.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 자세한 내용은 [DROP VIEW&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)를 참조하세요.  
  
  
