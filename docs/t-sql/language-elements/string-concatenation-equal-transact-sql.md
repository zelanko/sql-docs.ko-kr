---
title: "+ = (문자열 연결) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c557bcc1d3c2f314ce57e93701b11833f5a6fc6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="string-concatenation---equal-transact-sql"></a>문자열 연결-같음 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 문자열을 연결하고 문자열을 연산 결과로 설정합니다. 예를 들어 변수 @x 다음 'Adventure' equals @x 의 원래 값을 사용 하는 + = 'Works' @x, 'Works' 문자열에 추가 하 고 설정 @x 를 새 값 'AdventureWorks'.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자 데이터 형식 중 하나입니다.  
  
## <a name="result-types"></a>결과 형식  
 변수에 정의된 데이터 형식을 반환합니다.  
  
## <a name="remarks"></a>주의  
 설정 @v1 + = 'expression' 집합과 같습니다 @v1 = @v1 + ('expression'). 또한 설정 @v1 = @v2 + @v3 + @v4 집합과 같습니다 @v1 = (@v2 + @v3) + @v4합니다.  
  
 += 연산자는 변수 없이 사용할 수 없습니다. 예를 들어 다음 코드를 실행하면 오류가 발생합니다.  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>예  
### <a name="a-concatenation-using--operator"></a>1. + = 연산자를 사용 하 여 연결
 다음 예에서는 `+=` 연산자를 사용하여 문자열을 연결합니다.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>2. + = 연산자를 사용 하 여 연결 하는 동안 계산 순서
다음 예제에서는 여러 문자열을 하나의 긴 문자열로 연결 하 고 최종 문자열의 길이 계산 하려고 합니다. 이 예제에서는 연결 연산자를 사용 하는 동안 평가 순서 및 잘림 규칙을 보여 줍니다. 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>관련 항목:  
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+ = &#40; 추가 EQUALS &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40; 문자열 연결 &#41; &#40; Transact SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  

