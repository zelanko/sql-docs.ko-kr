---
title: "GetLevel (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aac401d8fbe9546404f44f5fa2455f9e9c5dfe9d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="getlevel-database-engine"></a>GetLevel(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

노드의 깊이 나타내는 정수를 반환 *이* 트리에서 합니다.
  
## <a name="syntax"></a>구문  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: smallint**
  
**CLR 반환 형식: SqlInt16**
  
## <a name="remarks"></a>주의  
하나 이상의 노드 수준을 확인하거나 지정된 수준의 멤버로 노드를 필터링하는 데 사용됩니다. 계층의 루트는 수준 0입니다.
  
GetLevel 너비 우선 검색 인덱스에 대 한 매우 유용합니다. 자세한 내용은 참조 [계층적 데이터 &#40; SQL Server &#41; ](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>예  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>1. 계층 수준을 열로 반환  
다음 예의 텍스트 표현을 반환 된 **hierarchyid**, 및 다음 계층 구조 수준으로는 **EmpLevel** 테이블의 모든 행에 대 한 열:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>2. 계층 수준의 모든 멤버 반환  
다음 예에서는 계층 수준 2에 있는 테이블의 모든 행을 반환합니다.
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>3. 계층의 루트 반환  
다음 예에서는 계층 수준의 루트를 반환합니다.
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>4. CLR 예  
다음 코드 조각 getlevel () 메서드를 호출합니다.
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

