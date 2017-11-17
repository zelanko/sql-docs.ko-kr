---
title: "및 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
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
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- TRUE
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f21efc0360c992c3a88706a13f84f35d7026b101
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="and-transact-sql"></a>AND(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 부울 식 결합 하 고 반환 **TRUE** 두 식이 모두 경우 **TRUE**합니다. 하나 이상의 논리 연산자 한 문에 사용 되는 경우는 **AND** 연산자가 먼저 계산 됩니다. 계산 순서를 변경하려면 괄호를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>인수  
 *boolean_expression*  
 유효한 [식](../../t-sql/language-elements/expressions-transact-sql.md) 부울 값을 반환 하는: **TRUE**, **FALSE**, 또는 **알 수 없는**합니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 두 식이 모두 TRUE일 때 TRUE를 반환합니다.  
  
## <a name="remarks"></a>주의  
 다음 차트에서는 AND 연산자를 사용하여 TRUE와 FALSE 값을 비교한 결과를 보여 줍니다.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**알 수 없음**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-and-operator"></a>1. AND 연산자 사용  
 다음 예에서는 직책이 `Marketing Assistant`이고 휴가가 `41`시간 넘게 남은 직원에 대한 정보를 선택합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>2. IF 문에서 AND 연산자 사용  
 다음 예에서는 IF 문에서 AND를 사용하는 방법의 예를 보여 줍니다. 첫 번째 문에서 `1 = 1` 및 `2 = 2`는 모두 true이므로 결과는 true입니다. 두 번째 예에서 인수 `2 = 17`이 false이므로 결과는 false입니다.  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [여기서 &#40; Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

