---
title: datetimeoffset(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- datetimeoffset_TSQL
- datetimeoffset
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74ab6c88467b20299574003c17fd96ac563dbc25
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502585"
---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

표준 시간대를 인식하며 24시간제를 기준으로 하는 시간과 결합된 날짜를 정의합니다.
  
## <a name="datetimeoffset-description"></a>datetimeoffset 설명
  
|속성|값|  
|---|---|
|구문|**datetimeoffset** [ (*초 소수 부분 자릿수*) ]|  
|사용법|DECLARE \@MyDatetimeoffset **datetimeoffset(7)**<br /><br /> CREATE TABLE Table1( Column1 **datetimeoffset(7)** )|  
|하위 클라이언트에 대해 사용되는 기본 문자열 리터럴 형식|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+&#124;-}hh:mm]<br /><br /> 자세한 내용은 뒷부분에 나오는 "하위 클라이언트에 대한 이전 버전과의 호환성" 섹션을 참조하세요.|  
|날짜 범위|0001-01-01부터 31.12.99까지<br /><br /> CE 1년 1월 1일부터 CE 9999년 12월 31일까지|  
|시간 범위|00:00:00부터 23:59:59.9999999까지(Informatica에서는 초 소수 부분이 지원되지 않음)|  
|표준 시간대 오프셋 범위|-14:00부터 +14:00(Informatica에서는 표준 시간대 오프셋이 무시됨)|  
|요소 범위|YYYY는 0001에서 9999 사이에 속하는 4자리 숫자로, 연도를 나타냅니다.<br /><br /> MM은 01에서 12 사이에 속하는 두 자리 숫자로, 지정한 연도의 월을 나타냅니다.<br /><br /> DD는 월에 따라 01에서 31 사이에 속하는 두 자리 숫자로, 지정한 월의 일을 나타냅니다.<br /><br /> hh는 00에서 23 사이에 속하는 두 자리 숫자로, 시를 나타냅니다.<br /><br /> mm은 00에서 59 사이에 속하는 두 자리 숫자로, 분을 나타냅니다.<br /><br /> ss는 00에서 59 사이에 속하는 두 자리 숫자로, 초를 나타냅니다.<br /><br /> n*은 0에서 9999999 사이에 속하는 0부터 7 자리의 숫자로, 소수 자릿수 초를 나타냅니다. Informatica에서는 초 소수 부분이 지원되지 않습니다.<br /><br /> hh는 -14에서 14 사이에 속하는 두 자리 숫자입니다. Informatica에서는 표준 시간대 오프셋이 무시됩니다.<br /><br /> mm은 00에서 59 사이에 속하는 두 자리 숫자입니다. Informatica에서는 표준 시간대 오프셋이 무시됩니다.|  
|문자 길이|최소 26자리(YYYY-MM-DD hh:mm:ss {+&#124;-}hh:mm)부터 최대 34자리(YYYY-MM-DD hh:mm:ss.nnnnnnn {+&#124;-}hh:mm)까지|  
|전체 자릿수, 소수 자릿수|아래 표를 참조하세요.|  
|스토리지 크기|초 소수 부분 자릿수 기본값 100ns를 기준으로 10바이트(고정)가 기본값입니다.|  
|정확도|100나노초|  
|기본값|1900-01-01 00:00:00 00:00|  
|달력|일반 달력|  
|사용자 정의 초 소수 부분 자릿수|예|  
|표준 시간대 오프셋 인식 및 유지|예|  
|일광 절약 시간제 인식|아니오|  
  
|지정한 소수 자릿수|결과(전체 자릿수, 소수 자릿수)|열 길이(바이트)|소수 자릿수 초의 전체 자릿수|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**datetimeoffset(0)**|(26,0)|8|0-2|  
|**datetimeoffset(1)**|(28,1)|8|0-2|  
|**datetimeoffset(2)**|(29,2)|8|0-2|  
|**datetimeoffset(3)**|(30,3)|9|3-4|  
|**datetimeoffset(4)**|(31,4)|9|3-4|  
|**datetimeoffset(5)**|(32,5)|10|5-7|  
|**datetimeoffset(6)**|(33,6)|10|5-7|  
|**datetimeoffset(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>datetimeoffset에 대해 지원되는 문자열 리터럴 형식
다음 표에는 **datetimeoffset**에 대해 지원되는 ISO 8601 문자열 리터럴 형식이 나와 있습니다. **datetimeoffset**의 날짜 및 시간 부분에 대한 영문자, 숫자, 시간 및 구분되지 않은 시간 형식에 대한 내용은 [date&#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md) 및 [time&#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)을 참조하세요.
  
|ISO 8601|설명|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn][{+&#124;-}hh:mm]|이 두 가지 형식은 SET LANGUAGE 및 SET DATEFORMAT 세션 로캘 설정의 영향을 받지 않습니다. **datetimeoffset**과 **datetime** 부분 사이에는 공백이 허용되지 않습니다.|  
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|ISO 정의에 따른 이 형식은 **datetime** 부분이 UTC(Coordinated Universal Time)로 표현되어야 함을 나타냅니다. 예를 들어 1999-12-12 12:30:30.12345 -07:00는 1999-12-12 19:30:30.12345Z로 표시되어야 합니다.|  
  
## <a name="time-zone-offset"></a>표준 시간대 오프셋
표준 시간대 오프셋은 **time** 또는 **datetime** 값에 대한 UTC로부터의 시간대 오프셋을 지정합니다. 표준 시간대 오프셋은 [+|-] hh:mm:으로 나타낼 수 있습니다.
-   hh는 0에서 14 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 시간(시간)을 나타냅니다.  
-   mm은 00에서 59 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 추가 시간(분)을 나타냅니다.  
-   \+(더하기) 또는 -(빼기)는 표준 시간대 오프셋의 필수 기호입니다. 이는 현지 시간을 가져오기 위해 UTC 시간에서 표준 시간대 오프셋을 더했는지 또는 뺐는지를 나타냅니다. 올바른 표준 시간대 오프셋 범위는 -14:00에서 +14:00 사이입니다.  
  
표준 시간대 범위는 XSD 스키마 정의에 대한 W3C XML 표준을 따르며 12:59에서 +14:00 사이인 SQL 2003 표준 정의와 약간 다릅니다.
  
선택적 유형 매개 변수인 *초 소수 부분 자릿수*는 초의 소수 부분의 자릿수를 지정합니다. 이 값은 0에서 7 사이의 정수입니다(100나노초). 기본 *초 소수 부분 자릿수*는 100ns입니다(초의 소수 부분 자릿수가 7자리임).
  
데이터는 데이터베이스에 저장되며 UTC에서와 마찬가지로 서버에서 처리, 비교, 정렬 및 인덱싱됩니다. 표준 시간대 오프셋은 검색할 수 있도록 데이터베이스에 유지됩니다.
  
지정된 표준 시간대 오프셋은 DST(일광 절약 시간제)를 인식하고, DST 기간에 있는 모든 **datetime**에 대해 조정할 수 있는 것으로 간주됩니다.
  
**datetimeoffset** 형식의 경우 UTC 및 영구 또는 변환 표준 시간대 오프셋에 대한 현지 **datetime** 값에 대해 삽입, 업데이트, 산술, 변환 또는 할당 작업 중 유효성 검사가 수행됩니다. 잘못된 UTC나 영구 또는 변환 표준 시간대 오프셋에 대한 현지 **datetime** 값이 인식되면 잘못된 값 오류가 발생합니다. 예를 들어 9999-12-31 10:10:00는 UTC에서 유효하지만 표준 시간대 오프셋 +13:50에 대한 현지 시간에서는 오버플로됩니다.
  
날짜를 대상 시간대의 해당 **datetimeoffset** 값으로 변환하려면 [AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)을 참조하십시오.
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 및 ISO 8601 호환성  
[date](../../t-sql/data-types/date-transact-sql.md) 및 [time](../../t-sql/data-types/time-transact-sql.md) 항목의 ANSI 및 ISO 8601 호환성 섹션이 **datetimeoffset**에 적용됩니다.
  
## <a name="backward-compatibility-for-down-level-clients"></a>하위 클라이언트에 대한 이전 버전과의 호환성
일부 하위 클라이언트는 **time**, **date**, **datetime2** 및 **datetimeoffset** 데이터 형식을 지원하지 않습니다. 다음 표에서는 상위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 하위 클라이언트 간 형식 매핑을 보여 줍니다.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|하위 클라이언트에 전달된 기본 문자열 리터럴 형식|하위 수준 ODBC|하위 수준 OLEDB|하위 수준 JDBC|하위 수준 SQLCLIENT|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
  
## <a name="converting-date-and-time-data"></a>date 및 time 데이터 변환
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터에 CAST 및 CONVERT 함수를 사용하는 방법은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>datetimeoffset 데이터 형식을 다른 날짜 및 시간 형식으로 변환
이 섹션에서는 **datetimeoffset** 데이터 형식이 다른 날짜 및 시간 데이터 형식으로 변환될 때 어떤 상황이 발생하는지를 설명합니다.
  
**date**으로 변환하는 경우 년, 월, 일이 복사됩니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `date` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10 +01:00';  
DECLARE @date date= @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @date AS 'date';  
  
--Result  
--@datetimeoffset                date  
-------------------------------- ----------  
--2025-12-10 12:32:10.0000 +01:0 2025-12-10  
--  
--(1 row(s) affected)  
  
```  
  
**time(n)** 으로 변환하는 경우 시, 분, 초, 초 소수 부분 자릿수가 복사됩니다. 표준 시간대 값은 잘립니다. **datetimeoffset(n)** 값의 전체 자릿수가 **time(n)** 값의 전체 자릿수보다 큰 경우 값이 반올림됩니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `time(3)` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @time time(3) = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @time AS 'time';  
  
--Result  
--@datetimeoffset                time  
-------------------------------- ------------  
-- 2025-12-10 12:32:10.1237 +01:00    12:32:10.124  
  
--  
--(1 row(s) affected)  
  
```  
  
**datetime**으로 변환하는 경우 날짜 및 시간 값이 복사되고 표준 시간대는 잘립니다. **datetimeoffset(n)** 값의 소수 자릿수가 세 자리보다 크면 값이 잘립니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @datetime AS 'datetime';  
  
--Result  
--@datetimeoffset                datetime  
-------------------------------- -----------------------  
--2025-12-10 12:32:10.1237 +01:0 2025-12-10 12:32:10.123  
--  
--(1 row(s) affected)  
```  
  
**smalldatetime**으로 변환하는 경우 날짜와 시간이 복사됩니다. 초 값에 따라 분이 반올림되고 초가 0으로 설정됩니다. 다음 코드에서는 `datetimeoffset(3)` 값을 `smalldatetime` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(3) = '1912-10-25 12:24:32 +10:0';  
DECLARE @smalldatetime smalldatetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetimeoffset                @smalldatetime  
-------------------------------- -----------------------  
--1912-10-25 12:24:32.000 +10:00 1912-10-25 12:25:00  
--  
--(1 row(s) affected)  
```  
  
**datetime2(n)** 로 변환하는 경우 날짜 및 시간이 **datetime2** 값으로 복사되고 시간대는 잘립니다. **datetime2(n)** 값의 전체 자릿수가 **datetimeoffset(n)** 값의 전체 자릿수보다 크면 초 소수 부분이 이에 맞게 잘립니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `datetime2(3)` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1912-10-25 12:24:32.1277 +10:0';  
DECLARE @datetime2 datetime2(3)=@datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @datetime2 AS '@datetime2';  
  
--Result  
@datetimeoffset                    @datetime2  
---------------------------------- ----------------------  
1912-10-25 12:24:32.1277 +10:00    1912-10-25 12:24:32.12  
  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-datetimeoffset"></a>문자열 리터럴을 datetimeoffset으로 변환
문자열에 포함된 모든 부분의 형식이 올바른 경우 문자열 리터럴에서 날짜/시간 유형으로 변환할 수 있습니다. 그렇지 않으면 런타임 오류가 발생합니다. 날짜/시간 유형에서 문자열 리터럴로의 암시적 변환 또는 명시적 변환에 스타일을 지정하지 않은 경우 현재 세션의 기본 형식이 지정됩니다. 다음 표에서는 문자열 리터럴을 **datetimeoffset** 데이터 형식으로 변환하는 규칙을 보여 줍니다.
  
|입력 문자열 리터럴|**datetimeoffset(n)**|  
|---|---|
|ODBC DATE|ODBC 문자열 리터럴은 **datetime** 데이터 형식으로 매핑됩니다. ODBC DATETIME 리터럴에서 **datetimeoffset** 형식으로 할당하면 변환 규칙으로 정의된 대로 **datetime**과 이러한 형식 간에 암시적 변환이 발생합니다.|  
|ODBC TIME|이전 ODBC DATE 규칙을 참조하세요.|  
|ODBC DATETIME|이전 ODBC DATE 규칙을 참조하세요.|  
|DATE만|TIME 부분의 기본값은 00:00:00입니다. TIMEZONE의 기본값은 +00:00입니다.|  
|TIME만|DATE 부분의 기본값은 1900-1-1입니다. TIMEZONE의 기본값은 +00:00입니다.|  
|TIMEZONE만|기본값이 제공됩니다.|  
|DATE+TIME|TIMEZONE의 기본값은 +00:00입니다.|  
|DATE+TIMEZONE|허용 안 됨|  
|TIME+TIMEZONE|DATE 부분의 기본값은 1900-1-1입니다.|  
|DATE+TIME+TIMEZONE|중요하지 않음|  
  
## <a name="examples"></a>예  
다음 예에서는 문자열을 각 **date** 및 **time** 데이터 형식으로 캐스팅하는 결과를 비교합니다.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset'  
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetimeoffset(7)) AS  
        'datetimeoffset IS08601';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|데이터 형식|출력|  
|---|---|
|**Time**|12:35:29. 1234567|  
|**Date**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**날짜/시간**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**Datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[AT TIME ZONE&#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  
