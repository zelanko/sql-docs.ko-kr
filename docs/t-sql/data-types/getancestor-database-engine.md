---
title: GetAncestor(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetAncestor_TSQL
- GetAncestor
dev_langs:
- TSQL
helpviewer_keywords:
- GetAncestor [Database Engine]
ms.assetid: b96a986f-d5e4-4034-8013-de7974594ee9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1c4f082b427aaafb8b93aff7f3247859a92a3b62
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738225"
---
# <a name="getancestor-database-engine"></a>GetAncestor(데이터베이스 엔진)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

*this*의 *n*번째 상위 항목을 나타내는 **hierarchyid**를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```sql
-- Transact-SQL syntax  
child.GetAncestor ( n )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetAncestor ( int n )  
```  
  
## <a name="arguments"></a>인수  
*n*  
계층에서 위로 이동할 수준 수를 나타내는 **int**입니다.
  
## <a name="return-types"></a>반환 형식
**SQL Server 반환 형식: hierarchyid**
  
**CLR 반환 형식: SqlHierarchyId**
  
## <a name="remarks"></a>설명  
출력의 각 노드가 현재 노드를 지정된 수준의 상위 항목으로 갖는지 여부를 테스트하는 데 사용됩니다.
  
[GetLevel()](../../t-sql/data-types/getlevel-database-engine.md)보다 큰 숫자가 전달되면 NULL이 반환됩니다.
  
음수가 전달되면 예외가 발생합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-finding-the-child-nodes-of-a-parent"></a>A. 부모의 자식 노드 찾기  
`GetAncestor(1)`는 `david0`을 직계 상위 항목(부모)으로 갖는 직원을 반환합니다. 다음 예에서는 `GetAncestor(1)`를 사용합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(1) = @CurrentEmployee ;  
```  
  
### <a name="b-returning-the-grandchildren-of-a-parent"></a>B. 부모의 손자 반환  
`GetAncestor(2)`는 계층에서 현재 노드보다 두 수준 낮은 직원을 반환합니다. 이러한 직원은 현재 노드의 손자입니다. 다음 예에서는 `GetAncestor(2)`를 사용합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\ken0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(2) = @CurrentEmployee ;  
```  
  
### <a name="c-returning-the-current-row"></a>C. 현재 행 반환  
`GetAncestor(0)`를 사용하여 현재 노드를 반환하려면 다음 코드를 실행합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(0) = @CurrentEmployee ;  
```  
  
### <a name="d-returning-a-hierarchy-level-if-a-table-isnt-present"></a>D. 테이블이 없는 경우 계층 수준 반환  
`GetAncestor`는 테이블이 없는 경우에도 계층에서 선택한 수준을 반환합니다. 예를 들어 다음 코드는 현재 직원을 지정하고 테이블에 대한 참조 없이 현재 직원의 상위 항목 `hierarchyid`를 반환합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid ;  
DECLARE @TargetEmployee hierarchyid ;  
SELECT @CurrentEmployee = '/2/3/1.2/5/3/' ;  
SELECT @TargetEmployee = @CurrentEmployee.GetAncestor(2) ;  
SELECT @TargetEmployee.ToString(), @TargetEmployee ;  
```  
  
### <a name="e-calling-a-common-language-runtime-method"></a>E. 공용 언어 런타임 메서드 호출  
다음 코드 조각은 `GetAncestor()` 메서드를 호출합니다.
  
```sql
this.GetAncestor(1)  
```  
  
## <a name="see-also"></a>참고 항목
[IsDescendantOf&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/isdescendantof-database-engine.md)  
[hierarchyid 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  