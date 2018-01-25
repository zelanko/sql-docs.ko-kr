---
title: "계층적 메서드를 사용하여 계층적 테이블 채우기 | Microsoft 문서"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
f1_keywords: HierarchyID
helpviewer_keywords: HierarchyID
ms.assetid: 2c95fa60-5b8e-4a05-ac09-cffe2b05900a
caps.latest.revision: "22"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 24e6481c9f9122786d46cf7b813fdbdddac2ef74
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-2-2---populating-a-hierarchical-table-using-hierarchical-methods"></a>2-2단원 - 계층적 메서드를 사용하여 계층적 테이블 채우기
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]의 마케팅 부서에는 8명의 직원이 근무하고 있습니다. 직원 계층은 다음과 같습니다.  
  
**EmployeeID**가 6인 **David** 는 Marketing Manager입니다. 다음과 같은 3명의 Marketing Specialist가 **David**에게 보고합니다.  
  
-   **Sariya**, **EmployeeID** 46  
  
-   **John**, **EmployeeID** 271  
  
-   **Jill**, **EmployeeID** 119  
  
Marketing Assistant인 **Wanida** (**EmployeeID** 269)는 **Sariya**에게 보고하고 다른 Marketing Assistant인 **Mary** (**EmployeeID** 272)는 **John**에게 보고합니다.  
  
### <a name="to-insert-the-root-of-the-hierarchy-tree"></a>계층 트리의 루트를 삽입하려면  
  
1.  다음 예에서는 Marketing Manager **David** 를 계층의 루트에 있는 테이블에 삽입합니다. **OrdLevel** 열은 계산 열입니다. 따라서 INSERT 문의 일부가 아닙니다. 이 첫 번째 레코드는 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) 메서드를 사용하여 이 첫 번째 레코드를 계층의 루트로 채웁니다.  
  
    ```  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  다음 코드를 실행하여 테이블의 초기 행을 검사합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
이전 단원에서와 같이 `ToString()` 메서드를 사용하여 **hierarchyid** 데이터 형식을 보다 이해하기 쉬운 형식으로 변환합니다.  
  
### <a name="to-insert-a-subordinate-employee"></a>부하 직원을 삽입하려면  
  
1.  **Sariya** 는 **David**에게 보고합니다. **Sariya** 의 노드를 삽입하려면 **hierarchyid** 데이터 형식의 적절한 **OrgNode**값을 만들어야 합니다. 다음 코드에서는 **hierarchyid** 데이터 형식의 변수를 만들고 이를 테이블의 루트 OrgNode 값으로 채웁니다. 그런 다음 해당 변수를 [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) 메서드와 함께 사용하여 하위 노드인 행을 삽입합니다. `GetDescendant` 는 두 개의 인수를 사용합니다. 인수 값에 대해 다음 옵션을 검토합니다.  
  
    -   부모가 NULL인 경우 `GetDescendant` 는 NULL을 반환합니다.  
  
    -   부모가 NULL이 아니고 자식1과 자식2가 모두 NULL인 경우 `GetDescendant` 는 부모의 자식을 반환합니다.  
  
    -   부모와 자식1이 NULL이 아니고 자식2가 NULL인 경우 `GetDescendant` 는 자식1보다 큰 부모의 자식을 반환합니다.  
  
    -   부모와 자식2가 NULL이 아니고 자식1이 NULL인 경우 `GetDescendant` 는 자식2보다 작은 부모의 자식을 반환합니다.  
  
    -   부모, 자식1 및 자식2가 모두 NULL이 아닌 경우 `GetDescendant` 는 자식1보다 크고 자식2보다 작은 부모의 자식을 반환합니다.  
  
    다음 코드에서는 테이블에 루트를 제외한 행이 아직 없기 때문에 루트 부모의 `(NULL, NULL)` 인수를 사용합니다. 다음 코드를 실행하여 **Sariya**를 삽입합니다.  
  
    ```  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  첫 번째 프로시저의 쿼리를 반복하여 테이블을 쿼리하고 항목이 나타나는 방식을 확인합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="to-create-a-procedure-for-entering-new-nodes"></a>새 노드를 입력하는 프로시저를 만들려면  
  
1.  데이터 입력을 단순화하기 위해 다음 저장 프로시저를 만들어 직원을 **EmployeeOrg** 테이블에 추가합니다. 이 프로시저는 추가하는 직원에 대한 입력 값을 받아들입니다. 여기에는 새 직원의 관리자에게 지정된 **EmployeeID** , 새 직원의 **EmployeeID** 번호 및 해당 직원의 이름과 직책이 포함됩니다. 이 프로시저는 `GetDescendant()` 및 [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) 메서드를 사용합니다. 다음 코드를 실행하여 프로시저를 만듭니다.  
  
    ```  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  다음 예에서는 **David**에게 직접 또는 간접적으로 보고하는 나머지 직원 4명을 추가합니다.  
  
    ```  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  다시 다음 쿼리를 실행하여 **EmployeeOrg** 테이블의 행을 검사합니다.  
  
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
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
이제 테이블이 마케팅 조직으로 모두 채워졌습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[계층 메서드를 사용하여 계층적 테이블 쿼리](../../relational-databases/tables/lesson-2-3-querying-a-hierarchical-table-using-hierarchy-methods.md)  
  
  
  
