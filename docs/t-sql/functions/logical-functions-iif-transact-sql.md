---
title: IIF(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IIF_TSQL
- IIF
dev_langs:
- TSQL
helpviewer_keywords:
- IIF function
ms.assetid: e3ccf8ed-1cec-43ac-90b7-d8597c24b050
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9055a2dcd0c39f1421dff025f6754f9450be176
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715001"
---
# <a name="logical-functions---iif-transact-sql"></a>논리 함수 - IIF(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 부울 식이 True인지 False인지에 따라 두 값 중 하나를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IIF ( boolean_expression, true_value, false_value )  
```  
  
## <a name="arguments"></a>인수  
 *boolean_expression*  
 유효한 부울 식입니다.  
  
 이 인수가 부울 식이 아닌 경우 구문 오류가 발생합니다.  
  
 *true_value*  
 *boolean_expression*이 true로 평가되면 반환할 값입니다.  
  
 *false_value*  
 *boolean_expression*이 false로 평가되면 반환할 값입니다.  
  
## <a name="return-types"></a>반환 형식  
 *true_value*와 *false_value* 형식에서 우선 순위가 가장 높은 데이터 형식을 반환합니다. 자세한 내용은 [데이터 형식 우선 순위&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 IIF는 CASE 문을 작성하는 약식 방법입니다. 첫 번째 인수로 전달되는 부울 식인 경우 평가 결과에 따라 나머지 두 인수 중 하나가 반환됩니다. 즉, 부울 식이 True이면 *true_value*가 반환되고, 부울 식이 False이거나 알 수 없으면 *false_value*가 반환됩니다. *true_value* 및 *false_value*는 모든 형식일 수 있습니다. 부울 식, null 처리 및 반환 형식에 대해 CASE 문에 적용되는 규칙이 IIF에도 적용됩니다. 자세한 내용은 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)를 참조하세요.  
  
 IIF가 CASE로 변환된다는 점은 이 함수의 다른 동작에도 영향을 줍니다. CASE 문은 최대 10개 수준만 중첩될 수 있으므로 IIF 문도 최대 10개 수준만 중첩될 수 있습니다. 또한 IIF는 원격 실행되는 CASE 문과 모든 동작이 같으므로 다른 서버에 대해 기능적으로 동일한 CASE 문으로 원격 실행됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-simple-iif-example"></a>1. 간단한 IIF 예  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
TRUE  
  
(1 row(s) affected)  
```  
  
### <a name="b-iif-with-null-constants"></a>2. NULL 상수가 있는 IIF  
  
```  
SELECT IIF ( 45 > 30, NULL, NULL ) AS Result;  
```  
  
 이 문의 결과는 오류입니다.  
  
### <a name="c-iif-with-null-parameters"></a>3. NULL 매개 변수가 있는 IIF  
  
```  
DECLARE @P INT = NULL, @S INT = NULL;  
SELECT IIF ( 45 > 30, @p, @s ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [CASE&#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CHOOSE&#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  
