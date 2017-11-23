---
title: datetimeoffset (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetimeoffset_TSQL
- datetimeoffset
dev_langs: TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b1b8fba166243143cd9ab8c03303fcfd7448e7a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

표준 시간대를 인식하며 24시간제를 기준으로 하는 시간과 결합된 날짜를 정의합니다.
  
## <a name="datetimeoffset-description"></a>datetimeoffset 설명
  
|속성|값|  
|---|---|
|구문|**datetimeoffset** [(*소수 자릿수 초의 전체 자릿수가*)]|  
|사용법|선언 @MyDatetimeoffset **(7)**<br /><br /> 테이블 Table1 만들기 (Column1 **(7)** )|  
|하위 클라이언트에 대해 사용되는 기본 문자열 리터럴 형식|YYYY-월-일 h:mm: ss [.nnnnnnn] [{+ &#124;-} hh: mm]<br /><br /> 자세한 내용은 뒷부분에 나오는 "하위 클라이언트에 대한 이전 버전과의 호환성" 섹션을 참조하세요.|  
|날짜 범위|0001-01-01부터 31.12.99까지<br /><br /> 1 년 1 월 1 일 CE에서 9999 년 12 월 31 일 까지의 CE|  
|시간 범위|00시: 00부터 23:59:59.9999999 (소수 자릿수 초는 Informatica에서 지원 되지 않음)|  
|표준 시간대 오프셋 범위|-14: 00부터 14:00 (Informatica에서 표준 시간대 오프셋은 무시 됨)|  
|요소 범위|YYYY는 0001에서 9999 사이에 속하는 4자리 숫자로, 연도를 나타냅니다.<br /><br /> MM은 01에서 12 사이에 속하는 두 자리 숫자로, 지정한 연도의 월을 나타냅니다.<br /><br /> DD는 월에 따라 01에서 31 사이에 속하는 두 자리 숫자로, 지정한 월의 일을 나타냅니다.<br /><br /> hh는 00에서 23 사이에 속하는 두 자리 숫자로, 시를 나타냅니다.<br /><br /> mm은 00에서 59 사이에 속하는 두 자리 숫자로, 분을 나타냅니다.<br /><br /> ss는 00에서 59 사이에 속하는 두 자리 숫자로, 초를 나타냅니다.<br /><br /> n*은 0에서 9999999 사이에 속하는 0부터 7 자리의 숫자로, 소수 자릿수 초를 나타냅니다. 소수 자릿수 초가 Informatica에서 지원 되지 않습니다.<br /><br /> hh는 -14에서 14 사이에 속하는 두 자리 숫자입니다. Informatica 표준 시간대 오프셋은 무시 됩니다.<br /><br /> mm은 00에서 59 사이에 속하는 두 자리 숫자입니다. Informatica 표준 시간대 오프셋은 무시 됩니다.|  
|문자 길이|최소 26 자리 (YYYY-월-일 h:mm: ss {+ &#124;-} hh: mm)부터 최대 34 (YYYY-ss.nnnnnnn {+ &#124;-} hh: mm)|  
|전체 자릿수, 소수 자릿수|아래 표를 참조 합니다.|  
|저장소 크기|초 소수 부분 자릿수 기본값 100ns를 기준으로 10바이트(고정)가 기본값입니다.|  
|정확도|100나노초|  
|기본값|1900-01-01 00:00:00 00:00|  
|달력|일반 달력|  
|사용자 정의 초 소수 부분 자릿수|예|  
|표준 시간대 오프셋 인식 및 유지|예|  
|일광 절약 시간제 인식|아니요|  
  
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
|**(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>Datetimeoffset의 지원 되는 문자열 리터럴 형식
다음 표에서 지원 되는 ISO 8601 문자열 리터럴 형식에 대 한 **datetimeoffset**합니다. 날짜 및 시간 부분에 대 한 영문자, 숫자, 구분 되지 않은 및 시간 형식에 대 한 내용은 **datetimeoffset**, 참조 [날짜 &#40; Transact SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) 및 [시간 &#40; Transact SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|YYYY-m M-DDThh:mm:ss [.nnnnnnn] [{+ &#124;-} hh: mm]|이 두 가지 형식은 SET LANGUAGE 및 SET DATEFORMAT 세션 로캘 설정의 영향을 받지 않습니다. 사이의 공백은 허용 되지 않습니다는 **datetimeoffset** 및 **datetime** 부분입니다.|  
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|ISO 정의 따른이 형식은 나타냅니다는 **datetime** 부분이 utc (협정 세계시)로 표현 해야 합니다. 예를 들어 1999-12-12 12:30:30.12345 -07:00는 1999-12-12 19:30:30.12345Z로 표시되어야 합니다.|  
  
## <a name="time-zone-offset"></a>표준 시간대 오프셋
표준 시간대 오프셋에 대 한 utc 표준 시간대 오프셋을 지정 된 **시간** 또는 **datetime** 값입니다. 표준 시간대 오프셋은 [+|-] hh:mm:으로 나타낼 수 있습니다.
-   hh는 0에서 14 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 시간(시간)을 나타냅니다.  
-   mm은 00에서 59 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 추가 시간(분)을 나타냅니다.  
-   \+(더하기) 또는-(빼기)는 표준 시간대 오프셋의 필수 기호입니다. 이는 현지 시간을 가져오기 위해 UTC 시간에서 표준 시간대 오프셋을 더했는지 또는 뺐는지를 나타냅니다. 올바른 표준 시간대 오프셋 범위는 -14:00에서 +14:00 사이입니다.  
  
표준 시간대 범위는 XSD 스키마 정의에 대한 W3C XML 표준을 따르며 12:59에서 +14:00 사이인 SQL 2003 표준 정의와 약간 다릅니다.
  
선택적 형식 매개 변수 *소수 자릿수 초의 전체 자릿수가* 는 초의 소수 부분에 대 한 자릿수를 지정 합니다. 이 값은 0에서 7 사이의 정수입니다(100나노초). 기본 *소수 자릿수 초의 전체 자릿수가* 은 100ns (초의 소수 부분의 자릿수가 7 자리).
  
데이터는 데이터베이스에 저장되며 UTC에서와 마찬가지로 서버에서 처리, 비교, 정렬 및 인덱싱됩니다. 표준 시간대 오프셋은 검색할 수 있도록 데이터베이스에 유지됩니다.
  
지정 된 표준 시간대 오프셋 DST 일광 절약 시간제 ()을 인식 하며 지정 된 모든 작업에 대 한 조정 된 것으로 간주 됩니다 **datetime** DST 기간에 있습니다.
  
에 대 한 **datetimeoffset** UTC 및 영구 또는 변환 표준 시간대 오프셋) (에 로컬 입력 **datetime** 값 삽입, 업데이트, 산술, convert 또는 할당 작업 중 유효성을 검사 합니다. 잘못 된 UTC 나 영구 또는 변환 표준 시간대 오프셋) (에 로컬 감지 **datetime** 값에서 잘못 된 값 오류가 발생 합니다. 예를 들어 9999-12-31 10:10:00는 UTC에서 유효하지만 표준 시간대 오프셋 +13:50에 대한 현지 시간에서는 오버플로됩니다.
  
해당 날짜를 변환 하려면 **datetimeoffset** 대상 표준 시간대 값 참조 [AT TIME ZONE &#40; Transact SQL &#41; ](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 및 ISO 8601 호환성  
ANSI 및 ISO 8601 호환성 섹션의 [날짜](../../t-sql/data-types/date-transact-sql.md) 및 [시간](../../t-sql/data-types/time-transact-sql.md) 항목에 적용 **datetimeoffset**합니다.
  
## <a name="backward-compatibility-for-down-level-clients"></a>하위 클라이언트에 대 한 이전 버전과 호환성
일부 하위 수준 클라이언트 지원 하지 않습니다는 **시간**, **날짜**, **datetime2** 및 **datetimeoffset** 데이터 형식입니다. 다음 표에서는 상위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 하위 클라이언트 간 형식 매핑을 보여 줍니다.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|하위 클라이언트에 전달된 기본 문자열 리터럴 형식|하위 수준 ODBC|하위 수준 OLEDB|하위 수준 JDBC|하위 수준 SQLCLIENT|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetimeoffset**|YYYY-월-일 h:mm: ss [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
  
## <a name="converting-date-and-time-data"></a>날짜 및 시간 데이터를 변환합니다.
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터와 함께 CAST 및 CONVERT 함수를 사용 하는 방법에 대 한 정보를 참조 하십시오. [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
변환할 때 **날짜**, 연도, 월 및 일이 복사 됩니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `date` 값으로 변환한 결과를 보여 줍니다.  
  
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
  
변환 하려는 경우 **time (n)**, 우리의 분, 초 및 소수 자릿수 초가 복사 됩니다. 표준 시간대 값은 잘립니다. 때 전체 자릿수는 **datetimeoffset (n)** 값의 전체 자릿수 보다 크면는 **time (n)** 값, 값 반올림 됩니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `time(3)` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환할 때**datetime**, 날짜 및 시간 값이 복사 되 고 표준 시간대는 잘립니다. 때의 소수 자릿수는 **datetimeoffset (n)** 값이 세 자리 보다 크면, 해당 값이 잘립니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환에 대 한 **smalldatetime**, 날짜 및 시간이 복사 됩니다. 초 값에 따라 분이 반올림되고 초가 0으로 설정됩니다. 다음 코드에서는 `datetimeoffset(3)` 값을 `smalldatetime` 값으로 변환한 결과를 보여 줍니다.  
  
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
  
변환 하려는 경우 **datetime2(n)**, 날짜 및 시간에 복사 됩니다는 **datetime2** 값 및 표준 시간대는 잘립니다. 때 전체 자릿수는 **datetime2(n)** 값의 전체 자릿수 보다 크면는 **datetimeoffset (n)** 값, 소수 자릿수 초가에 맞게 잘립니다. 다음 코드에서는 `datetimeoffset(4)` 값을 `datetime2(3)` 값으로 변환한 결과를 보여 줍니다.
  
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
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>Datetimeoffset 데이터 형식을 다른 날짜 및 시간 형식으로 변환
다음 표에서 발생 하는 상황을 설명 때는 **datetimeoffset** 데이터 형식을 다른 날짜 및 시간 데이터 형식으로 변환 됩니다.
  
### <a name="converting-string-literals-to-datetimeoffset"></a>문자열 리터럴을 datetimeoffset으로 변환
문자열에 포함된 모든 부분의 형식이 올바른 경우 문자열 리터럴에서 날짜/시간 유형으로 변환할 수 있습니다. 그렇지 않으면 런타임 오류가 발생합니다. 날짜/시간 유형에서 문자열 리터럴로의 암시적 변환 또는 명시적 변환에 스타일을 지정하지 않은 경우 현재 세션의 기본 형식이 지정됩니다. 다음 표에서 문자열을 변환 하기 위한 규칙 리터럴을 **datetimeoffset** 데이터 형식입니다.
  
|입력 문자열 리터럴|**datetimeoffset (n)**|  
|---|---|
|ODBC DATE|ODBC 문자열 리터럴에 매핑되는 **datetime** 데이터 형식입니다. 모든 할당 연산에 ODBC DATETIME 리터럴에서 **datetimeoffset** 형식 간에 암시적 변환이 발생 합니다 **datetime** 과 이러한 형식 변환 규칙으로 정의 된 대로 합니다.|  
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
다음 예제에서는 문자열을 각각 캐스팅 한 결과를 비교 **날짜** 및 **시간** 데이터 형식입니다.
  
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
|**날짜**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**날짜/시간**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**Datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[표준 시간대 &AMP;#40; Transact SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  
