---
title: 계층적 메서드를 사용하여 계층적 테이블의 데이터 다시 정렬 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: 7b8064c7-62c6-488d-84d2-57a5828fb907
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a1058effc6a942bbe75d0f6369860fb4ab73330
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33007240"
---
# <a name="lesson-2-4---reordering-data-in-a-hierarchical-table-using-hierarchical-methods"></a>2-4단원 - 계층적 메서드를 사용하여 계층적 테이블의 데이터 다시 정렬
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
계층을 다시 구성하는 것은 일반적인 유지 관리 태스크입니다. 이 태스크에서는 UPDATE 문을 [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) 메서드와 함께 사용하여 먼저 단일 행을 계층의 새 위치로 이동합니다. 그런 다음 전체 하위 트리를 새 위치로 이동합니다.  
  
`GetReparentedValue` 메서드는 두 개의 인수를 사용합니다. 첫 번째 인수는 수정할 계층 부분을 설명합니다. 예를 들어 계층이 **/1/4/2/3/** 인 경우 **/1/4/** 섹션을 변경하여 계층을 **/2/1/2/3/** 으로 만들고 마지막 두 노드(**2/3/**)는 변경하지 않으려면 변경되는 노드(**/1/4/**)를 첫 번째 인수로 제공해야 합니다. 두 번째 인수는 새 계층 구조 수준(이 예제의 경우 **/2/1/**)을 제공합니다. 두 인수의 수준 수가 같을 필요는 없습니다.  
  
### <a name="to-move-a-single-row-to-a-new-location-in-the-hierarchy"></a>단일 행을 계층의 새 위치로 이동하려면  
  
1.  현재 Wanida는 Sariya에게 보고합니다. 이 절차에서는 Wanida가 Jill에게 보고하도록 현재 노드 **/1/1/** 에서 Wanida를 이동합니다. Wanida의 새 노드는 **/3/1/** 이 되므로 **/1/** 이 첫 번째 인수이고 **/3/** 이 두 번째 인수입니다. 이러한 인수는 Sariya와 Jill의 **OrgNode** 값에 해당합니다. 다음 코드를 실행하여 Wanida를 Sariya의 조직에서 Jill의 조직으로 이동합니다.  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  다음 코드를 실행하여 결과를 확인합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    이제 Wanida는 **/3/1/** 노드에 있습니다.  
  
### <a name="to-reorganize-a-section-of-a-hierarchy"></a>계층의 섹션을 다시 구성하려면  
  
1.  동시에 많은 사람을 이동하는 방법을 보여 주기 위해 먼저 다음 코드를 실행하여 Wanida에게 보고하는 인턴을 한 명 추가합니다.  
  
    ```  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  이제 Kevin은 Wanida에게 보고하고 Wanida는 Jill에게 보고하며 Jill은 David에게 보고합니다. 즉, Kevin은 **/3/1/1/** 수준에 있습니다. Jill의 부하 직원을 모두 새 관리자에게로 이동하기 위해 **OrgNode** 가 **/3/** 인 모든 노드를 새 값으로 업데이트합니다. 다음 코드를 실행하여 Wanida가 Sariya에게 보고하도록 업데이트하고 Kevin은 계속 Wanida에게 보고하도록 둡니다.  
  
    ```  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  다음 코드를 실행하여 결과를 확인합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
Jill에게 보고했던 전체 조직 트리(Wanida와 Kevin)가 이제 Sariya에게 보고합니다.  
  
계층의 섹션을 다시 구성하는 저장 프로시저는 [Moving Subtrees](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees)의 "하위 트리 이동" 섹션을 참조하세요.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[요약: 계층적 테이블의 데이터 관리](../../relational-databases/tables/lesson-2-5-summary-managing-data-in-a-hierarchical-table.md)  
  
  
  
