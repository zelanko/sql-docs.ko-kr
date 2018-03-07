---
title: "선택 @local_variable (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 44fd55346e8a4a27f1d3301d6cb3c6bdf7bdf548
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="select-localvariable-transact-sql"></a>선택 @local_variable (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  식의 값을 지역 변수를 설정합니다.  
  
 변수 할당에 사용 하는 권장 [설정 @local_variable ](../../t-sql/language-elements/set-local-variable-transact-sql.md) @ 선택 하는 대신*local_variable*합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>인수  
@*local_variable*  
 값을 할당할 선언된 변수입니다.  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
오른쪽의 값을 왼쪽의 변수에 할당합니다.  
  
복합 할당 연산자:  
  |적용한 후 |action |   
  |-----|-----|  
  | = | 이어지는 식을를 변수에 할당 합니다. |  
  | += | 추가 및 할당 |   
  | -= | 빼기 및 할당 |  
  | \*= | 곱하기 및 할당 |  
  | /= | 나누기 및 할당 |  
  | %= | 모듈로 및 할당 |  
  | &= | 비트 AND 및 할당 |  
  | ^= | 비트 XOR 및 할당 |  
  | \|= | 비트 OR 및 할당 |  
  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다. 여기에는 스칼라 하위 쿼리가 포함됩니다.  
  
## <a name="remarks"></a>주의  
 SELECT @*local_variable* 변수에는 단일 값을 반환 하려면 일반적으로 사용 됩니다. 그러나 때 *식* 이름인 여러 값 열을 반환할 수 있습니다. SELECT 문에서 둘 이상의 값을 반환하면 반환된 값 중 마지막 값이 변수에 할당됩니다.  
  
 SELECT 문에서 행을 반환하지 않으면 변수는 현재 값을 그대로 유지합니다. 경우 *식* 스칼라 변수 값은 NULL로 설정 하는 반환 하위 쿼리일 됩니다.  
  
 하나의 SELECT 문으로 여러 개의 지역 변수를 초기화할 수 있습니다.  
  
> [!NOTE]  
>  변수 할당이 포함된 SELECT 문을 일반 결과 집합 검색 작업을 수행하는 데 사용할 수는 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>1. SELECT를 사용 하 여 @local_variable 단일 값을 반환 하려면  
 다음 예에서는 `@var1` 변수에 `Generic Name` 값이 할당됩니다. `Store`에 지정된 값이 테이블에 없기 때문에 `CustomerID` 테이블에 대한 쿼리에서 행을 반환하지 않습니다. 따라서 변수는 `Generic Name` 값을 유지합니다.  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>2. SELECT를 사용 하 여 @local_variable null을 반환  
 다음 예에서는 `@var1`에 값을 할당하기 위해 하위 쿼리가 사용됩니다. `CustomerID`에 대해 요청한 값이 없기 때문에 하위 쿼리에서 값을 반환하지 않고 변수가 `NULL`로 설정됩니다.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>관련 항목  
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT &#40;TRANSACT-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
