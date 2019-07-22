---
title: '1단원: 테이블을 계층 구조로 변환 | Microsoft Docs'
ms.custom: ''
ms.date: 08/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1a9217d42af6b361a02595abcb459102183494b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016344"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>1단원: 테이블을 계층 구조로 변환
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
자체 조인을 사용하여 계층 관계를 나타내는 테이블을 보유하고 있는 경우 이 단원의 내용을 참조하여 해당 테이블을 계층 구조로 변환할 수 있습니다. 이 표현을 **hierarchyid**를 사용하는 표현으로 마이그레이션하는 작업은 비교적 쉽습니다. 마이그레이션하면 간단하고 이해하기 쉬운 계층적 표현이 완성되며 효율적인 쿼리를 위해 여러 가지 방법으로 인덱싱할 수 있습니다.  
  
이 단원에서는 기존 테이블을 검토하고, **hierarchyid** 열이 포함된 새 테이블을 만들고, 원본 테이블의 데이터로 이 테이블을 채운 다음 인덱싱 방법 3가지를 보여 줍니다. 이 단원에서는 다음 항목을 다룹니다.  
 
  
## <a name="prerequisites"></a>사전 요구 사항  
이 자습서를 완료하려면 SQL Server Management Studio, SQL Server를 실행하는 서버에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다.

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks2017 샘플 데이터베이스](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)를 다운로드합니다.

SSMS에서 데이터베이스를 복원하기 위한 지침은 [데이터베이스 복원](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)을 참조하세요.  

## <a name="examine-the-current-structure-of-the-employee-table"></a>Employee 테이블의 현재 구조 검사
샘플 Adventureworks2017(또는 이상) 데이터베이스에는 **HumanResources** 스키마에 **Employee** 테이블이 있습니다. 원래 테이블이 변경되지 않도록 이 단계에서는 **EmployeeDemo** 라는 **Employee**테이블의 복사본을 만듭니다. 예를 단순화하기 위해 원래 테이블에서 5개의 열만 복사합니다. 그런 다음 **HumanResources.EmployeeDemo** 테이블을 쿼리하여 **hierarchyid** 데이터 형식을 사용하지 않고 한 테이블에서 데이터가 구조화되는 방식을 검토합니다.  
  
### <a name="copy-the-employee-table"></a>Employee 테이블 복사  
  
1.  쿼리 편집기 창에서 다음 코드를 실행하여 테이블 구조와 데이터를 **Employee** 테이블에서 **EmployeeDemo**라는 새 테이블로 복사합니다. 원래 테이블에서 hierarchyid를 이미 사용했으므로 이 쿼리는 기본적으로 계층 구조를 평면화하여 직원의 관리자를 검색합니다. 이 단원의 다음 부분에서는 이 계층 구조를 다시 구성합니다.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]


   ```sql  
   USE AdventureWorks2017;  
   GO  
     if OBJECT_ID('HumanResources.EmployeeDemo') is not null
    drop table HumanResources.EmployeeDemo 

    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
     (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
        WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
            (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID,
          emp.JobTitle, emp.HireDate
   INTO HumanResources.EmployeeDemo   
   FROM HumanResources.Employee emp ;
   GO
   ```  
  
### <a name="examine-the-structure-and-data-of-the-employeedemo-table"></a>EmployeeDemo 테이블의 구조와 데이터 검사  
  
-   이 새 **EmployeeDemo** 테이블은 새 구조로 마이그레이션할 수 있는 기존 데이터베이스의 일반적인 테이블을 나타냅니다. 쿼리 편집기 창에서 다음 코드를 실행하여 테이블이 자체 조인을 통해 직원/관리자 관계를 나타내는 방법을 표시합니다.  
  
    ```sql  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL                    1   adventure-works\ken0        Chief Executive Officer
    1   adventure-works\ken0        2   adventure-works\terri0      Vice President of Engineering
    1   adventure-works\ken0       16   adventure-works\david0    Marketing Manager
    1   adventure-works\ken0       25   adventure-works\james1    Vice President of Production
    1   adventure-works\ken0      234   adventure-works\laura1    Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0       Information Services Manager
    1   adventure-works\ken0      273   adventure-works\brian3    Vice President of Sales
    2   adventure-works\terri0    3 adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0        Senior Tool Designer
    ...  
    ```  
  
    결과로 총 290개의 행이 나타납니다.  
  
**ORDER BY** 절로 인해 출력에 각 관리자 수준의 직접 보고가 함께 나열되었습니다. 예를 들어 **MgrID** 1(ken0)의 모든 직접 보고 7개가 서로 인접하게 나열됩니다. 불가능하지는 않지만 **MgrID** 1에게 결과적으로 보고하게 되는 모든 직원을 그룹화하기는 훨씬 더 어렵습니다.  


## <a name="populate-a-table-with-existing-hierarchical-data"></a>기존 계층적 데이터로 테이블 채우기
이 태스크에서는 새 테이블을 만들고 이를 **EmployeeDemo** 테이블의 데이터로 채웁니다. 이 태스크의 단계는 다음과 같습니다.  
  
-   **hierarchyid** 열이 포함된 새 테이블을 만듭니다. 이 열로 기존 **EmployeeID** 및 **ManagerID** 열을 대체할 수도 있지만 여기서는 해당 열을 유지합니다. 이는 기존 애플리케이션에서 해당 열을 참조할 수 있으며 해당 열을 유지하는 것이 전송 후에 데이터를 이해하는 데 도움이 되기 때문입니다. 테이블 정의에서 **OrgNode** 를 기본 키로 지정하므로 해당 열에 고유 값을 포함해야 합니다. **OrgNode** 열의 클러스터형 인덱스는 **OrgNode** 시퀀스의 날짜를 저장합니다.    
-   각 관리자에게 직접 보고하는 직원 수를 추적하는 데 사용되는 임시 테이블을 만듭니다. 
-   **EmployeeDemo** 테이블의 데이터를 사용하여 새 테이블을 채웁니다.  
  
### <a name="to-create-a-new-table-named-neworg"></a>NewOrg라는 새 테이블을 만들려면  
  
-   쿼리 편집기 창에서 다음 코드를 실행하여 **HumanResources.NewOrg**라는 새 테이블을 만듭니다.  
  
    ```sql   
    CREATE TABLE HumanResources.NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="create-a-temporary-table-named-children"></a>#Children이라는 임시 테이블 만들기  
  
1.  각 노드의 자식 수를 포함할 **Num** 열이 포함된 **#Children** 이라는 임시 테이블을 만듭니다.  
  
    ```sql  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  **NewOrg** 테이블을 채우는 쿼리의 속도를 상당히 높일 인덱스를 추가합니다.  
  
    ```sql  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="populate-the-neworg-table"></a>NewOrg 테이블 채우기  
  
1.  재귀 쿼리는 집계가 있는 하위 쿼리를 금지합니다. 대신 **ROW_NUMBER()** 메서드를 통해 [Num](../../t-sql/functions/row-number-transact-sql.md) 열을 채우는 다음 코드를 사용하여 **#Children** 테이블을 채웁니다.  
  
    ```sql 
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM HumanResources.EmployeeDemo  
    GO 
    ```  
  
2.  **#Children** 테이블을 검토합니다. **Num** 열에 각 관리자에 대한 일련 번호가 포함되는 방식을 확인합니다.  
  
    ```sql  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

    ```
    EmployeeID  ManagerID   Num
    1   NULL    1
    2        1    1
    16     1      2
    25     1      3
    234    1      4
    263    1      5
    273    1      6
    3        2    1
    4        3    1
    5        3    2
    6        3    3
    7        3    4
    ```


3.  **NewOrg** 테이블을 채웁니다. GetRoot 및 ToString 메서드를 사용하여 **Num** 값을 **hierarchyid** 형식에 연결한 다음 **OrgNode** 열을 결과 계층 값으로 업데이트합니다.  
  
    ```sql  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   

    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT HumanResources.NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM HumanResources.EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO 
    ```  
  
4.  **hierarchyid** 열을 문자 형식으로 변환하면 이해하기가 더 쉬워집니다. **OrgNode** 열의 두 가지 표현이 포함된 다음 코드를 실행하여 **NewOrg** 테이블의 데이터를 검토합니다.  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM HumanResources.NewOrg   
    ORDER BY LogicalNode;  
    GO  
    ```  
  
    **LogicalNode** 열은 계층을 나타내는 보다 읽기 쉬운 텍스트 형식으로 **hierarchyid** 열을 변환합니다. 나머지 태스크에서는 `ToString()` 메서드를 사용하여 **hierarchyid** 열의 논리 형식을 표시합니다.  
  
5.  더 이상 필요하지 않은 임시 테이블을 삭제합니다.  
  
    ```sql  
    DROP TABLE #Children  
    GO  
    ```  
  
## <a name="optimizing-the-neworg-table"></a>NewOrg 테이블 최적화
[기존 계층적 데이터로 테이블 채우기](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) 태스크에서 만든 **NewOrd** 테이블은 모든 직원 정보를 포함하며 **hierarchyid** 데이터 형식을 사용하여 계층 구조를 나타냅니다. 이 태스크에서는 새 인덱스를 추가하여 **hierarchyid** 열의 검색을 지원합니다.  
  

**hierarchyid** 열(**OrgNode**)은 **NewOrg** 테이블의 기본 키입니다. 테이블을 만들 때 **OrgNode** 열의 고유성을 적용하기 위해 이 열에 **PK_NewOrg_OrgNode** 라는 클러스터형 인덱스가 포함되었습니다. 이 클러스터형 인덱스는 테이블의 깊이 우선 검색도 지원합니다.  
  
  
### <a name="create-index-on-neworg-table-for-efficient-searches"></a>효율적인 검색을 위해 NewOrg 테이블에 인덱스 만들기  
  
1.  계층의 같은 수준에서의 쿼리를 돕기 위해 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 메서드를 사용하여 계층의 수준을 포함하는 계산 열을 만듭니다. 그런 다음 수준 및 **Hierarchyid**에 대한 복합 인덱스를 만듭니다. 다음 코드를 실행하여 계산 열과 너비 우선 인덱스를 만듭니다.  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  **EmployeeID** 열에 대한 고유 인덱스를 만듭니다. 이는 **EmployeeID** 번호를 기준으로 단일 직원을 단일 조회하는 일반적인 방법입니다. 다음 코드를 실행하여 **EmployeeID**에 대한 인덱스를 만듭니다.  
  
    ```sql  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  다음 코드를 실행하여 3가지 인덱스 각각의 순서대로 테이블에서 데이터를 검색합니다.  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  결과 집합을 비교하여 각 인덱스 유형에서 순서가 저장되는 방법을 확인합니다. 각 출력의 처음 4개 행만 표시됩니다.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    깊이 우선 인덱스: 직원 레코드가 해당 관리자에 인접하게 저장됩니다.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    **EmployeeID** 우선 인덱스: 행이 **EmployeeID** 시퀀스에 저장됩니다.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> 깊이 우선 인덱스와 너비 우선 인덱스의 차이를 보여 주는 다이어그램은 [계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)를 참조하세요.  
  
### <a name="drop-the-unnecessary-columns"></a>불필요한 열 삭제  
  
1.  **ManagerID** 열은 직원/관리자 관계를 나타냅니다(이제 **OrgNode** 열이 나타냄). 다른 애플리케이션에 **ManagerID** 열이 필요하지 않은 경우 다음 문을 사용하여 해당 열을 삭제하는 것이 좋습니다.  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  **EmployeeID** 열도 중복됩니다. **OrgNode** 열은 각 직원을 고유하게 식별합니다. 다른 애플리케이션에 **EmployeeID** 열이 필요하지 않은 경우 다음 코드를 사용하여 인덱스와 열을 차례로 삭제하는 것이 좋습니다.  
  
    ```sql  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
### <a name="replace-the-original-table-with-the-new-table"></a>원래 테이블을 새 테이블로 바꾸기  
  
1.  원래 테이블에 추가 인덱스 또는 제약 조건이 포함된 경우 이를 **NewOrg** 테이블에 추가합니다.  
  
2.  이전 **EmployeeDemo** 테이블을 새 테이블로 바꿉니다. 다음 코드를 실행하여 이전 테이블을 삭제한 다음 새 테이블의 이름을 이전 이름으로 바꿉니다.  
  
    ```sql  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  다음 코드를 실행하여 최종 테이블을 검사합니다.  
  
    ```sql  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-steps"></a>다음 단계
다음 문서에서는 계층적 테이블에서 데이터를 만들고 관리하는 방법을 설명합니다. 

자세히 알아보려면 다음 문서로 이동합니다.
> [!div class="nextstepaction"]
> [다음 단계](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)
