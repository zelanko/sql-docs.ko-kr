---
title: datetime2 (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetime2
- datetime2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- dates [SQL Server], data types
- date and time [SQL Server], datetime2
- data types [SQL Server], date and time
- datetime2 data type [SQL Server]
ms.assetid: 868017f3-214f-43ef-8536-cc1632a2288f
caps.latest.revision: 58
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13766b3d0cb86780c2eca55c7f36e8fd16e973c5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2-transact-sql"></a>datetime2(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

24시간제 기준의 시간과 결합된 날짜를 정의합니다. **datetime2** 기존의 확장으로 간주할 수 있는 **datetime** 형식에 더 큰 날짜 범위, 더 큰 기본 소수 자릿수 및 선택적 사용자 지정 전체 자릿수입니다.
  
## <a name="datetime2-description"></a>datetime2 설명
  
|속성|값|  
|--------------|-----------|  
|구문|**datetime2** [(*소수 자릿수 초의 전체 자릿수가*)]|  
|사용법|선언 @MyDatetime2 **datetime2 (7)**<br /><br /> 테이블 Table1 만들기 (Column1 **datetime2 (7)** )|  
|기본 문자열 리터럴 형식<br /><br /> (하위 클라이언트에 대해 사용됨)|YYYY-MM-DD hh:mm:ss[.소수 자릿수 초]<br /><br /> 자세한 내용은 뒷부분에 나오는 "하위 클라이언트에 대한 이전 버전과의 호환성" 섹션을 참조하세요.|  
|날짜 범위|0001-01-01부터 31.12.99까지<br /><br /> 1 월 1, 1 CE에서 9999 년 12 월 31 일 까지의 CE|  
|시간 범위|00:00:00부터 23:59:59.9999999까지|  
|표준 시간대 오프셋 범위|없음|  
|요소 범위|YYYY는 0001에서 9999 사이에 속하는 4자리 숫자로, 연도를 나타냅니다.<br /><br /> MM은 01에서 12 사이에 속하는 두 자리 숫자로, 지정된 연도의 월을 나타냅니다.<br /><br /> DD는 월에 따라 01에서 31 사이에 속하는 두 자리 숫자로, 특정 월의 일을 나타냅니다.<br /><br /> hh는 00에서 23 사이에 속하는 두 자리 숫자로, 시간을 나타냅니다.<br /><br /> Mm은 00에서 59 사이에 속하는 두 자리 숫자로, 분을 나타냅니다.<br /><br /> ss는 00에서 59 사이에 속하는 두 자리 숫자로, 초를 나타냅니다.<br /><br /> n*은 0에서 9999999 사이에 속하는 0 ~ 7 자리의 숫자로, 소수 자릿수 초를 나타냅니다. Informatica에서 소수 자릿수 초가 잘립니다 n > 3.|  
|문자 길이|최소 19자리(YYYY-MM-DD hh:mm:ss )부터 최대 27자리(YYYY-MM-DD hh:mm:ss.0000000)까지|  
|전체 자릿수, 소수 자릿수|0 ~ 7자리, 정확도 100ns. 기본 전체 자릿수는 7자리입니다.|  
|저장소 크기|전체 자릿수가 3 미만인 경우 6바이트, 3 및 4인 경우 7바이트, 기타 모든 전체 자릿수의 경우 8바이트가 필요합니다.|  
|정확도|100나노초|  
|기본값|1900-01-01 00:00:00|  
|달력|일반 달력|  
|사용자 정의 초 소수 부분 자릿수|예|  
|표준 시간대 오프셋 인식 및 유지|아니요|  
|일광 절약 시간제 인식|아니요|  
  
데이터 형식 메타 데이터에 대 한 참조 [sys.systypes &#40; Transact SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md) 또는 [TYPEPROPERTY &#40; Transact SQL &#41; ](../../t-sql/functions/typeproperty-transact-sql.md). 일부 날짜 및 시간 데이터 형식의 경우 전체 자릿수와 소수 자릿수는 변할 수 있습니다. 전체 자릿수와 소수 자릿수는 열에 대 한을 가져오려면 참조 [COLUMNPROPERTY &#40; Transact SQL &#41; ](../../t-sql/functions/columnproperty-transact-sql.md), [COL_LENGTH &#40; Transact SQL &#41; ](../../t-sql/functions/col-length-transact-sql.md), 또는 [sys.columns&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>Datetime2에 대 한 지원 되는 문자열 리터럴 형식
다음 표에 나열 된 지원 되는 ISO 8601 및 ODBC 문자열 리터럴 형식에 대 한 **datetime2**합니다. 날짜 및 시간 부분에 대 한 영문자, 숫자, 구분 되지 않은 및 시간 형식에 대 한 내용은 **datetime2**, 참조 [날짜 &#40; Transact SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) 및 [시간 &#40; Transact SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|설명|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> YYYY-MM-DDThh:mm:ss[.nnnnnnn]|이 형식은 SET LANGUAGE 및 SET DATEFORMAT 세션 로캘 설정의 영향을 받지 않습니다. **T**, 콜론 (:) 및 마침표 (.) 문자열에 포함 됩니다는 리터럴, 예: ' 2007-05-02T19:58:47.1234567'.|  
  
|ODBC|Description|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.소수 자릿수 초]' }|ODBC API 사양:<br /><br /> 소수 자릿수 초를 나타내는 소수점 오른쪽 자릿수는 0에서 최대 7(100나노초)까지 지정할 수 있습니다.|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 및 ISO 8601 호환성  
ANSI 및 ISO 8601 호환성 [날짜](../../t-sql/data-types/date-transact-sql.md) 및 [시간](../../t-sql/data-types/time-transact-sql.md) 적용할 **datetime2**합니다.
  
##  <a name="backward-compatibility-for-down-level-clients"></a>하위 클라이언트에 대한 이전 버전과의 호환성  
일부 하위 수준 클라이언트 지원 하지 않습니다는 **시간**, **날짜**, **datetime2** 및 **datetimeoffset** 데이터 형식입니다. 다음 표에서는 상위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 하위 클라이언트 간 형식 매핑을 보여 줍니다.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|하위 클라이언트에 전달된 기본 문자열 리터럴 형식|하위 수준 ODBC|하위 수준 OLEDB|하위 수준 JDBC|하위 수준 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetimeoffset**|YYYY-월-일 h:mm: ss [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
  
## <a name="converting-date-and-time-data"></a>날짜 및 시간 데이터를 변환합니다.
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터와 함께 CAST 및 CONVERT 함수를 사용 하는 방법에 대 한 정보를 참조 하십시오. [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>다른 날짜 / 시간 형식 datetime2 데이터 형식으로 변환합니다.
이 섹션에서는 다른 날짜 / 시간 데이터 형식으로 변환할 때 발생 하는 상황을 설명는 **datetime2** 데이터 형식입니다.  
  
변환은에서 **날짜**, 년, 월 및 일이 복사 됩니다.  시간 구성 요소 이며로 설정 됩니다.  다음 코드에서는 `date` 값을 `datetime2` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
변환은에서 **time (n)**, 시간 구성 요소가 복사 되 고로 설정 되어 날짜 구성 요소가 ' 1900-01-01'. 다음 예에서는 `time(7)` 값을 `datetime2` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
변환은에서 **smalldatetime**, 시간 및 분이 복사 됩니다. 초 및 소수 자릿수 초는 0으로 설정됩니다. 다음 코드에서는 `smalldatetime` 값을 `datetime2` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
변환은에서 **datetimeoffset (n)**, 날짜 및 시간 구성 요소가 복사 됩니다. 표준 시간대는 잘립니다. 다음 예에서는 `datetimeoffset(7)` 값을 `datetime2` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

변환은에서 **datetime**, 날짜 및 시간이 복사 됩니다.  소수 자릿수는 7 자리까지 확장 됩니다.  다음 예에서는 `datetime` 값을 `datetime2` 값으로 변환한 결과를 보여 줍니다.

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  
  
### <a name="converting-string-literals-to-datetime2"></a>문자열 리터럴을 datetime2로 변환  
문자열에 포함된 모든 부분의 형식이 올바른 경우 문자열 리터럴에서 날짜/시간 유형으로 변환할 수 있습니다. 그렇지 않으면 런타임 오류가 발생합니다. 날짜/시간 유형에서 문자열 리터럴로의 암시적 변환 또는 명시적 변환에 스타일을 지정하지 않은 경우 현재 세션의 기본 형식이 지정됩니다. 다음 표에서 문자열을 변환 하기 위한 규칙 리터럴을 **datetime2** 데이터 형식입니다.
  
|입력 문자열 리터럴|**datetime2(n)**|  
|---|---|
|ODBC DATE|ODBC 문자열 리터럴에 매핑되는 **datetime** 데이터 형식입니다. 모든 할당 연산에 ODBC DATETIME 리터럴에서 **datetime2** 형식 간에 암시적 변환이 발생 합니다 **datetime** 과 이러한 형식 변환 규칙으로 정의 된 대로 합니다.|  
|ODBC TIME|이전 ODBC DATE 규칙을 참조하세요.|  
|ODBC DATETIME|이전 ODBC DATE 규칙을 참조하세요.|  
|DATE만|TIME 부분의 기본값은 00:00:00입니다.|  
|TIME만|DATE 부분의 기본값은 1900-1-1입니다.|  
|TIMEZONE만|기본값이 제공됩니다.|  
|DATE+TIME|중요하지 않음|  
|DATE+TIMEZONE|허용되지 않습니다.|  
|TIME+TIMEZONE|DATE 부분의 기본값은 1900-1-1입니다. TIMEZONE 입력은 무시됩니다.|  
|DATE+TIME+TIMEZONE|로컬 DATETIME이 사용됩니다.|  
  
## <a name="examples"></a>예  
다음 예제에서는 문자열을 각각 캐스팅 한 결과를 비교 **날짜** 및 **시간** 데이터 형식입니다.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|데이터 형식|출력|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

