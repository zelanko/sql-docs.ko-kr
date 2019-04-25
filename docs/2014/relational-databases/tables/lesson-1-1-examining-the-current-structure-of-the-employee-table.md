---
title: Employee 테이블의 현재 구조 검사 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 38c16d837dd886785479e1e2994b5b0f19372cfe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62760866"
---
# <a name="examining-the-current-structure-of-the-employee-table"></a>Employee 테이블의 현재 구조 검사
  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스의 **HumanResources** 스키마에 **Employee** 테이블이 있습니다. 원래 테이블이 변경되지 않도록 이 단계에서는 **EmployeeDemo** 라는 **Employee**테이블의 복사본을 만듭니다. 예를 단순화하기 위해 원래 테이블에서 5개의 열만 복사합니다. 쿼리 한 다음, 합니다 **HumanResources.EmployeeDemo** 테이블을 사용 하지 않고 테이블에서 데이터가 구조화 되는 방식을 검토는 `hierarchyid` 데이터 형식.  
  
### <a name="to-copy-the-employee-table"></a>Employee 테이블을 복사하려면  
  
1.  쿼리 편집기 창에서 다음 코드를 실행하여 테이블 구조와 데이터를 **Employee** 테이블에서 **EmployeeDemo**라는 새 테이블로 복사합니다.  
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT EmployeeID, LoginID, ManagerID, Title, HireDate   
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee ;  
    GO  
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>EmployeeDemo 테이블의 구조와 데이터를 검사하려면  
  
-   이 새 **EmployeeDemo** 테이블은 새 구조로 마이그레이션할 수 있는 기존 데이터베이스의 일반적인 테이블을 나타냅니다. 쿼리 편집기 창에서 다음 코드를 실행하여 테이블이 자체 조인을 통해 직원/관리자 관계를 나타내는 방법을 표시합니다.  
  
    ```  
    SELECT   
         Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
         Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.Title  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  Title  
    NULL NULL                      109 adventure-works\ken0     Chief Executive Officer  
    3    adventure-works\roberto0  4   adventure-works\rob0     Senior Tool Designer  
    3    adventure-works\roberto0  9   adventure-works\gail0    Design Engineer  
    3    adventure-works\roberto0  11  adventure-works\jossef0  Design Engineer  
    3    adventure-works\roberto0  158 adventure-works\dylan0   Research and Development Manager  
    3    adventure-works\roberto0  263 adventure-works\ovidiu0  Senior Tool Designer  
    3    adventure-works\roberto0  267 adventure-works\michael8 Senior Design Engineer  
    3    adventure-works\roberto0  270 adventure-works\sharon0  Design Engineer  
    6    adventure-works\david0    2   adventure-works\kevin0   Marketing Assistant  
    ...  
    ```  
  
     결과로 총 290개의 행이 나타납니다.  
  
 `ORDER BY` 절로 인해 출력에 각 관리자 수준의 직접 보고가 함께 나열되었습니다. 예를 들어 **MgrID** 3(roberto0)의 모든 직접 보고 7개가 서로 인접하게 나열됩니다. 불가능하지는 않지만 **MgrID** 3에게 결과적으로 보고하게 되는 모든 직원을 그룹화하기는 훨씬 더 어렵습니다.  
  
 다음 태스크에서는 `hierarchyid` 데이터 형식으로 새 테이블을 만들고 데이터를 새 테이블로 이동합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [기존 계층적 데이터로 테이블 채우기](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
