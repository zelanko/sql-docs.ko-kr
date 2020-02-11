---
title: NewOrg 테이블 최적화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 952043d5d001fe4fe65e6dd1aa7bb2001290429e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110067"
---
# <a name="optimizing-the-neworg-table"></a>NewOrg 테이블 최적화
  [기존 계층적 데이터로 테이블 채우기](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) 태스크에서 만든 `hierarchyid` **neword** 테이블은 모든 직원 정보를 포함 하며 데이터 형식을 사용 하 여 계층 구조를 나타냅니다. 이 태스크에서는 새 인덱스를 추가하여 `hierarchyid` 열에서의 검색을 지원합니다.  
  
## <a name="clustered-index"></a>클러스터형 인덱스  
 `hierarchyid` 열 (**OrgNode**)은 **neworg** 테이블의 기본 키입니다. 테이블을 만들 때 **OrgNode** 열의 고유성을 적용하기 위해 이 열에 **PK_NewOrg_OrgNode** 라는 클러스터형 인덱스가 포함되었습니다. 이 클러스터형 인덱스는 테이블의 깊이 우선 검색도 지원합니다.  
  
## <a name="nonclustered-index"></a>비클러스터형 인덱스  
 이 단계에서는 일반적인 검색을 지원하는 두 개의 비클러스터형 인덱스를 만듭니다.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>효율적인 검색을 위해 NewOrg 테이블을 인덱싱하려면  
  
1.  계층의 같은 수준에서의 쿼리를 돕기 위해 [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) 메서드를 사용하여 계층의 수준을 포함하는 계산 열을 만듭니다. 그런 다음 수준 및 `Hierarchyid`에 대한 복합 인덱스를 만듭니다. 다음 코드를 실행하여 계산 열과 너비 우선 인덱스를 만듭니다.  
  
    ```  
    ALTER TABLE NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  
  **EmployeeID** 열에 대한 고유 인덱스를 만듭니다. 이는 **EmployeeID** 번호를 기준으로 단일 직원을 단일 조회하는 일반적인 방법입니다. 다음 코드를 실행하여 **EmployeeID**에 대한 인덱스를 만듭니다.  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON NewOrg(EmployeeID) ;  
    GO  
    ```  
  
3.  다음 코드를 실행하여 3가지 인덱스 각각의 순서대로 테이블에서 데이터를 검색합니다.  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM NewOrg   
    ORDER BY OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY H_Level, OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  결과 집합을 비교하여 각 인덱스 유형에서 순서가 저장되는 방법을 확인합니다. 각 출력의 처음 4개 행만 표시됩니다.  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     깊이 우선 인덱스: 직원 레코드가 해당 관리자에 인접하게 저장됩니다.  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     **Employeeid**-첫 번째 인덱스: 행이 **EmployeeID** 시퀀스에 저장 됩니다.  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
> [!NOTE]  
>  깊이 우선 인덱스와 너비 우선 인덱스의 차이를 보여 주는 다이어그램은 [계층적 데이터&#40;SQL Server&#41;](../hierarchical-data-sql-server.md)를 참조하세요.  
  
#### <a name="to-drop-the-unnecessary-columns"></a>불필요한 열을 삭제하려면  
  
1.  
  **ManagerID** 열은 직원/관리자 관계를 나타냅니다(이제 **OrgNode** 열이 나타냄). 다른 애플리케이션에 **ManagerID** 열이 필요하지 않은 경우 다음 문을 사용하여 해당 열을 삭제하는 것이 좋습니다.  
  
    ```  
    ALTER TABLE NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  
  **EmployeeID** 열도 중복됩니다. 
  **OrgNode** 열은 각 직원을 고유하게 식별합니다. 다른 애플리케이션에 **EmployeeID** 열이 필요하지 않은 경우 다음 코드를 사용하여 인덱스와 열을 차례로 삭제하는 것이 좋습니다.  
  
    ```  
    DROP INDEX EmpIDs_unq ON NewOrg ;  
    ALTER TABLE NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>원래 테이블을 새 테이블로 바꾸려면  
  
1.  원래 테이블에 추가 인덱스 또는 제약 조건이 포함된 경우 이를 **NewOrg** 테이블에 추가합니다.  
  
2.  이전 **EmployeeDemo** 테이블을 새 테이블로 바꿉니다. 다음 코드를 실행하여 이전 테이블을 삭제한 다음 새 테이블의 이름을 이전 이름으로 바꿉니다.  
  
    ```  
    DROP TABLE EmployeeDemo ;  
    GO  
    sp_rename 'NewOrg', EmployeeDemo ;  
    GO  
    ```  
  
3.  다음 코드를 실행하여 최종 테이블을 검사합니다.  
  
    ```  
    SELECT * FROM EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [요약: 테이블을 계층 구조로 변환](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
