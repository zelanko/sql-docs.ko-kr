---
title: 날짜 및 시간 데이터 형식과 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azure-sqldw-latest||= azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 340967f5f44b7cbdec4e23dd0cd9a400522bbe8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65943718"
---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>날짜 및 시간 데이터 형식 및 함수(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

이 항목의 섹션에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 모든 날짜/시간 데이터 형식 및 함수를 다룹니다.
-   [날짜 및 시간 데이터 형식](#DateandTimeDataTypes)  
-   [날짜 및 시간 함수](#DateandTimeFunctions)  
    -   [시스템 날짜 및 시간 값을 반환하는 함수](#GetSystemDateandTimeValues)  
    -   [날짜 및 시간 부분을 반환하는 함수](#GetDateandTimeParts)  
    -   [해당 부분에서 날짜 및 시간 값을 반환하는 함수](#fromParts)  
    -   [날짜 및 시간 차이 값을 반환하는 함수](#GetDateandTimeDifference)  
    -   [날짜 및 시간 값 수정 함수](#ModifyDateandTimeValues)  
    -   [세션 형식 함수를 설정 또는 반환하는 함수](#SetorGetSessionFormatFunctions)  
    -   [날짜 및 시간 값 유효성 검사 함수](#ValidateDateandTimeValues)  
-   [날짜 및 시간 관련 토픽](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a> 날짜 및 시간 데이터 형식
다음 표에 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 날짜 및 시간 데이터 형식이 나와 있습니다.
  
|데이터 형식|형식|범위|정확도|스토리지 크기(바이트)|사용자 정의 초 소수 부분 자릿수|표준 시간대 오프셋|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000부터 23:59:59.9999999까지|100나노초|3 ~ 5|예|아니오|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01부터 31.12.99까지|1일|3|아니오|아니오|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01부터 2079-06-06까지|1분|4|아니오|아니오|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01부터 9999-12-31까지|0.00333초|8|아니오|아니오|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000부터 9999-12-31 23:59:59.9999999까지|100나노초|6 ~ 8|예|아니오|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|0001-01-01 00:00:00.0000000부터 9999-12-31 23:59:59.9999999까지(UTC)|100나노초|8 ~ 10|예|예|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) 데이터 형식은 날짜 또는 시간 데이터 형식이 아닙니다. **timestamp**는 **rowversion**에 사용되지 않는 동의어입니다.  
  
##  <a name="DateandTimeFunctions"></a> 날짜 및 시간 함수  
다음 표에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 함수를 나열합니다. 결정성에 대한 자세한 내용은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.
  
###  <a name="GetSystemDateandTimeValues"></a> 시스템 날짜 및 시간 값을 반환하는 함수 
[!INCLUDE[tsql](../../includes/tsql-md.md)]은 모든 시스템 날짜 및 시간 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행 중인 컴퓨터 운영 체제에서 가져옵니다.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>정밀도가 높은 시스템 날짜 및 시간 함수  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 GetSystemTimeAsFileTime() Windows API를 사용하여 날짜 및 시간 값을 가져옵니다. 정확도는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 하드웨어와 Windows 버전에 따라 달라집니다. 이 API의 정밀도는 100나노초에 고정되어 있습니다. 정확도를 확인하려면 GetSystemTimeAdjustment() Windows API를 사용합니다.
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 날짜와 시간이 포함된 **datetime2(7)** 값을 반환합니다. 반환 값에는 표준 시간대 오프셋이 포함되지 않습니다.|**datetime2(7)**|비결정적|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 날짜와 시간이 포함된 **datetimeoffset(7)** 값을 반환합니다. 반환 값에는 표준 시간대 오프셋이 포함됩니다.|**datetimeoffset(7)**|비결정적|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 날짜와 시간이 포함된 **datetime2(7)** 값을 반환합니다. 함수는 날짜와 시간 값을 UTC 시간(Coordinated Universal Time)으로 반환합니다.|**datetime2(7)**|비결정적|  
  
#### <a name="lower-precision-system-date-and-time-functions"></a>정밀도가 낮은 시스템 날짜 및 시간 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 날짜와 시간이 포함된 **datetime** 값을 반환합니다. 반환 값에는 표준 시간대 오프셋이 포함되지 않습니다.|**datetime**|비결정적|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 날짜와 시간이 포함된 **datetime** 값을 반환합니다. 반환 값에는 표준 시간대 오프셋이 포함되지 않습니다.|**datetime**|비결정적|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 날짜와 시간이 포함된 **datetime** 값을 반환합니다. 함수는 날짜와 시간 값을 UTC 시간(Coordinated Universal Time)으로 반환합니다.|**datetime**|비결정적|  
  
###  <a name="GetDateandTimeParts"></a> 날짜 및 시간 부분을 반환하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *date* )|지정한 날짜에서 특정 *datepart*를 나타내는 문자열을 반환합니다.|**nvarchar**|비결정적|   
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *date* )|지정한 *date*에서 특정 *datepart*를 나타내는 정수를 반환합니다.|**ssNoversion**|비결정적|  
|[DAY](../../t-sql/functions/day-transact-sql.md)|DAY ( *date* )|지정한 *date*에서 일 부분을 나타내는 정수를 반환합니다.|**ssNoversion**|결정적|  
|[MONTH](../../t-sql/functions/month-transact-sql.md)|MONTH ( *date* )|지정한 *date*에서 월 부분을 나타내는 정수를 반환합니다.|**ssNoversion**|결정적|  
|[YEAR](../../t-sql/functions/year-transact-sql.md)|YEAR ( *date* )|지정한 *date*에서 연도 부분을 나타내는 정수를 반환합니다.|**ssNoversion**|결정적|  
  
###  <a name="fromParts"></a> 해당 부분에서 날짜 및 시간 값을 반환하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS  ( *year*, *month*, *day* )|지정된 년, 월, 일에 대한 **date** 값을 반환합니다.|**date**|결정적|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *precision*)|지정된 전체 자릿수를 사용하여 지정된 날짜 및 시간에 대한 **datetime2** 값을 반환합니다.|**datetime2(** _precision_ **)**|결정적|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *milliseconds*)|지정된 날짜 및 시간에 대한 **datetime** 값을 반환합니다.|**datetime**|결정적|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute*, *seconds*, *fractions*, *hour_offset*, *minute_offset*, *precision*)|지정된 오프셋 및 전체 자릿수를 사용하여 지정된 날짜 및 시간에 대한 **datetimeoffset** 값을 반환합니다.|**datetimeoffset(** _precision_ **)**|결정적|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS  ( *year*, *month*, *day*, *hour*, *minute* )|지정된 날짜 및 시간에 대한 **smalldatetime** 값을 반환합니다.|**smalldatetime**|결정적|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS  ( *hour*, *minute*, *seconds*, *fractions*, *precision* )|지정한 전체 자릿수를 사용하여 지정한 시간에 대한 **time** 값을 반환합니다.|**time(** _precision_ **)**|결정적|  
  
###  <a name="GetDateandTimeDifference"></a> 날짜 및 시간 차이 값을 반환하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|지정된 두 날짜 간에 교차되는 날짜 또는 시간 *datepart* 경계의 수를 반환합니다.|**ssNoversion**|결정적|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|지정된 두 날짜 간에 교차되는 날짜 또는 시간 *datepart* 경계의 수를 반환합니다.|**bigint**|결정적|  
  
###  <a name="ModifyDateandTimeValues"></a> 날짜 및 시간 값을 수정하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *number* , *date* )|지정된 *date*의 지정된 *datepart*에 간격을 더하여 새 **datetime** 값을 반환합니다.|*date* 인수의 데이터 형식|결정적|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH  ( *start_date* [, *month_to_add* ] )|선택 사항인 오프셋 옵션을 사용하여 지정한 날짜가 포함된 달의 마지막 날을 반환합니다.|반환 유형은 *start_date* 인수 형식이거나 **date** 데이터 형식입니다.|결정적|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|SWITCHOFFSET (*DATETIMEOFFSET* , *time_zone*)|SWITCHOFFSET은 DATETIMEOFFSET 값의 표준 시간대 오프셋을 변경하고 UTC 값을 유지합니다.|**datetimeoffset**을 *DATETIMEOFFSET*의 소수 자릿수로 표시|결정적|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expression* , *time_zone*)|TODATETIMEOFFSET은 datetime2 값을 datetimeoffset 값으로 변환합니다. *TODATETIMEOFFSET*은 datetime2 값을 지정된 time_zone의 현지 시간으로 해석합니다.|**datetimeoffset**을 *datetime* 인수의 소수 자릿수로 표시|결정적|  
  
###  <a name="SetorGetSessionFormatFunctions"></a> 세션 형식 함수를 설정 또는 반환하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|세션에 대한 SET DATEFIRST의 현재 값을 반환합니다.|**tinyint**|비결정적|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *number* &#124; * *@***number_var* }|일주일의 시작 요일을 1부터 7까지의 숫자로 설정합니다.|해당 사항 없음|해당 사항 없음|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *format* &#124; **@** _format_var_ }|**datetime** 또는 **smalldatetime** 데이터를 입력할 때 날짜 부분의 순서(월/일/년도)를 설정합니다.|해당 사항 없음|해당 사항 없음|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|현재 사용 중인 언어의 이름을 반환합니다. @@LANGUAGE는 날짜 또는 시간 함수가 아닙니다. 하지만 언어 설정은 날짜 함수의 출력에 영향을 줄 수 있습니다.|해당 사항 없음|해당 사항 없음|  
|[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE { [ N ] **'** _language_ **'** &#124; * *@***language_var* }|세션 및 시스템 메시지에 대한 언어 환경을 설정합니다. SET LANGUAGE는 날짜 또는 시간 함수가 아닙니다. 하지만 언어 설정은 날짜 함수의 출력에 영향을 줍니다.|해당 사항 없음|해당 사항 없음|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [ [ **@language =** ] **'** _language_ **'** ]|지원되는 모든 언어의 날짜 형식에 대한 정보를 반환합니다. **sp_helplanguage**는 날짜 또는 시간 저장 프로시저가 아닙니다. 하지만 언어 설정은 날짜 함수의 출력에 영향을 줍니다.|해당 사항 없음|해당 사항 없음|  
  
###  <a name="ValidateDateandTimeValues"></a> 날짜 및 시간 값 유효성 검사 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expression* )|**datetime** 또는 **smalldatetime** 입력 식이 유효한 날짜 또는 시간 값인지 여부를 확인합니다.|**ssNoversion**|ISDATE는 CONVERT 함수와 함께 사용되고 CONVERT 스타일 매개 변수가 지정되고 스타일이 0, 100, 9 또는 109가 아닌 경우에만 결정적입니다.|  
  
##  <a name="DateandTimeRelatedTopics"></a> 날짜 및 시간 관련 토픽 
  
|항목|설명|  
|-----------|-----------------|  
|[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|문자열 리터럴과 다른 날짜 및 시간 형식 간의 날짜/시간 값 변환에 대한 정보를 제공합니다.|  
|[국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하거나 여러 언어를 지원하는 데이터베이스 및 데이터베이스 애플리케이션의 언어 간 이식성에 대한 지침을 제공합니다.|  
|[ODBC 스칼라 함수 &#40;Transact-SQL&#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 사용할 수 있는 ODBC 스칼라 함수에 대한 정보를 제공합니다. 여기에는 ODBC 날짜 및 시간 함수가 포함됩니다.|  
|[AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|표준 시간대 변환 기능을 제공합니다.|  
  
## <a name="see-also"></a>관련 항목:
[함수](../../t-sql/functions/functions.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
