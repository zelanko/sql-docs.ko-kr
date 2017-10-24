---
title: "날짜 및 시간 데이터 형식 및 함수 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 79
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 7ce3baac7ec87ff3cad771234ab1196fb0a3855e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/06/2017

---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>날짜 및 시간 데이터 형식 및 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

이 항목의 다음 섹션에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 모든 날짜/시간 데이터 형식 및 함수에 대한 개요를 제공합니다.
-   [날짜 및 시간 데이터 형식](#DateandTimeDataTypes)  
-   [날짜 및 시간 함수](#DateandTimeFunctions)  
    -   [함수를 Get 시스템 날짜 및 시간 값](#GetSystemDateandTimeValues)  
    -   [날짜 함수 및 시간 부분](#GetDateandTimeParts)  
    -   [해당 부분에서 날짜 및 시간 값 가져오기 함수](#fromParts)  
    -   [날짜 함수 및 시간 차](#GetDateandTimeDifference)  
    -   [날짜를 수정 하는 함수 및 시간 값](#ModifyDateandTimeValues)  
    -   [세션 형식 함수를 가져오거나 설정 하는 함수](#SetorGetSessionFormatFunctions)  
    -   [날짜의 유효성을 검사 하는 함수 및 시간 값](#ValidateDateandTimeValues)  
-   [날짜 및 시간 관련 항목](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>날짜 및 시간 데이터 형식
[!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 데이터 형식이 다음 표에 나열 되어 있습니다.
  
|데이터 형식|형식|범위|정확도|저장소 크기(바이트)|사용자 정의 초 소수 부분 자릿수|표준 시간대 오프셋|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000부터 23:59:59.9999999까지|100나노초|3 ~ 5|예|아니요|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01부터 31.12.99까지|1일|3|아니요|아니요|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01부터 2079-06-06까지|1분|4|아니요|아니요|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01부터 9999-12-31까지|0.00333초|8|아니요|아니요|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000부터 9999-12-31 23:59:59.9999999까지|100나노초|6 ~ 8|예|아니요|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY-월-일 h:mm: ss [.nnnnnnn] [+ &#124;-] hh: mm|0001-01-01 00:00:00.0000000부터 9999-12-31 23:59:59.9999999까지(UTC)|100나노초|8 ~ 10|예|예|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) 데이터 형식이 날짜 또는 시간 데이터 형식 않습니다. **타임 스탬프** 에 대 한 사용 되지 않는 동의어 **rowversion**합니다.  
  
##  <a name="DateandTimeFunctions"></a>날짜 및 시간 함수  
다음 표에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 날짜 및 시간 함수가 나와 있습니다. 결정성에 대 한 자세한 내용은 참조 [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)합니다.
  
###  <a name="GetSystemDateandTimeValues"></a>시스템 날짜 및 시간 값 가져오기 함수 
모든 시스템 날짜 및 시간 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행 중인 컴퓨터 운영 체제에서 가져옵니다.
  
#### <a name="higher-precision-system-date-and-time-functions"></a>정밀도가 높은 시스템 날짜 및 시간 함수  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]GetSystemTimeAsFileTime() Windows API를 사용 하 여 날짜 및 시간 값을 가져옵니다. 정확도는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터의 하드웨어와 Windows 버전에 따라 달라집니다. 이 API의 정밀도는 100나노초로 고정됩니다. GetSystemTimeAdjustment() Windows API를 사용 하 여 정확도 확인할 수 있습니다.
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|반환 된 **datetime2 (7)** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 합니다. 여기에는 표준 시간대 오프셋이 포함되지 않습니다.|**datetime2(7)**|비결정적|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|반환 된 **(7)** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 합니다. 여기에는 표준 시간대 오프셋이 포함됩니다.|**(7)**|비결정적|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|반환 된 **datetime2 (7)** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 합니다. 날짜 및 시간이 UTC (협정 세계시) 시간으로 반환 됩니다.|**datetime2(7)**|비결정적|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>정밀도 낮은 시스템 날짜 및 시간 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|반환은 **datetime** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 있습니다. 여기에는 표준 시간대 오프셋이 포함되지 않습니다.|**datetime**|비결정적|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|반환은 **datetime** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 있습니다. 여기에는 표준 시간대 오프셋이 포함되지 않습니다.|**datetime**|비결정적|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|반환은 **datetime** 되는 컴퓨터의 시간과 날짜를 포함 하는 값의 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 되 고 있습니다. 날짜 및 시간이 UTC (협정 세계시) 시간으로 반환 됩니다.|**datetime**|비결정적|  
  
###  <a name="GetDateandTimeParts"></a>날짜 및 시간 부분 가져오기 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *날짜* )|지정 된을 나타내는 문자열을 반환 *datepart* 지정한 날짜의 합니다.|**nvarchar**|비결정적|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *날짜* )|지정 된을 나타내는 정수를 반환 *datepart* 는 지정 된 *날짜*합니다.|**int**|비결정적|  
|[일](../../t-sql/functions/day-transact-sql.md)|DAY ( *날짜* )|지정 된 날짜 부분을 나타내는 정수를 반환 *날짜*합니다.|**int**|결정적|  
|[월](../../t-sql/functions/month-transact-sql.md)|월 ( *날짜* )|지정 된의 월 부분을 나타내는 정수를 반환 *날짜*합니다.|**int**|결정적|  
|[연도](../../t-sql/functions/year-transact-sql.md)|연도 ( *날짜* )|지정 된 연도 부분을 나타내는 정수를 반환 *날짜*합니다.|**int**|결정적|  
  
###  <a name="fromParts"></a>해당 부분에서 날짜 및 시간 값 가져오기 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS ( *연도*, *월*, *일* )|반환 된 **날짜** 지정 된 연도, 월 및 일에 대 한 값입니다.|**date**|결정적|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS ( *연도*, *월*, *일*, *시간*, *분*, *초* , *분수*, *정밀도*)|반환 된 **datetime2** 지정한 전체 자릿수 하 고 지정 된 날짜 및 시간에 대 한 값입니다.|**datetime2 (** *정밀도* **)**|결정적|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS ( *연도*, *월*, *일*, *시간*, *분*, *초* , *밀리초*)|반환 된 **datetime** 지정 된 날짜 및 시간에 대 한 값입니다.|**datetime**|결정적|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS ( *연도*, *월*, *일*, *시간*, *분*,  *초*, *분수*, *hour_offset*, *minute_offset*, *정밀도*)|반환 된 **datetimeoffset** 고 지정 된 오프셋 및 전체 자릿수 지정 된 날짜 및 시간에 대 한 값입니다.|**datetime (** *정밀도* **)**|결정적|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS ( *연도*, *월*, *일*, *시간*, *분* )|반환 된 **smalldatetime** 지정 된 날짜 및 시간에 대 한 값입니다.|**smalldatetime**|결정적|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS ( *시간*, *분*, *초*, *분수*, *정밀도* )|반환 된 **시간** 지정한 전체 자릿수 하 고 지정된 된 시간에 대 한 값입니다.|**시간 (** *정밀도* **)**|결정적|  
  
###  <a name="GetDateandTimeDifference"></a>날짜 및 시간 차 가져오기 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|날짜 또는 시간 수를 반환 *datepart* 지정한 두 날짜 간에 겹쳐지는 합니다.|**int**|결정적|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|날짜 또는 시간 수를 반환 *datepart* 지정한 두 날짜 간에 겹쳐지는 합니다.|**bigint**|결정적|  
  
###  <a name="ModifyDateandTimeValues"></a>날짜 및 시간 값을 수정 하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *번호* , *날짜* )|새 반환 **datetime** 값을 지정 된 시간 간격을 더하여 *datepart* 는 지정 된 *날짜*합니다.|데이터 형식이 고 *날짜* 인수|결정적|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *start_date* [, *month_to_add* ])|선택 사항인 오프셋 옵션을 사용하여 지정한 날짜가 포함된 달의 마지막 날을 반환합니다.|반환 형식이 유형의 *start_date* 또는 **날짜**합니다.|결정적|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|스위치*오프셋* (*DATETIMEOFFSET* , *time_zone*)|스위치*오프셋* DATETIMEOFFSET 값의 표준 시간대 오프셋 변경 되 고 UTC 값을 유지 합니다.|**datetimeoffset** 의 소수 자릿수와는 *DATETIMEOFFSET*|결정적|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*식* , *time_zone*)|TODATETIMEOFFSET은 datetime2 값을 datetimeoffset 값으로 변환합니다. datetime2 값은 지정된 time_zone의 현지 시간으로 해석됩니다.|**datetimeoffset** 의 소수 자릿수와는 *datetime* 인수|결정적|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>함수를 가져오거나 세션 형식 설정
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|세션에 대한 SET DATEFIRST의 현재 값을 반환합니다.|**tinyint**|비결정적|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *번호* &#124;  **@**  *number_var* }|일주일의 시작 요일을 1부터 7까지의 숫자로 설정합니다.|해당 사항 없음|해당 사항 없음|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *형식* &#124;  **@**  *format_var* }|입력에 대 한 날짜 부분 (월/일/연도)의 순서를 설정 **datetime** 또는 **smalldatetime** 데이터입니다.|해당 사항 없음|해당 사항 없음|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|현재 사용 중인 언어의 이름을 반환합니다. @@LANGUAGE 날짜 또는 시간 함수가 아닙니다. 하지만 언어 설정은 날짜 함수의 출력에 영향을 줄 수 있습니다.|해당 사항 없음|해당 사항 없음|  
|[언어 설정](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {[N] **'***언어***'** &#124;  **@**  *language_var* }|세션 및 시스템 메시지에 대한 언어 환경을 설정합니다. SET LANGUAGE는 날짜 또는 시간 함수가 아닙니다. 하지만 언어 설정은 날짜 함수의 출력에 영향을 줍니다.|해당 사항 없음|해당 사항 없음|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [[  **@language =** ] **'***언어***'** ]|지원되는 모든 언어의 날짜 형식에 대한 정보를 반환합니다. **sp_helplanguage** 가 날짜 또는 시간 저장 프로시저입니다. 하지만 언어 설정은 날짜 함수의 출력에 영향을 줍니다.|해당 사항 없음|해당 사항 없음|  
  
###  <a name="ValidateDateandTimeValues"></a>날짜 및 시간 값의 유효성을 검사 하는 함수
  
|함수|구문|반환 값|반환 데이터 형식|결정성|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *식* )|결정 여부는 **datetime** 또는 **smalldatetime** 입력 식이 유효한 날짜 또는 시간 값입니다.|**int**|ISDATE는 CONVERT 함수와 함께 사용되고 CONVERT 스타일 매개 변수가 지정되고 스타일이 0, 100, 9 또는 109가 아닌 경우에만 결정적입니다.|  
  
##  <a name="DateandTimeRelatedTopics"></a>날짜 및 시간 관련 항목 
  
|항목|Description|  
|-----------|-----------------|  
|[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|문자열 리터럴과 다른 날짜 및 시간 형식 간의 날짜/시간 값 변환에 대한 정보를 제공합니다.|  
|[국가별 Transact-SQL 문 작성](../../relational-databases/collations/write-international-transact-sql-statements.md)|데이터베이스 및 사용 하는 데이터베이스 응용 프로그램의 이식성에 대 한 지침을 제공 [!INCLUDE[tsql](../../includes/tsql-md.md)] 다른 디렉터리로 또는 해당 언어 문을 여러 언어를 지원 합니다.|  
|[ODBC 스칼라 함수 &#40; Transact SQL &#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|사용할 수 있는 ODBC 스칼라 함수에 대 한 정보를 제공 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문. ODBC 날짜 및 시간 함수가 포함 됩니다.|  
|[표준 시간대 &AMP; #40; Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|표준 시간대 변환 기능을 제공 합니다.|  
  
## <a name="see-also"></a>참고 항목
[함수](../../t-sql/functions/functions.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

