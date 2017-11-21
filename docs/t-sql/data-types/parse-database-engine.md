---
title: "Parse (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 027940c7575f3c7901cd8668879064ff375d9986
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="parse-database-engine"></a>Parse(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

구문 분석의 정식 문자열 표현을 **hierarchyid** 에 **hierarchyid** 값입니다. 구문 분석 하는 문자열 형식에서 변환 될 때 암시적으로 호출 됩니다 **hierarchyid** 발생 합니다. 역할의 반대를 [ToString](../../t-sql/data-types/tostring-database-engine.md)합니다. Parse ()는 정적 메서드입니다.
  
## <a name="syntax"></a>구문  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>인수  
*입력*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: 변환되는 문자 데이터 형식 값입니다.
  
CLR: 평가 되는 문자열 값입니다.
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: hierarchyid**
  
**CLR 반환 형식: SqlHierarchyId**
  
## <a name="remarks"></a>주의  
구문 분석의 유효한 문자열 표현을 하지 않은 값을 수신 하는 경우는 **hierarchyid**, 예외가 발생 합니다. 예를 들어 경우 **char** 데이터 형식에 후행 공백이, 예외가 발생 합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>1. 테이블이 없는 Transact-SQL 값 변환  
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
  
### <a name="b-clr-example"></a>2. CLR 예  
다음 코드 조각 parse () 메서드를 호출합니다.
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

