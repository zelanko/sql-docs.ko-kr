---
title: 계층적 메서드를 사용하여 계층적 테이블 쿼리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 3b4f7dae-65b5-4d8d-8641-87aba9aa692d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be1d0dcd37dba9b1025ba3e4a93aa60d2198b237
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110051"
---
# <a name="querying-a-hierarchical-table-using-hierarchy-methods"></a>계층 메서드를 사용하여 계층적 테이블 쿼리
  이제 HumanResources.EmployeeOrg 테이블을 완전히 채웠으므로 이 태스크에서는 일부 계층 메서드를 사용하여 계층을 쿼리하는 방법을 보여 줍니다.  
  
### <a name="to-find-subordinate-nodes"></a>부하 직원 노드를 찾으려면  
  
1.  Sariya에게는 부하 직원이 한 명 있습니다. Sariya의 부하 직원에 대해 쿼리하려면 [IsDescendantOf](/sql/t-sql/data-types/isdescendantof-database-engine) 메서드를 사용하는 다음 쿼리를 실행합니다.  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
     결과에 Sariya와 Wanida가 모두 나열됩니다. Sariya는 0 수준에서 하위 항목이므로 나열됩니다. Wanida는 1 수준에서 하위 항목입니다.  
  
2.  [GetAncestor](/sql/t-sql/data-types/getancestor-database-engine) 메서드를 사용하여 이 정보에 대해 쿼리할 수도 있습니다. `GetAncestor` 는 반환하려는 수준에 대한 인수를 사용합니다. Wanida는 Sariya보다 한 수준 아래이므로 다음 코드와 같이 `GetAncestor(1)` 를 사용합니다.  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
     이번에는 결과에 Wanida만 나열됩니다.  
  
3.  이제 `@CurrentEmployee` 를 David(EmployeeID 6)로 변경하고 수준을 2로 변경합니다. 다음을 실행하여 Wanida도 반환합니다.  
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
     이번에는 David에게 보고하는 두 수준 아래에 있는 Mary도 반환됩니다.  
  
### <a name="to-use-getroot-and-getlevel"></a>GetRoot 및 GetLevel을 사용하려면  
  
1.  계층이 커질수록 계층에서의 멤버 위치를 확인하기가 더 어려워집니다. [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) 메서드를 사용하여 계층에서의 각 행 수준을 알 수 있습니다. 다음 코드를 실행하여 모든 행의 수준을 확인합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  [GetRoot](/sql/t-sql/data-types/getroot-database-engine) 메서드를 사용하여 계층의 루트 노드를 확인할 수 있습니다. 다음 코드에서는 루트인 단일 행을 반환합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
  
 다음 태스크에서는 계층을 다시 구성합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [계층 메서드를 사용하여 계층적 테이블의 데이터 다시 정렬](lesson-2-4-reordering-data-in-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
