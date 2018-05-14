---
title: IsDescendantOf(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 679f75007cc60521f569a42a5c580f8553b61eca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

*this*가 부모의 하위 항목인 경우 true를 반환합니다.
  
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
*parent*  
IsDescendantOf 테스트를 수행해야 하는 **hierarchyid** 노드입니다.
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: bit**
  
**CLR 반환 형식: SqlBoolean**
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목:
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
