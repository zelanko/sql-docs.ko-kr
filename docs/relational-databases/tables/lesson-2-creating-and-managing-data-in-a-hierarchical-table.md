---
title: '2단원: 계층적 테이블의 데이터 만들기 및 관리 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 657dedcf4944a2540d1237b53fa8ea822c31ae3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031637"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>2단원: 계층적 테이블의 데이터 만들기 및 관리
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
1단원에서는 **hierarchyid** 데이터 형식을 사용하여 기존 테이블을 수정한 다음 기존 데이터 표현으로 **hierarchyid** 열을 채웠습니다. 이 단원에서는 계층 메서드를 사용하여 새 테이블에 처음부터 데이터를 삽입합니다. 그런 다음 계층 메서드를 사용하여 데이터를 쿼리하고 조작합니다. 

## <a name="prerequisites"></a>사전 요구 사항  
이 자습서를 완료하려면 SQL Server Management Studio, SQL Server를 실행하는 서버에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다.

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks2017 샘플 데이터베이스](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)를 다운로드합니다.

SSMS에서 데이터베이스를 복원하기 위한 지침은 [데이터베이스 복원](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요.   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>hierarchyid 데이터 형식을 사용하여 테이블 만들기
다음 예에서는 직원 데이터와 보고 계층을 포함하는 EmployeeOrg라는 테이블을 만듭니다. 이 예제에서는 AdventureWorks2017 데이터베이스에 테이블을 만들지만 이는 선택 사항입니다. 예를 간단히 유지하기 위해 테이블에는 다음 5개 열만 포함합니다.  
  
-   OrgNode는 계층 관계를 저장하는 **hierarchyid** 열입니다.   
-   OrgLevel은 계산 열이며 계층의 각 노드 수준을 저장하는 OrgNode 열을 기반으로 합니다. 이는 너비 우선 인덱스에 사용됩니다.  
-   EmployeeID에는 급여와 같은 애플리케이션에 사용되는 일반적인 직원 ID가 포함됩니다. 새 애플리케이션 개발 시 애플리케이션에서 OrgNode를 사용할 수 있으므로 이러한 별도의 EmployeeID 열은 필요하지 않습니다.   
-   EmpName에는 직원의 이름이 포함됩니다.    
-   Title에는 직원의 직책이 포함됩니다.  

## <a name="create-the-employeeorg-table"></a>EmployeeOrg 테이블 만들기  
  
1.  쿼리 편집기 창에서 다음 코드를 실행하여 `EmployeeOrg` 테이블을 만듭니다. `OrgNode` 열을 클러스터형 인덱스가 있는 기본 키로 지정하면 깊이 우선 인덱스가 생성됩니다.  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  다음 코드를 실행하여 `OrgLevel` 및 `OrgNode` 열에 복합 인덱스를 만들어 효율적인 너비 우선 검색을 지원합니다.  
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
이제 테이블에 데이터를 채울 준비가 되었습니다. 다음 태스크에서는 계층 메서드를 사용하여 테이블을 채웁니다.   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>계층 메서드를 사용하여 계층적 테이블 채우기
AdventureWorks2017에는 마케팅 부서에서 근무하는 8명의 직원이 있습니다. 직원 계층은 다음과 같습니다.  
  
**EmployeeID**가 6인 **David** 는 Marketing Manager입니다. 다음과 같은 3명의 Marketing Specialist가 **David**에게 보고합니다.  
  
-   **Sariya**, **EmployeeID** 46  
  
-   **John**, **EmployeeID** 271  
  
-   **Jill**, **EmployeeID** 119  
  
Marketing Assistant인 **Wanida** (**EmployeeID** 269)는 **Sariya**에게 보고하고 다른 Marketing Assistant인 **Mary** (**EmployeeID** 272)는 **John**에게 보고합니다.  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>계층 트리의 루트 삽입  
  
1.  다음 예에서는 Marketing Manager **David** 를 계층의 루트에 있는 테이블에 삽입합니다. **OrdLevel** 열은 계산 열입니다. 따라서 INSERT 문의 일부가 아닙니다. 이 첫 번째 레코드는 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) 메서드를 사용하여 이 첫 번째 레코드를 계층의 루트로 채웁니다.  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  다음 코드를 실행하여 테이블의 초기 행을 검사합니다.  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
이전 단원에서와 같이 `ToString()` 메서드를 사용하여 **hierarchyid** 데이터 형식을 보다 이해하기 쉬운 형식으로 변환합니다.  
  
### <a name="insert-a-subordinate-employee"></a>부하 직원 삽입  
  
1.  **Sariya** 는 **David**에게 보고합니다. **Sariya** 의 노드를 삽입하려면 **hierarchyid** 데이터 형식의 적절한 **OrgNode**값을 만들어야 합니다. 다음 코드에서는 **hierarchyid** 데이터 형식의 변수를 만들고 이를 테이블의 루트 OrgNode 값으로 채웁니다. 그런 다음 해당 변수를 [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) 메서드와 함께 사용하여 하위 노드인 행을 삽입합니다. `GetDescendant` 는 두 개의 인수를 사용합니다. 인수 값에 대해 다음 옵션을 검토합니다.  
  
    -   부모가 NULL인 경우 `GetDescendant` 는 NULL을 반환합니다.  
    -   부모가 NULL이 아니고 자식1과 자식2가 모두 NULL인 경우 `GetDescendant` 는 부모의 자식을 반환합니다.  
    -   부모와 자식1이 NULL이 아니고 자식2가 NULL인 경우 `GetDescendant` 는 자식1보다 큰 부모의 자식을 반환합니다.   
    -   부모와 자식2가 NULL이 아니고 자식1이 NULL인 경우 `GetDescendant` 는 자식2보다 작은 부모의 자식을 반환합니다.   
    -   부모, 자식1 및 자식2가 모두 NULL이 아닌 경우 `GetDescendant` 는 자식1보다 크고 자식2보다 작은 부모의 자식을 반환합니다.  
  
    다음 코드에서는 테이블에 루트를 제외한 행이 아직 없기 때문에 루트 부모의 `(NULL, NULL)` 인수를 사용합니다. 다음 코드를 실행하여 **Sariya**를 삽입합니다.  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  첫 번째 프로시저의 쿼리를 반복하여 테이블을 쿼리하고 항목이 나타나는 방식을 확인합니다.  
  
    ```sql  
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
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>새 노드를 입력하는 프로시저 만들기  
  
1.  데이터 입력을 단순화하기 위해 다음 저장 프로시저를 만들어 직원을 **EmployeeOrg** 테이블에 추가합니다. 이 프로시저는 추가하는 직원에 대한 입력 값을 받아들입니다. 여기에는 새 직원의 관리자에게 지정된 **EmployeeID** , 새 직원의 **EmployeeID** 번호 및 해당 직원의 이름과 직책이 포함됩니다. 이 프로시저는 `GetDescendant()` 및 [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) 메서드를 사용합니다. 다음 코드를 실행하여 프로시저를 만듭니다.  
  
    ```sql  
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
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  다시 다음 쿼리를 실행하여 **EmployeeOrg** 테이블의 행을 검사합니다.  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
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

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>계층 메서드를 사용하여 계층적 테이블 쿼리
이제 HumanResources.EmployeeOrg 테이블을 완전히 채웠으므로 이 태스크에서는 일부 계층 메서드를 사용하여 계층을 쿼리하는 방법을 보여 줍니다.  
  
### <a name="find-subordinate-nodes"></a>하위 노드 찾기  
  
1.  Sariya에게는 부하 직원이 한 명 있습니다. Sariya의 부하 직원에 대해 쿼리하려면 [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) 메서드를 사용하는 다음 쿼리를 실행합니다.  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    결과에 Sariya와 Wanida가 모두 나열됩니다. Sariya는 0 수준에서 하위 항목이므로 나열됩니다. Wanida는 1 수준에서 하위 항목입니다.  
  
2.  [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) 메서드를 사용하여 이 정보에 대해 쿼리할 수도 있습니다. `GetAncestor` 는 반환하려는 수준에 대한 인수를 사용합니다. Wanida는 Sariya보다 한 수준 아래이므로 다음 코드와 같이 `GetAncestor(1)` 를 사용합니다.  
  
    ```sql  
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
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    이번에는 David에게 보고하는 두 수준 아래에 있는 Mary도 반환됩니다.  
  
## <a name="use-getroot-and-getlevel"></a>GetRoot 및 GetLevel 사용  
  
1.  계층이 커질수록 계층에서의 멤버 위치를 확인하기가 더 어려워집니다. [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 메서드를 사용하여 계층에서의 각 행 수준을 알 수 있습니다. 다음 코드를 실행하여 모든 행의 수준을 확인합니다.  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  [GetRoot](../../t-sql/data-types/getroot-database-engine.md) 메서드를 사용하여 계층의 루트 노드를 확인할 수 있습니다. 다음 코드에서는 루트인 단일 행을 반환합니다.  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>계층 메서드를 사용하여 계층적 테이블의 데이터 다시 정렬
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
계층을 다시 구성하는 것은 일반적인 유지 관리 태스크입니다. 이 태스크에서는 UPDATE 문을 [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) 메서드와 함께 사용하여 먼저 단일 행을 계층의 새 위치로 이동합니다. 그런 다음 전체 하위 트리를 새 위치로 이동합니다.  
  
`GetReparentedValue` 메서드는 두 개의 인수를 사용합니다. 첫 번째 인수는 수정할 계층 부분을 설명합니다. 예를 들어 계층이 **/1/4/2/3/** 인 경우 **/1/4/** 섹션을 변경하여 계층을 **/2/1/2/3/** 으로 만들고 마지막 두 노드(**2/3/** )는 변경하지 않으려면 변경되는 노드( **/1/4/** )를 첫 번째 인수로 제공해야 합니다. 두 번째 인수는 새 계층 구조 수준(이 예제의 경우 **/2/1/** )을 제공합니다. 두 인수의 수준 수가 같을 필요는 없습니다.  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>단일 행을 계층의 새 위치로 이동  
  
1.  현재 Wanida는 Sariya에게 보고합니다. 이 절차에서는 Wanida가 Jill에게 보고하도록 현재 노드 **/1/1/** 에서 Wanida를 이동합니다. Wanida의 새 노드는 **/3/1/** 이 되므로 **/1/** 이 첫 번째 인수이고 **/3/** 이 두 번째 인수입니다. 이러한 인수는 Sariya와 Jill의 **OrgNode** 값에 해당합니다. 다음 코드를 실행하여 Wanida를 Sariya의 조직에서 Jill의 조직으로 이동합니다.  
  
    ```sql  
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
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    이제 Wanida는 **/3/1/** 노드에 있습니다.  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>계층의 섹션 다시 구성  
  
1.  동시에 많은 사람을 이동하는 방법을 보여 주기 위해 먼저 다음 코드를 실행하여 Wanida에게 보고하는 인턴을 한 명 추가합니다.  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  이제 Kevin은 Wanida에게 보고하고 Wanida는 Jill에게 보고하며 Jill은 David에게 보고합니다. 즉, Kevin은 **/3/1/1/** 수준에 있습니다. Jill의 부하 직원을 모두 새 관리자에게로 이동하기 위해 **OrgNode** 가 **/3/** 인 모든 노드를 새 값으로 업데이트합니다. 다음 코드를 실행하여 Wanida가 Sariya에게 보고하도록 업데이트하고 Kevin은 계속 Wanida에게 보고하도록 둡니다.  
  
    ```sql  
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
  
    ```sql  
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
  
