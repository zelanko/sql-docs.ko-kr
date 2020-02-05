---
title: += 문자열 연결
description: 두 문자열을 연결하고 문자열을 연산 결과로 설정합니다.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd21fb221076470d0c39194ea4c38d96af0f1056
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75257049"
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+=(문자열 연결 대입)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 문자열을 연결하고 문자열을 연산 결과로 설정합니다. 예를 들어 @x 변수가 'Adventure'와 같으면 @x += 'Works'는 @x의 원래 값을 가져오고, 이 문자열에 'Works'를 추가하고, @x를 새 값('AdventureWorks')으로 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 임의의 문자 데이터 형식 중 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="result-types"></a>결과 형식  
 변수에 정의된 데이터 형식을 반환합니다.  
  
## <a name="remarks"></a>설명  
 SET @v1 += 'expression'은 SET @v1 = @v1 + ('expression')과 같습니다. 또한 SET @v1 = @v2 + @v3 + @v4도 SET @v1 = (@v2 + @v3) + @v4와 동일합니다.  
  
 += 연산자는 변수 없이 사용할 수 없습니다. 예를 들어 다음 코드를 실행하면 오류가 발생합니다.  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>예  
### <a name="a-concatenation-using--operator"></a>A. += 연산자를 사용한 연결
 다음 예에서는 `+=` 연산자를 사용하여 문자열을 연결합니다.  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. += 연산자를 사용한 연결 시의 계산 순서
다음 예제에서는 여러 문자열을 연결하여 하나의 긴 문자열을 만든 다음, 최종 문자열의 길이를 컴퓨팅합니다. 이 예제에서는 연결 연산자 사용 시의 계산 순서 및 잘림 규칙을 보여 줍니다. 

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
   
## <a name="see-also"></a>참고 항목  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+=&#40;더하기 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;문자열 연결&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
