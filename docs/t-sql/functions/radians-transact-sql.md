---
title: RADIANS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RADIANS
- RADIANS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RADIANS function
ms.assetid: e9f69951-ecda-45d9-8909-dcb716b1b1c0
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6350b2f53082b4d671f3f8b54aa1f9d31a6235ef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="radians-transact-sql"></a>RADIANS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  숫자 식을 도 단위로 입력하면 라디안을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
RADIANS ( numeric_expression )  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 정확한 수치 또는 근사치 숫자 데이터 형식 범주에서를 제외 하 고는 **비트** 데이터 형식입니다.  
  
## <a name="return-types"></a>반환 형식  
 *numeric_expression*과 같은 유형을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-radians-to-show-00"></a>1. 0.0을 표시하기 위해 RADIANS 사용  
 다음 예에서는 라디안으로 변환하기 위한 숫자 식이 `0.0` 함수에 대해 너무 작기 때문에 `RADIANS`인 결과를 반환합니다.  
  
```  
SELECT RADIANS(1e-307)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------   
0.0                        
(1 row(s) affected)  
```  
  
### <a name="b-using-radians-to-return-the-equivalent-angle-of-a-float-expression"></a>2. float 식에서 같은 각도를 반환하기 위해 RADIANS 사용  
 다음 예에서는 `float` 식을 사용하고 지정한 각도의 `RADIANS`를 반환합니다.  
  
```  
-- First value is -45.01.  
DECLARE @angle float  
SET @angle = -45.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is -181.01.  
DECLARE @angle float  
SET @angle = -181.01  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.00.  
DECLARE @angle float  
SET @angle = 0.00  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
-- Next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The RADIANS of the angle is: ' +  
    CONVERT(varchar, RADIANS(@angle))  
GO  
-- Last value is 197.1099392.  
DECLARE @angle float  
SET @angle = 197.1099392  
SELECT 'The RADIANS of the angle is: ' +  
   CONVERT(varchar, RADIANS(@angle))  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------------------------------   
The RADIANS of the angle is: -0.785573                        
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: -3.15922                         
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0                                
(1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 0.00257041                       
 (1 row(s) affected)  
---------------------------------------   
The RADIANS of the angle is: 3.44022                          
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-radians-to-show-00"></a>3. 0.0을 표시하기 위해 RADIANS 사용  
 다음 예에서는 라디안으로 변환하기 위한 숫자 식이 `0.0` 함수에 대해 너무 작기 때문에 `RADIANS`인 결과를 반환합니다.  
  
```  
SELECT RADIANS(1e-307)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------   
0.0                        
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [decimal 및 numeric&#40; Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float 및 real &#40; Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int, bigint, smallint 및 tinyint &#40; Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [수치 연산 함수 &#40; Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [money 및 smallmoney &#40; Transact SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  


