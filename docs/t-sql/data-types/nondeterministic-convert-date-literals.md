---
title: 날짜 리터럴의 비결정적 변환 | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eba0e28d8f2d5587a07308a4ffcbf5f7eaedf278
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119847"
---
# <a name="nondeterministic-conversion-of-literal-date-strings-into-date-values"></a>날짜 값으로 리터럴 날짜 문자열의 비결정적 변환

날짜 데이터 형식으로 CHARACTER 문자열의 변환을 허용하는 경우에 주의해야 합니다. 이유는 이러한 변환이 자주 _비결정적_이기 때문입니다.

[SET LANGUAGE](../statements/set-language-transact-sql.md) 및 [SET DATEFORMAT](../statements/set-dateformat-transact-sql.md)의 설정을 고려하여 이러한 비결정적 변환을 제어합니다.



## <a name="set-language-example-month-name-in-polish"></a>SET LANGUAGE 예: 폴란드어로 Month 이름

- `SET LANGUAGE Polish;`

문자열은 월의 이름일 수 있습니다. 하지만 이름이 영어 또는 폴란드어 또는 크로아티아어 또는 다른 언어인가요? 사용자의 세션이 올바른 해당 언어로 설정되나요?

예를 들어 단어 달의 이름인 _listopad_를 고려해봅니다. 하지만 SQL 시스템에서 믿는 언어에 따라 달라지는 달이 사용됩니다.
- 폴란드어의 경우 _listopad_는 11월로 변역됩니다(영어로 _November_).
- 크로아티아어의 경우 _listopad_는 10월로 변역됩니다(영어로 _October_).

#### <a name="code-example-of-set-language"></a>SET LANGUAGE의 코드 예제

```sql
--SELECT alias FROM sys.syslanguages ORDER BY alias;

DECLARE @yourInputDate  NVARCHAR(32) = '28 listopad 2018';

SET LANGUAGE Polish;
SELECT CONVERT(DATE, @yourInputDate) AS [SL_Polish];

SET LANGUAGE Croatian;
SELECT CONVERT(DATE, @yourInputDate) AS [SL_Croatian];

SET LANGUAGE English;


/***  Actual output:  For the two months, note the 11 versus the 10.
SL_Polish
2018-11-28

SL_Croatian
2018-10-28
***/
```



## <a name="set-dateformat-example"></a>SET DATEFORMAT 예제

- `SET DATEFORMAT dmy;`

위의 **dmy** 형식은 '01-03-2018'의 예제 날짜 문자열이 _2018년 3월 1일_을 의미하는 것으로 번역되는 것을 말합니다.

대신 **mdy**가 지정된 경우 동일한 '01-03-2018' 문자열은 _2018년 1월 3일_을 의미합니다.

**ymd**가 지정된 경우 출력 값은 보장되지 않습니다. '2018'의 숫자 값은 너무 커서 날이 될 수 없습니다.
<!--
The preceding claim of "no guarantee" might be incorrect, in the minds of the SQL query engine Developer team?
-->

#### <a name="specific-countries"></a>특정 국가

일본 및 중국에서 **ymd**의 DATEFORMAT이 사용됩니다. 형식의 부분은 가장 큰 단위에서 가장 작은 단위까지 합리적인 순서로 배열되어 있습니다. 따라서 이 형식에서 잘 정렬합니다. 이 형식은 _국제_ 형식으로 간주됩니다. 연도의 네 자리는 모호하지 않으며, 지구상의 어떤 나라도 **ydm**의 낡은 형식을 사용하지 않으므로 이는 국제적입니다.

독일 및 프랑스와 같은 다른 국가에서 DATEFORMAT은 **dmy**, 즉 **'dd-mm-yyyy'** 입니다. **dmy** 형식은 잘 정렬하지 않지만 가장 작은 단위에서 가장 큰 단위의 합리적인 순서입니다.

미국 및 미크로네시아는 정렬되지 않는 **mdy**를 사용하는 유일한 국가입니다. 형식의 혼합 시퀀스는 구술 날짜의 구두 음성의 패턴과 일치합니다.

#### <a name="code-example-of-set-dateformat-mdy-versus-dmy"></a>SET DATEFORMAT의 코드 예제: *mdy*와 *dmy* 비교

다음 Transact-SQL 코드 예제에서는 세 가지 다른 DATEFORMAT 설정으로 동일한 날짜 문자열을 사용합니다. 코드를 실행하면 주석에서 표시되는 출력이 생성됩니다.

```sql
DECLARE @yourDateString NVARCHAR(10) = '12-09-2018';
PRINT @yourDateString + '  = the input.';

SET DATEFORMAT dmy;
SELECT CONVERT(DATE, @yourDateString) AS [DMY-Interpretation-of-input-format];

SET DATEFORMAT mdy;
SELECT CONVERT(DATE, @yourDateString) AS [MDY-Interpretation-of-input-format];

SET DATEFORMAT ymd;
SELECT CONVERT(DATE, @yourDateString) AS [YMD-Interpretation--?--NotGuaranteed];


/***  Actual output:
12-09-2018  = the input.

DMY-Interpretation-of-input-format
2018-09-12

MDY-Interpretation-of-input-format
2018-12-09

YMD-Interpretation--?--NotGuaranteed
2018-12-09
***/
```

위의 코드 예제에서 마지막 예제에는 **ymd** 형식과 입력 문자열 간에 불일치가 있습니다. 입력 문자열의 세 번째 노드는 날이 되기에 너무 큰 숫자 값을 나타냅니다. Microsoft는 이러한 불일치에서 출력 값을 보장하지 않습니다.

#### <a name="convert-offers-explicit-codes-for-deterministic-control-of-date-formats"></a>CONVERT는 날짜 형식의 _결정적_ 제어에 대한 명시적 코드를 제공합니다.

CAST 및 CONVERT 설명서 문서는 날짜 변환을 _결정적으로_ 제어하는 데 CONVERT 함수와 함께 사용할 수 있는 명시적 코드를 나열합니다. 해당 문서는 매달 가장 높은 페이지뷰 중 하나를 차지합니다.

- [CAST 및 CONVERT(Transact-SQL): 날짜 및 시간 스타일](../functions/cast-and-convert-transact-sql.md#date-and-time-styles)
- [CAST 및 CONVERT(Transact-SQL): 일부 datetime 변환은 비결정적임](../functions/cast-and-convert-transact-sql.md#certain-datetime-conversions-are-nondeterministic)



## <a name="compatibility-level-90-and-above"></a>호환성 수준 90 이상

SQL Server 2000에서는 호환성 수준이 80이었습니다. 80 이하의 수준 설정의 경우 암시적 날짜 변환은 결정적이었습니다.

SQL Server 2005 및 90의 호환성 수준부터 암시적 데이터 변환은 비결정적이 되었습니다. 날짜 변환은 SET LANGUAGE 및 수준 90으로 시작하는 SET DATEFORMAT에 따라 달라지게 되었습니다.

#### <a name="unicode"></a>유니코드

<!-- The next live sentence needs an explanatory example!  N'somethingHere?'.
-->
데이터 정렬 간의 비유니코드 문자 데이터를 변환하는 작업도 비결정적인 것으로 간주됩니다.



## <a name="see-also"></a>관련 항목:

- [세션 언어 설정](../../relational-databases/collations/set-a-session-language.md)
- [날짜 및 시간 데이터 형식 및 함수(Transact-SQL)](../functions/date-and-time-data-types-and-functions-transact-sql.md)
- [FORMAT(Transact-SQL)](../functions/format-transact-sql.md)
- [ISDATE(Transact-SQL)](../functions/isdate-transact-sql.md)



<!--
This new article is linked-to by the following articles (at least initially on 2018/11/19).....
...
* docs/relational-databases/views/create-indexed-views.md
* docs/relational-databases/indexes/indexes-on-computed-columns.md
* docs/t-sql/functions/cast-and-convert-transact-sql.md
...
As a reaction to public PR 1279, this approach of creating a new article to link to is a better alternative than a docs/includes/ approach.
GeneMi (MightyPen), 2018/11/19
-->

