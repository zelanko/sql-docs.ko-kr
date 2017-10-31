---
title: TERTIARY_WEIGHTS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TERTIARY_WEIGHTS_TSQL
- TERTIARY_WEIGHTS
dev_langs:
- TSQL
helpviewer_keywords:
- weights [SQL Server]
- SQL tertiary collations
- TERTIARY_WEIGHTS function
ms.assetid: 7e1f5350-260b-4c61-8c84-69bb1a214f1f
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7414f60414c14457dddc6f860201fd84409f1cb1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="collation-functions---tertiaryweights-transact-sql"></a>데이터 정렬 함수-TERTIARY_WEIGHTS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

비유니코드 문자열 식의 각 문자에 대해 SQL 3차 데이터 정렬로 정의된 정렬 조건(weight)을 이진 문자열로 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
TERTIARY_WEIGHTS( non_Unicode_character_string_expression )  
```  
  
## <a name="arguments"></a>인수  
*non_Unicode_character_string_expression*  
문자열인 [식](../../t-sql/language-elements/expressions-transact-sql.md) 형식의 **char**, **varchar**, 또는 **varchar (max)** 3 차 SQL 데이터 정렬에서 정의 합니다. 이러한 데이터 정렬의 목록은 주의를 참조하세요.
  
## <a name="return-types"></a>반환 형식
TERTIARY_WEIGHTS 반환 **varbinary** 때 *non_Unicode_character_string_expression* 은 **char** 또는 **varchar**, 반환 **varbinary (max)** 때 *non_Unicode_character_string_expression* 은 **varchar (max)**합니다.
  
## <a name="remarks"></a>주의  
TERTIARY_WEIGHTS NULL을 반환 *non_Unicode_character_string_expression* 는 SQL 3 차 데이터 정렬으로 정의 되어 있지 않습니다. 표에서는 SQL 3차 데이터 정렬을 보여 줍니다.
  
|정렬 순서 ID|SQL 데이터 정렬|  
|---|---|
|33|SQL_Latin1_General_Pref_CP437_CI_AS|  
|34|SQL_Latin1_General_CP437_CI_AI|  
|43|SQL_Latin1_General_Pref_CP850_CI_AS|  
|44|SQL_Latin1_General_CP850_CI_AI|  
|49|SQL_1xCompat_CP850_CI_AS|  
|53|SQL_Latin1_General_Pref_CP1_CI_AS|  
|54|SQL_Latin1_General_CP1_CI_AI|  
|56|SQL_AltDiction_Pref_CP850_CI_AS|  
|57|SQL_AltDiction_CP850_CI_AI|  
|58|SQL_Scandinavian_Pref_CP850_CI_AS|  
|82|SQL_Latin1_General_CP1250_CI_AS|  
|84|SQL_Czech_CP1250_CI_AS|  
|86|SQL_Hungarian_CP1250_CI_AS|  
|88|SQL_Polish_CP1250_CI_AS|  
|90|SQL_Romanian_CP1250_CI_AS|  
|92|SQL_Croatian_CP1250_CI_AS|  
|94|SQL_Slovak_CP1250_CI_AS|  
|96|SQL_Slovenian_CP1250_CI_AS|  
|106|SQL_Latin1_General_CP1251_CI_AS|  
|108|SQL_Ukrainian_CP1251_CI_AS|  
|113|SQL_Latin1_General_CP1253_CS_AS|  
|114|SQL_Latin1_General_CP1253_CI_AS|  
|130|SQL_Latin1_General_CP1254_CI_AS|  
|146|SQL_Latin1_General_CP1256_CI_AS|  
|154|SQL_Latin1_General_CP1257_CI_AS|  
|156|SQL_Estonian_CP1257_CI_AS|  
|158|SQL_Latvian_CP1257_CI_AS|  
|160|SQL_Lithuanian_CP1257_CI_AS|  
|183|SQL_Danish_Pref_CP1_CI_AS|  
|184|SQL_SwedishPhone_Pref_CP1_CI_AS|  
|185|SQL_SwedishStd_Pref_CP1_CI_AS|  
|186|SQL_Icelandic_Pref_CP1_CI_AS|  
  
값에 정의 된 계산 열의 정의에 사용 하기 위한 TERTIARY_WEIGHTS는 **char**, **varchar**, 또는 **varchar (max)** 열입니다. 계산된 열에 인덱스를 정의 및 **char**, **varchar**, 또는 **varchar (max)** 열에는 성능을 향상 시킬 수는 경우는 **char**, **varchar**, 또는 **varchar (max)** 열이 쿼리의 ORDER BY 절에 지정 됩니다.
  
## <a name="examples"></a>예  
다음 예에서는 `TERTIARY_WEIGHTS` 함수를 `char` 열의 값에 적용하는 계산 열을 테이블에 만듭니다.
  
```sql
CREATE TABLE TertColTable  
(Col1 char(15) COLLATE SQL_Latin1_General_Pref_CP437_CI_AS,  
Col2 AS TERTIARY_WEIGHTS(Col1));  
GO   
```  
  
## <a name="see-also"></a>참고 항목
[ORDER BY 절 &#40; Transact SQL &#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)
  
  

