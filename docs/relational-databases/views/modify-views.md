---
title: "뷰 수정 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [SQL Server], renaming
- views [SQL Server], modifying
- modifying views
- renaming views
ms.assetid: 2d3c14dc-43e5-4324-b8fb-f2692d330b16
caps.latest.revision: 
author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8b389a635dceb2af0e8457f72ae56013edb1065c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="modify-views"></a>뷰 수정
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
뷰를 정의한 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 해당 뷰를 삭제하고 다시 만들지 않고 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 해당 정의를 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **뷰를 수정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   종속 개체를 무효화하는 방식으로 뷰 정의를 변경하지 않는 한 뷰를 수정해도 저장 프로시저나 트리거 등의 종속 개체에는 영향을 주지 않습니다.  
  
-   현재 사용 중인 뷰를 ALTER VIEW를 사용하여 수정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 해당 뷰에 대한 배타적 스키마 잠금을 얻습니다. 잠금이 부여되고 현재 뷰를 사용 중인 사용자가 없으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 프로시저 캐시에서 뷰의 복사본을 모두 삭제합니다. 해당 뷰를 참조하는 기존 계획은 캐시에 남아 있지만 다음 호출 시 다시 컴파일됩니다.  
  
-   인덱싱된 뷰에도 ALTER VIEW를 적용할 수 있지만 ALTER VIEW는 뷰에 대한 모든 인덱스를 무조건 삭제합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 ALTER VIEW를 실행하려면 최소 OBJECT에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-view"></a>뷰를 수정하려면  
  
1.  **개체 탐색기**에서 뷰가 있는 데이터베이스 옆의 더하기 기호를 클릭한 다음 **뷰** 폴더 옆의 더하기 기호를 클릭합니다.  
  
2.  수정할 뷰를 마우스 오른쪽 단추로 클릭하고 **디자인**을 클릭합니다.  
  
3.  쿼리 디자이너의 다이어그램 창에서 다음과 같은 방법으로 뷰를 변경합니다.  
  
    1.  추가하거나 제거할 요소의 확인란을 선택하거나 선택을 취소합니다.  
  
    2.  다이어그램 창 내부를 마우스 오른쪽 단추로 클릭하고 **테이블 추가...**를 선택한 다음 **테이블 추가** 대화 상자에서 뷰에 추가할 열을 선택합니다.  
  
    3.  제거할 테이블의 제목 표시줄을 마우스 오른쪽 단추로 클릭하고 **제거**를 선택합니다.  
  
4.  **파일** 메뉴에서 **저장***뷰 이름*을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-modify-a-view"></a>뷰를 수정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 먼저 뷰를 만든 다음 ALTER VIEW를 사용하여 이 뷰를 수정합니다. WHERE 절이 뷰 정의에 추가됩니다.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    -- Create a view.  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
  
    -- Modify the view by adding a WHERE clause to limit the rows returned.  
    ALTER VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID  
    WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;   
    GO  
    ```  
  
 자세한 내용은 [ALTER VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)를 참조하세요.  
  
  
