---
title: ISDATE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e005b11ad15170dcc2f6f45441d62e6ccc29570
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isdate-transact-sql"></a>ISDATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  경우 1을 반환는 *식* 은 유효한 **날짜**, **시간**, 또는 **datetime** ; 값, 그렇지 않으면 0입니다.  
  
 ISDATE 0을 반환 하는 경우는 *식* 은 **datetime2** 값입니다.  
  
 모든 개요 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식 및 함수, 참조 [날짜 및 시간 데이터 형식 및 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md). datetime 데이터의 범위는 1753-01-01부터 9999-12-31까지이지만 date 데이터의 범위는 0001-01-01부터 9999-12-31까지입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ISDATE ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 문자열 또는 [식](../../t-sql/language-elements/expressions-transact-sql.md) 문자로 된 문자열로 변환할 수 있습니다. 이 식은 4,000자 미만이어야 합니다. datetime 및 smalldatetime을 제외하고 날짜 및 시간 데이터 형식은 ISDATE에 대한 인수로 허용되지 않습니다.  
  
## <a name="return-type"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 ISDATE는 함께 사용할 경우에 결정적는 [변환](../../t-sql/functions/cast-and-convert-transact-sql.md) CONVERT 스타일 매개 변수를 지정 하 고 스타일이 0, 100, 9 또는 109가 아닌 경우 작동 합니다.  
  
 ISDATE의 반환 값의 설정에 따라 달라 집니다 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md), [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및 [default language 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)합니다.  
  
## <a name="isdate-expression-formats"></a>ISDATE 식 형식  
 ISDATE 메서드 1를 반환 하는 유효한 형식의 예의 "지원 되는 문자열 리터럴 형식 datetime에 대해" 섹션을 참조는 [datetime](../../t-sql/data-types/datetime-transact-sql.md) 및 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 항목입니다. 예를 보려면의 "인수" 섹션의 입/출력 열이 표시도 [CAST 및 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)합니다.  
  
 다음 표에서는 0 또는 오류를 반환하는 잘못된 입력 식 형식을 요약하여 보여 줍니다.  
  
|ISDATE 식|ISDATE 반환 값|  
|-----------------------|-------------------------|  
|NULL|0|  
|데이터 형식의 값에 나열 된 [데이터 형식](../../t-sql/data-types/data-types-transact-sql.md) 문자열, 유니코드 문자열 또는 날짜 및 시간 이외의 모든 데이터 형식 범주에 있습니다.|0|  
|값 **텍스트**, **ntext**, 또는 **이미지** 데이터 형식입니다.|0|  
|초의 소수 자릿수가 세 자리를 초과하는 모든 값(.0000부터 .0000000...n까지) ISDATE 경우 0을 반환 합니다는 *식* 는 **datetime2** 그러나 값 이면 1을 반환 합니다는 *식* 유효한 **datetime** 값입니다.|0|  
|1995-10-1a와 같이 유효한 날짜에 잘못된 값이 섞여 있는 경우|0|  
  
## <a name="examples"></a>예  
  
### <a name="a-using-isdate-to-test-for-a-valid-datetime-expression"></a>1. ISDATE를 사용하여 올바른 datetime 식 테스트  
 다음 예제에서는 사용 하는 방법을 보여 줍니다. `ISDATE` 문자열은 유효한 있는지 여부를 테스트 **datetime**합니다.  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    PRINT 'VALID'  
ELSE  
    PRINT 'INVALID';  
```  
  
### <a name="b-showing-the-effects-of-the-set-dateformat-and-set-language-settings-on-return-values"></a>2. SET DATEFORMAT 및 SET LANGUAGE 설정이 반환 값에 미치는 영향  
 다음 문에서는 `SET DATEFORMAT` 및 `SET LANGUAGE` 설정의 결과로 반환되는 값을 보여 줍니다.  
  
```  
/* Use these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
/* Expression in mdy dateformat */  
SELECT ISDATE('04/15/2008'); --Returns 1.  
/* Expression in mdy dateformat */  
SELECT ISDATE('04-15-2008'); --Returns 1.   
/* Expression in mdy dateformat */  
SELECT ISDATE('04.15.2008'); --Returns 1.   
/* Expression in myd  dateformat */  
SELECT ISDATE('04/2008/15'); --Returns 1.  
  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET DATEFORMAT mdy;  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-isdate-to-test-for-a-valid-datetime-expression"></a>3. ISDATE를 사용하여 올바른 datetime 식 테스트  
 다음 예제에서는 사용 하는 방법을 보여 줍니다. `ISDATE` 문자열은 유효한 있는지 여부를 테스트 **datetime**합니다.  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    SELECT 'VALID';  
ELSE  
    SELECT 'INVALID';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


