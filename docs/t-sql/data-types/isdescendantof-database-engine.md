---
description: IsDescendantOf(데이터베이스 엔진)
title: IsDescendantOf(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b6d9d75083472b347a7cf78641aeb1bbe202dae2
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111268"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf(데이터베이스 엔진)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

*this*가 부모의 하위 항목인 경우 true를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```syntaxsql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*parent*  
IsDescendantOf 테스트를 수행해야 하는 **hierarchyid** 노드입니다.
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: bit**
  
**CLR 반환 형식: SqlBoolean**
  
## <a name="remarks"></a>설명  
부모에서 시작하는 하위 트리의 모든 노드에 대해서는 true를 반환하고 다른 모든 노드에 대해서는 false를 반환합니다.
  
부모는 자신의 하위 항목으로 간주됩니다.
  
## <a name="examples"></a>예제  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. WHERE 절에서 IsDescendantOf 사용  
다음 예에서는 관리자와 관리자에게 보고하는 직원을 반환합니다.
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. IsDescendantOf를 사용하여 관계 평가  
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
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. 공용 언어 런타임 메서드 호출  
다음 코드 조각은 `IsDescendantOf()` 메서드를 호출합니다.
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
