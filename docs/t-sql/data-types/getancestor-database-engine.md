---
title: "GetAncestor (데이터베이스 엔진) | Microsoft Docs"
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
- GetAncestor_TSQL
- GetAncestor
dev_langs:
- TSQL
helpviewer_keywords:
- GetAncestor [Database Engine]
ms.assetid: b96a986f-d5e4-4034-8013-de7974594ee9
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7649b3290175787b293ea1b720bb299ead89971
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="getancestor-database-engine"></a>GetAncestor(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

반환 된 **hierarchyid** 나타내는  *n* 번째 상위 항목을 *이*합니다.
  
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
**int**, 계층 구조에서 위로 이동할 수준 수를 나타내는입니다.
  
## <a name="return-types"></a>반환 형식
**SQL Server 반환 형식: hierarchyid**
  
**CLR 반환 형식: SqlHierarchyId**
  
## <a name="remarks"></a>주의  
출력의 각 노드가 현재 노드를 지정된 수준의 상위 항목으로 갖는지 여부를 테스트하는 데 사용됩니다.
  
보다 큰 숫자가 [getlevel ()](../../t-sql/data-types/getlevel-database-engine.md) 가 전달, NULL이 반환 됩니다.
  
음수가 전달되면 예외가 발생합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-finding-the-child-nodes-of-a-parent"></a>1. 부모의 자식 노드 찾기  
`GetAncestor(1)`는 `david0`을 직계 상위 항목(부모)으로 갖는 직원을 반환합니다. 다음 예에서는 `GetAncestor(1)`를 사용합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(1) = @CurrentEmployee ;  
```  
  
### <a name="b-returning-the-grandchildren-of-a-parent"></a>2. 부모의 손자 반환  
`GetAncestor(2)`는 계층에서 현재 노드보다 두 수준 낮은 직원을 반환합니다. 이러한 항목은 현재 노드의 손자입니다. 다음 예에서는 `GetAncestor(2)`를 사용합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\ken0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(2) = @CurrentEmployee ;  
```  
  
### <a name="c-returning-the-current-row"></a>3. 현재 행 반환  
사용 하 여 현재 노드를 반환할 `GetAncestor(0)`, 다음 코드를 실행 합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid  
SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\david0'  
  
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetAncestor(0) = @CurrentEmployee ;  
```  
  
### <a name="d-returning-a-hierarchy-level-if-a-table-is-not-present"></a>4. 테이블이 없는 경우 계층 수준 반환  
`GetAncestor`는 테이블이 없는 경우에도 계층에서 선택한 수준을 반환합니다. 예를 들어 다음 코드에서는 현재 직원을 지정 하 고 반환 된 `hierarchyid` 테이블을 참조 하지 않고 현재 직원의 상위 항목의 합니다.
  
```sql
DECLARE @CurrentEmployee hierarchyid ;  
DECLARE @TargetEmployee hierarchyid ;  
SELECT @CurrentEmployee = '/2/3/1.2/5/3/' ;  
SELECT @TargetEmployee = @CurrentEmployee.GetAncestor(2) ;  
SELECT @TargetEmployee.ToString(), @TargetEmployee ;  
```  
  
### <a name="e-calling-a-common-language-runtime-method"></a>5. 공용 언어 런타임 메서드 호출  
다음 코드 조각은 `GetAncestor()` 메서드를 호출합니다.
  
```sql
this.GetAncestor(1)  
```  
  
## <a name="see-also"></a>참고 항목
[IsDescendantOf &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/isdescendantof-database-engine.md)  
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

