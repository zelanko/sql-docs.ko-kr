---
title: AND(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- "TRUE"
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb5211a2d45ef1a5495d1df57143190f1d5f6419
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67927374"
---
# <a name="and-transact-sql"></a>AND(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 개의 부울 식을 결합하여 두 식이 모두 **TRUE**일 때만 **TRUE**를 반환합니다. 문에 두 개 이상의 논리 연산자가 사용될 경우 **AND** 연산자가 먼저 계산됩니다. 계산 순서를 변경하려면 괄호를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>인수  
 *boolean_expression*  
 [TRUE](../../t-sql/language-elements/expressions-transact-sql.md), **FALSE** 또는 **UNKNOWN**의 부울 값을 반환하는 유효한 **식**입니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 두 식이 모두 TRUE일 때 TRUE를 반환합니다.  
  
## <a name="remarks"></a>설명  
 다음 차트에서는 AND 연산자를 사용하여 TRUE와 FALSE 값을 비교한 결과를 보여 줍니다.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**UNKNOWN**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-and-operator"></a>A. AND 연산자 사용  
 다음 예에서는 직책이 `Marketing Assistant`이고 휴가가 `41`시간 넘게 남은 직원에 대한 정보를 선택합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. IF 문에서 AND 연산자 사용  
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
  
## <a name="see-also"></a>참고 항목  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
