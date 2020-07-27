---
title: ISDATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISDATETIME
- ISDATE_TSQL
- ISDATE
- ISDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], ISDATE
- validate dates times [SQL Server]
- formats [SQL Server], time
- dates [SQL Server], validate
- verify dates times [SQL Server]
- functions [SQL Server], time
- formats [SQL Server], dates
- functions [SQL Server], date and time
- time [SQL Server], functions
- time [SQL Server], validate
- ISDATE function [SQL Server]
ms.assetid: 8e2c9ee7-388a-432f-b2c9-7b398f26bf85
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aadb2783bbb92123355cef1adba98170d3cd0a2f
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484226"
---
# <a name="isdate-transact-sql"></a>ISDATE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  *expression*이 유효한 **date**, **time** 또는 **datetime** 값인 경우 1을 반환합니다. 그렇지 않을 경우 0을 반환합니다.

 *expression*이 **datetime2** 값인 경우 ISDATE에서 0을 반환합니다.

 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식 및 함수에 대한 개요는 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)을 참조하세요. datetime 데이터의 범위는 1753-01-01부터 9999-12-31까지이지만 date 데이터의 범위는 0001-01-01부터 9999-12-31까지입니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
ISDATE ( expression )
```

## <a name="arguments"></a>인수
 *expression* 문자열이거나 문자열로 변환할 수 있는 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 이 식은 4,000자 미만이어야 합니다. datetime 및 smalldatetime을 제외하고 날짜 및 시간 데이터 형식은 ISDATE에 대한 인수로 허용되지 않습니다.

## <a name="return-type"></a>반환 형식
 **int**

## <a name="remarks"></a>설명
 ISDATE는 [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 함수와 함께 사용하고 CONVERT 스타일 매개 변수가 지정되고 스타일이 0, 100, 9 또는 109가 아닌 경우에만 결정적입니다.

 ISDATE의 반환 값은 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md), [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및 [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)의 설정에 따라 달라집니다.

## <a name="isdate-expression-formats"></a>ISDATE 식 형식
 ISDATE에서 1을 반환하는 유효한 형식의 예는 [datetime](../../t-sql/data-types/datetime-transact-sql.md) 및 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 항목의 "datetime에 대해 지원되는 문자열 리터럴 형식" 섹션을 참조하세요. 다른 예를 보려면 [CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)의 "인수" 섹션에서 입/출력 열을 참조하세요.

 다음 표에서는 0 또는 오류를 반환하는 잘못된 입력 식 형식을 요약하여 보여 줍니다.

|ISDATE 식|ISDATE 반환 값|
|-----------------------|-------------------------|
|NULL|0|
|[데이터 형식](../../t-sql/data-types/data-types-transact-sql.md)에서 문자열, 유니코드 문자열, 또는 날짜 및 시간을 제외한 모든 데이터 형식 범주에 속한 데이터 형식의 값|0|
|**text**, **ntext** 또는 **image** 데이터 형식의 값|0|
|초의 소수 자릿수가 세 자리를 초과하는 모든 값(.0000부터 .0000000...n까지) ISDATE는 *식*이 **datetime2** 값일 경우 0을 반환하지만 *식*이 유효한 **datetime** 값일 경우에는 1을 반환합니다.|0|
|1995-10-1a와 같이 유효한 날짜에 잘못된 값이 섞여 있는 경우|0|

## <a name="examples"></a>예

### <a name="a-using-isdate-to-test-for-a-valid-datetime-expression"></a>A. ISDATE를 사용하여 올바른 datetime 식 테스트
 다음 예에서는 `ISDATE`를 사용하여 문자열이 올바른 **datetime**인지 테스트하는 방법을 보여 줍니다.

```sql
IF ISDATE('2009-05-12 10:19:41.177') = 1
    PRINT 'VALID'
ELSE
    PRINT 'INVALID';
```

### <a name="b-showing-the-effects-of-the-set-dateformat-and-set-language-settings-on-return-values"></a>B. SET DATEFORMAT 및 SET LANGUAGE 설정이 반환 값에 미치는 영향
 다음 문에서는 `SET DATEFORMAT` 및 `SET LANGUAGE` 설정의 결과로 반환되는 값을 보여 줍니다.

```sql
/* Use these sessions settings. */
SET LANGUAGE us_english;
SET DATEFORMAT mdy;

/* Expression in mdy dateformat */  
SELECT ISDATE('04/15/2008'); --Returns 1.
SELECT ISDATE('04-15-2008'); --Returns 1.
SELECT ISDATE('04.15.2008'); --Returns 1.

/* Expression in myd dateformat */
SELECT ISDATE('04/2008/15'); --Returns 1.

SET DATEFORMAT mdy;
SELECT ISDATE('15/04/2008'); --Returns 0.
SELECT ISDATE('15/2008/04'); --Returns 0.
SELECT ISDATE('2008/15/04'); --Returns 0.
SELECT ISDATE('2008/04/15'); --Returns 1.

SET DATEFORMAT dmy;
SELECT ISDATE('15/04/2008'); --Returns 1.
SET DATEFORMAT dym;
SELECT ISDATE('15/2008/04'); --Returns 1.
SET DATEFORMAT ydm;
SELECT ISDATE('2008/15/04'); --Returns 1.
SET DATEFORMAT ymd;
SELECT ISDATE('2008/04/15'); --Returns 1.

SET LANGUAGE English;
SELECT ISDATE('15/04/2008'); --Returns 0.
SET LANGUAGE Hungarian;
SELECT ISDATE('15/2008/04'); --Returns 0.
SET LANGUAGE Swedish;
SELECT ISDATE('2008/15/04'); --Returns 0.
SET LANGUAGE Italian;
SELECT ISDATE('2008/04/15'); --Returns 1.

/* Return to these sessions settings. */
SET LANGUAGE us_english;
SET DATEFORMAT mdy;
```

## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### <a name="c-using-isdate-to-test-for-a-valid-datetime-expression"></a>C. ISDATE를 사용하여 올바른 datetime 식 테스트
 다음 예에서는 `ISDATE`를 사용하여 문자열이 올바른 **datetime**인지 테스트하는 방법을 보여 줍니다.

```sql
IF ISDATE('2009-05-12 10:19:41.177') = 1
    SELECT 'VALID';
ELSE
    SELECT 'INVALID';
```


## <a name="see-also"></a>참고 항목
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
