---
title: '%(모듈러스)(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- modulo
- modulus
- '% (Modulo)'
- '% (Modulus)'
- MOD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '% (modulo operator)'
- '% (modulus operator)'
- remainder of division operation
- modulo operator (%)
- modulus operator (%)
ms.assetid: f93c662e-f405-486e-bf23-a2d03907b5bd
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67a4a4ad32e1d9471dc9a5b3d2f1c7b067cf480b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68122124"
---
# <a name="-modulus-transact-sql"></a>%(모듈러스)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  한 숫자를 다른 숫자로 나눈 나머지를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
dividend % divisor  
```  
  
## <a name="arguments"></a>인수  
 *dividend*  
 나눌 숫자 식입니다. *dividend*는 정수 및 통화 데이터 형식 범주에 속하는 데이터 형식 중 하나 또는 [numeric](../../t-sql/language-elements/expressions-transact-sql.md) 데이터 형식을 사용하는 유효한 **식**이어야 합니다.  
  
 *divisor*  
 피제수를 나눌 숫자 식입니다. *divisor*는 정수 및 통화 데이터 형식 범주에 속하는 데이터 형식 중 하나 또는 **numeric** 데이터 형식을 사용하는 유효한 식이어야 합니다.  
  
## <a name="result-types"></a>결과 형식  
 두 인수의 데이터 형식에 따라 결정됩니다.  
  
## <a name="remarks"></a>설명  
 열 이름, 숫자 상수 또는 정수 및 통화 데이터 형식 범주나 **numeric** 데이터 형식을 사용한 유효한 식의 모든 조합이 들어 있는 SELECT 문의 선택 목록에 모듈로 산술 연산자를 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-example"></a>A. 간단한 예  
 다음 예에서는 숫자 38을 5로 나눕니다. 결과의 정수 부분은 7이며 나머지 3을 반환하는 모듈로를 보여 줍니다.  
  
```  
SELECT 38 / 5 AS Integer, 38 % 5 AS Remainder ;  
  
```  
  
### <a name="b-example-using-columns-in-a-table"></a>B. 테이블에서 열을 사용한 예  
 다음 예에서는 제품 ID 수, 제품 단가 및 정수 값으로 변환된 각 제품의 가격을 주문한 제품의 수로 나눈 모듈로(나머지)를 반환합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(100)ProductID, UnitPrice, OrderQty,  
   CAST((UnitPrice) AS int) % OrderQty AS Modulo  
FROM Sales.SalesOrderDetail;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example"></a>C: 간단한 예  
 다음 예제에서는 3을 2로 나눌 때 `%` 연산자에 대한 결과를 보여 줍니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) 3%2 FROM dimEmployee;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
1         
```  
  
## <a name="see-also"></a>참고 항목  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [%=&#40;모듈러스 대입&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


