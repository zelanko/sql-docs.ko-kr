---
title: "GetDescendant (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ced4a5518ce7d58785a1d2954c4f131b66a5ddb0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="getdescendant-database-engine"></a>GetDescendant(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

부모의 자식 노드를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>인수  
*child1*  
NULL 또는 **hierarchyid** 현재 노드의 자식입니다.
  
*자식 2*  
NULL 또는 **hierarchyid** 현재 노드의 자식입니다.
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: hierarchyid**
  
**CLR 반환 형식: SqlHierarchyId**
  
## <a name="remarks"></a>주의  
부모의 하위 항목인 자식 노드 하나를 반환합니다.
-   parent가 NULL인 경우 NULL을 반환합니다.  
-   parent가 NULL이 아니고 child1과 child2가 모두 NULL인 경우 부모의 자식을 반환합니다.  
-   parent와 child1이 NULL이 아니고 child2가 NULL인 경우 child1보다 큰 부모의 자식을 반환합니다.  
-   parent와 child2가 NULL이 아니고 child1이 NULL인 경우 child2보다 작은 부모의 자식을 반환합니다.  
-   parent, child1 및 child2가 NULL이 아닌 경우 <codeInline>GetDescendant</codeInline>는 child1보다 크고 child2보다 작은 부모의 자식을 반환합니다.  
-   child1이 NULL도 아니고 부모의 자식도 아닌 경우 예외가 발생합니다.  
-   child2가 NULL도 아니고 부모의 자식도 아닌 경우 예외가 발생합니다.  
-   child1이 child2보가 크거나 같으면 예외가 발생합니다.  
  
GetDescendant는 결정적입니다. 따라서 동일한 입력을 GetDescendant를 호출 하면 동일한 출력이 생성 항상 됩니다. 그러나 생성되는 자식의 정확한 ID는 예 3에 표시된 대로 다른 노드와의 관계에 따라 달라질 수 있습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>1. 행을 가장 작은 항목 노드로 삽입  
노드 `/3/1/`에 있는 기존 직원에게 보고하는 새 직원을 고용합니다. 으로 새 행 노드를 지정 하려면 인수 없이 GetDescendant 메서드를 사용 하 여 새 행을 삽입 하려면 다음 코드를 실행 `/3/1/1/`:
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>2. 행을 큰 하위 항목 노드로 삽입  
다른 새 직원을 고용, 자식 1 인수를 사용 하 여 되도록 지정 하려면 GetDescendant 메서드를 사용 하 여 새 행을 삽입 하는 다음 코드는 새 행의 노드가 A. 실행 예제와 같이 동일한 관리자에 게 보고 예 A 될 예정 되 고 `/3/1/2/`:
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>3. 행을 기존의 두 노드 사이에 삽입  
예 1과 같은 관리자에 보고 하는 세 번째 직원을 고용 보다 큰 노드에 새 행을 삽입 하는이 예제는 `FirstNewEmployee` 예에서 및 보다 작은 `SecondNewEmployee` GetDescendant 메서드를 사용 하 여 다음 코드 예제 B. 실행 합니다. child1 인수와 child2 인수를 모두 사용하여 새 행의 노드가 노드 `/3/1/1.1/`이 되도록 지정합니다.
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
테이블에 추가 하는 노드 A, B 및 C 예제를 완료 한 후 다음과 피어가 됩니다 **hierarchyid** 값:
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
노드 `/3/1/1.1/`은 노드 `/3/1/1/`보다 크지만 같은 계층 수준에 있습니다.
  
### <a name="d-scalar-examples"></a>4. 스칼라 예  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]임의 삽입 및 삭제의 지원 **hierarchyid** 노드. GetDescendant()를 사용 하 여 항상 이므로 두 사이 노드를 생성할 수 **hierarchyid** 노드. 다음 코드에서는 `GetDescendant`를 사용하여 예제 노드를 생성합니다.
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>5. CLR 예  
다음 코드 조각에서는 `GetDescendant()` 메서드를 호출합니다.
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

