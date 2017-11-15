---
title: "계획 지침 속성 보기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.planguideprop.general.f1
helpviewer_keywords:
- plan guides [SQL Server], view plan guide properties
- viewing plan guide properties
ms.assetid: 8c0d2f39-59c1-4168-a649-65473f6a771b
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7de2a92c043154971b786815d8fa93ef9bb30ee
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="view-plan-guide-properties"></a>계획 지침 속성 보기
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 다음을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 계획 지침의 속성을 확인할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **계획 지침의 속성을 보려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 사용자가 소유하고 있거나 사용 권한을 부여 받은 보안 개체에 대해서만 카탈로그 뷰의 메타데이터를 볼 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>계획 지침의 속성을 보려면  
  
1.  더하기 기호를 클릭하여 계획 지침의 속성을 보려는 데이터베이스를 확장한 다음 더하기 기호를 클릭하여 **프로그래밍 기능** 폴더를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **계획 지침** 폴더를 확장합니다.  
  
3.  속성을 보려는 계획 지침을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     다음 속성이 **계획 지침 속성** 대화 상자에 표시됩니다.  
  
     **힌트**  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 적용되는 쿼리 힌트 또는 쿼리 계획을 표시합니다. 쿼리 계획이 힌트로 지정되면 해당 계획의 XML 실행 계획 출력이 표시됩니다.  
  
     **사용 안 함**  
     계획 지침의 상태를 표시합니다. 가능한 값은 **True** 및 **False**입니다.  
  
     **이름**  
     계획 지침의 이름을 표시합니다.  
  
     **매개 변수**  
     범위 유형이 SQL 또는 TEMPLATE인 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 포함된 모든 매개 변수의 데이터 형식과 이름을 표시합니다.  
  
     **범위 일괄 처리**  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나타나는 일괄 처리 텍스트를 표시합니다.  
  
     **범위 개체 이름**  
     범위 유형이 OBJECT인 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나타나는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 이름, 사용자 정의 스칼라 함수, 다중 문 테이블 반환 함수 또는 DML 트리거를 표시합니다.  
  
     **범위 스키마 이름**  
     범위 유형이 OBJECT인 경우 개체가 포함되는 스키마의 이름을 표시합니다.  
  
     **범위 유형**  
     [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 나타나는 엔터티 유형을 표시합니다. 이것은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 계획 지침과 일치시키기 위한 컨텍스트를 제공합니다. 가능한 값은 **OBJECT**, **SQL**및 **TEMPLATE**입니다.  
  
     **문**  
     계획 지침이 적용되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
4.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-properties-of-a-plan-guide"></a>계획 지침의 속성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- If a plan guide named “Guide1” already exists in the AdventureWorks2012 database, delete it.  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID(N'Guide1') IS NOT NULL  
       EXEC sp_control_plan_guide N'DROP', N'Guide1';  
    GO  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
    GO  
    -- Gets the name, created date, and all other relevant property information on the plan guide created above.   
    SELECT name AS plan_guide_name,  
       create_date,  
       query_text,  
       scope_type_desc,  
       OBJECT_NAME(scope_object_id) AS scope_object_name,  
       scope_batch,  
       parameters,  
       hints,  
       is_disabled  
    FROM sys.plan_guides  
    WHERE name = N’Guide1’;  
    GO  
    ```  
  
 자세한 내용은 [sys.plan_guides&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)를 참조하세요.  
  
  
