---
title: Parse(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 00464f88444957c52d4671e143c6e3b425770ed6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052939"
---
# <a name="parse-database-engine"></a>Parse(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Parse는 **hierarchyid**의 정식 문자열 표현을 **hierarchyid** 값으로 변환합니다. Parse는 문자열 형식에서 **hierarchyid**로 변환될 때 암시적으로 호출됩니다. [ToString](../../t-sql/data-types/tostring-database-engine.md)과 반대로 작동합니다. Parse()는 정적 메서드입니다.
  
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
*input*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: 변환되는 문자 데이터 형식 값입니다.
  
CLR: 평가되는 문자열 값입니다.
  
## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: hierarchyid**
  
**CLR 반환 형식: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Parse가 **hierarchyid**의 유효한 문자열 표현이 아닌 값을 수신하면 예외가 발생합니다. 예를 들어 **char** 데이터 형식에 후행 공백이 포함되어 있으면 예외가 발생합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>1. 테이블이 없는 Transact-SQL 값 변환  
다음 코드 예에서는 `ToString`을 사용하여 **hierarchyid** 값을 문자열로 변환하고 `Parse`를 사용하여 문자열 값을 **hierarchyid**로 변환합니다.
  
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
다음 코드 조각에서는 Parse() 메서드를 호출합니다.
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>관련 항목:
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
