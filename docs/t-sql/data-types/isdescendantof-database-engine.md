---
title: "IsDescendantOf (데이터베이스 엔진) | Microsoft Docs"
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
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f8ff83344e577e5479e21316a3c043d6ef4f702
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이면 true를 반환 *이* 가 부모의 하위 항목인 합니다.
  
## <a name="syntax"></a>구문  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>인수  
*부모*  
**hierarchyid** IsDescendantOf 테스트를 수행 해야 하는 노드.
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: 비트**
  
**CLR 반환 형식: SqlBoolean**
  
## <a name="remarks"></a>주의  
부모에서 시작하는 하위 트리의 모든 노드에 대해서는 true를 반환하고 다른 모든 노드에 대해서는 false를 반환합니다.
  
부모는 자신의 하위 항목으로 간주됩니다.
  
## <a name="examples"></a>예  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>1. WHERE 절에서 IsDescendantOf 사용  
다음 예에서는 관리자와 관리자에게 보고하는 직원을 반환합니다.
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>2. IsDescendantOf를 사용하여 관계 평가  
다음 코드는 세 개의 변수를 선언하고 채웁니다. 그런 다음 계층 관계를 평가하고 비교를 기반으로 두 개의 출력된 결과 중 하나를 반환합니다.
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>3. 공용 언어 런타임 메서드 호출  
다음 코드 조각은 `IsDescendantOf()` 메서드를 호출합니다.
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

