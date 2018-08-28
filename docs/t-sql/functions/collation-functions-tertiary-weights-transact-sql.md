---
title: TERTIARY_WEIGHTS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab610f5fbb691e9ec3493fc9bf5637d6b2f841eb
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43060640"
---
# <a name="collation-functions---tertiaryweights-transact-sql"></a>데이터 정렬 함수 - TERTIARY_WEIGHTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

비유니코드 문자열 식의 각 문자에 대해 SQL 3차 데이터 정렬로 정의된 이 함수는 정렬 조건(weight)의 이진 문자열로 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
TERTIARY_WEIGHTS( non_Unicode_character_string_expression )  
```  
  
## <a name="arguments"></a>인수  
*non_Unicode_character_string_expression*  
3차 SQL 데이터 정렬에 정의된 **char**, **varchar** 또는 **varchar(max)** 형식의 문자열 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 이러한 데이터 정렬의 목록은 주의를 참조하세요.
  
## <a name="return-types"></a>반환 형식
`TERTIARY_WEIGHTS`는 *non_Unicode_character_string_expression*이 **char** 또는 **varchar**인 경우 **varbinary**를 반환하고, *non_Unicode_character_string_expression*이 **varchar(max)** 데이터 형식을 가진 경우 **varbinary(max)** 를 반환합니다.
  
## <a name="remarks"></a>Remarks  
`TERTIARY_WEIGHTS`는 SQL 3차 컬렉션이 *non_Unicode_character_string_expression*을 정의하지 않는 경우 NULL을 반환합니다. 이 표에서는 SQL 3차 데이터 정렬을 보여 줍니다.
  
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
  
**char**, **varchar** 또는 **varchar(max)** 열 값에 정의되는 계산 열 정의에 `TERTIARY_WEIGHTS`를 사용합니다. 계산 열과 **char**, **varchar** 또는 **varchar(max)** 열 모두에서 인덱스 정의는 쿼리의 ORDER BY 절이 해당 **char**, **varchar** 또는 **varchar(max)** 열을 지정하는 경우 성능을 향상시킬 수 있습니다.
  
## <a name="examples"></a>예  
이 예에서는 `TERTIARY_WEIGHTS` 함수를 `char` 열의 값에 적용하는 계산 열을 테이블에 만듭니다.
  
```sql
CREATE TABLE TertColTable  
(Col1 char(15) COLLATE SQL_Latin1_General_Pref_CP437_CI_AS,  
Col2 AS TERTIARY_WEIGHTS(Col1));  
GO   
```  
  
## <a name="see-also"></a>관련 항목:
[ORDER BY 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)
  
  
