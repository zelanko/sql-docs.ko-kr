---
title: IF...ELSE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IF_TSQL
- IF
dev_langs:
- TSQL
helpviewer_keywords:
- IF...ELSE keyword
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 676c881f-dee1-417a-bc51-55da62398e81
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b5068b47f1622171ec4d39087cb16fa3d37838f
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299034"
---
# <a name="ifelse-transact-sql"></a>IF...ELSE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

> [!div class="nextstepaction"]
> [SQL Docs 목차에 대한 피드백을 공유하세요!](https://aka.ms/sqldocsurvey)

[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하기 위한 조건을 설정합니다. IF 키워드 및 조건 다음에 이어지는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 부울 식이 TRUE를 반환하는 경우 즉, 조건이 만족되는 경우 실행됩니다. ELSE 키워드는 선택적이며 IF 조건이 만족되지 않는 경우 즉, 부울 식이 FALSE를 반환하는 경우 실행될 대체 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 동반합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>인수  
 *Boolean_expression*  
 TRUE 또는 FALSE를 반환하는 식입니다. 부울 식이 SELECT 문을 포함하는 경우에는 SELECT 문을 괄호로 묶어야 합니다.  
  
 { *sql_statement*| *statement_block* }  
 문 블록을 사용하여 정의한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 그룹입니다. 문 블록을 사용하지 않으면 IF나 ELSE 조건이 하나의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행에만 영향을 줍니다.  
  
 문 블록을 정의하려면 흐름 제어 키워드인 BEGIN 및 END를 사용하세요.  
  
## <a name="remarks"></a>Remarks  
 일괄 처리, 저장 프로시저 및 임시 쿼리 내에서 IF...ELSE 구문을 사용할 수 있습니다. 저장 프로시저에서는 일부 매개 변수의 존재 여부를 테스트하는 데 이 구문이 자주 사용됩니다.  
  
 IF 검사는 다른 IF 뒤에 중첩될 수 있으며 ELSE 뒤에 다른 IF가 올 수도 있습니다. 가능한 중첩 수준은 사용 가능한 메모리에 따라 달라집니다.  
  
## <a name="example"></a>예제  
  
```  
IF DATENAME(weekday, GETDATE()) IN (N'Saturday', N'Sunday')
       SELECT 'Weekend';
ELSE 
       SELECT 'Weekday';
```  
  
 더 많은 예제를 보려면 [ELSE &#40;IF...ELSE&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md)을 참조하세요.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `IF...ELSE`를 사용하여 `DimProduct` 테이블에 있는 항목의 가중치에 따라 두 응답 중 사용자를 표시할 응답을 결정합니다.  
  
```  
-- Uses AdventureWorksDW  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct 
                  WHERE ProductKey = @productKey)   
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is too heavy to ship and is only available for pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
ELSE  
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is available for shipping or pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
```  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [END&#40;BEGIN...END&#41;&#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHILE&#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [흐름 제어 언어&#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md) [ELSE &#40;IF...ELSE&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md) 
  
  



