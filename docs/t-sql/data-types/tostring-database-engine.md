---
title: "ToString (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ToString
- ToString_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ToString [Database Engine]
ms.assetid: 5fc11ca5-c26d-4518-9512-67aa0270f110
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1544b27215083f8628696cebaaf14c53c628a9ba
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tostring-database-engine"></a>ToString(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

논리적으로 표현한 문자열을 반환 *이*합니다. ToString 변환 될 때 암시적으로 호출 됩니다 **hierarchyid** 문자열로 형식 발생 합니다. 역할의 반대를 [parse&#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/parse-database-engine.md)합니다.
  
## <a name="syntax"></a>구문  
  
```sql
-- Transact-SQL syntax  
node.ToString  ( )   
-- This is functionally equivalent to the following syntax  
-- which implicitly calls ToString():  
CAST(node AS nvarchar(4000))  
```  
  
```sql
-- CLR syntax  
string ToString  ( )   
```  
  
## <a name="return-types"></a>반환 형식
**SQL Server 반환 type:nvarchar(4000)**
  
**CLR 반환 형식: String**
  
## <a name="remarks"></a>주의  
계층의 논리적 위치를 반환합니다. 예를 들어 `/2/1/` 네 번째 행을 나타냅니다 ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 파일 시스템의 다음 계층 구조에서:
  
```sql
/        C:\  
/1/      C:\Database Files  
/2/      C:\Program Files  
/2/1/    C:\Program Files\Microsoft SQL Server  
/2/2/    C:\Program Files\Microsoft Visual Studio  
/3/      C:\Windows  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-transact-sql-example-in-a-table"></a>1. 테이블의 Transact-SQL 예  
다음 예제에서는 모두 반환는 `OrgNode` 둘 다로 열은 **hierarchyid** 데이터 형식 및 보다 읽기 쉬운 문자열 형식:
  
```sql
SELECT OrgNode,  
OrgNode.ToString() AS Node  
FROM HumanResources.EmployeeDemo  
ORDER BY OrgNode ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
OrgNode   Node  
0x        /  
0x58      /1/  
0x5AC0    /1/1/  
0x5B40    /1/2/  
0x5BC0    /1/3/  
0x5C20    /1/4/  
...  
```  
  
### <a name="b-converting-transact-sql-values-without-a-table"></a>2. 테이블이 없는 Transact-SQL 값 변환  
다음 코드 예제에서는 `ToString` 변환 하는 **hierarchyid** 값에 문자열 및 `Parse` 문자열 값을 변환 하는 **hierarchyid**합니다.
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="c-clr-example"></a>3. CLR 예  
다음 코드 조각 tostring () 메서드를 호출합니다.
  
```sql
this.ToString()  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

