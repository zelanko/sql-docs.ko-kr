---
title: "기존 계층적 데이터로 테이블 채우기 | Microsoft 문서"
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
helpviewer_keywords: HierarchyID
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 25feafb61615372739cc6997666cee5841424bb9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-1-2---populating-a-table-with-existing-hierarchical-data"></a>1-2단원 - 기존 계층적 데이터로 테이블 채우기
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] 이 태스크에서는 새 테이블을 만들고 이를 **EmployeeDemo** 테이블의 데이터로 채웁니다. 이 태스크의 단계는 다음과 같습니다.  
  
-   **hierarchyid** 열이 포함된 새 테이블을 만듭니다. 이 열로 기존 **EmployeeID** 및 **ManagerID** 열을 대체할 수도 있지만 여기서는 해당 열을 유지합니다. 이는 기존 응용 프로그램에서 해당 열을 참조할 수 있으며 해당 열을 유지하는 것이 전송 후에 데이터를 이해하는 데 도움이 되기 때문입니다. 테이블 정의에서 **OrgNode** 를 기본 키로 지정하므로 해당 열에 고유 값을 포함해야 합니다. **OrgNode** 열의 클러스터형 인덱스는 **OrgNode** 시퀀스의 날짜를 저장합니다.  
  
-   각 관리자에게 직접 보고하는 직원 수를 추적하는 데 사용되는 임시 테이블을 만듭니다.  
  
-   **EmployeeDemo** 테이블의 데이터를 사용하여 새 테이블을 채웁니다.  
  
### <a name="to-create-a-new-table-named-neworg"></a>NewOrg라는 새 테이블을 만들려면  
  
-   쿼리 편집기 창에서 다음 코드를 실행하여 **HumanResources.NewOrg**라는 새 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE NewOrg  
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
  
### <a name="to-create-a-temporary-table-named-children"></a>#Children이라는 임시 테이블을 만들려면  
  
1.  각 노드의 자식 수를 포함할 **Num** 열이 포함된 **#Children** 이라는 임시 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  **NewOrg** 테이블을 채우는 쿼리의 속도를 상당히 높일 인덱스를 추가합니다.  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>NewOrg 테이블을 채우려면  
  
1.  재귀 쿼리는 집계가 있는 하위 쿼리를 금지합니다. 대신 **ROW_NUMBER()** 메서드를 통해 [Num](../../t-sql/functions/row-number-transact-sql.md) 열을 채우는 다음 코드를 사용하여 **#Children** 테이블을 채웁니다.  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  **#Children** 테이블을 검토합니다. **Num** 열에 각 관리자에 대한 일련 번호가 포함되는 방식을 확인합니다.  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    `EmployeeID ManagerID Num`  
  
    `---------- --------- ---`  
  
    `1        NULL       1`  
  
    `2         1         1`  
  
    `3         1         2`  
  
    `4         2         1`  
  
    `5         2         2`  
  
    `6         2         3`  
  
    `7         3         1`  
  
    `8         3         2`  
  
    `9         4         1`  
  
    `10        4         2`  
  
3.  **NewOrg** 테이블을 채웁니다. GetRoot 및 ToString 메서드를 사용하여 **Num** 값을 **hierarchyid** 형식에 연결한 다음 **OrgNode** 열을 결과 계층 값으로 업데이트합니다.  
  
    ```  
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
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  **hierarchyid** 열을 문자 형식으로 변환하면 이해하기가 더 쉬워집니다. **OrgNode** 열의 두 가지 표현이 포함된 다음 코드를 실행하여 **NewOrg** 테이블의 데이터를 검토합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
    **LogicalNode** 열은 계층을 나타내는 보다 읽기 쉬운 텍스트 형식으로 **hierarchyid** 열을 변환합니다. 나머지 태스크에서는 `ToString()` 메서드를 사용하여 **hierarchyid** 열의 논리 형식을 표시합니다.  
  
5.  더 이상 필요하지 않은 임시 테이블을 삭제합니다.  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
다음 태스크에서는 계층 구조를 지원하는 인덱스를 만듭니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[NewOrg 테이블 최적화](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
  
  
