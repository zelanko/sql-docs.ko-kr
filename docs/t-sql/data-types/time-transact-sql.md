---
title: "시간 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- time_TSQL
- time
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- time [SQL Server]
- date and time [SQL Server], time
- data types [SQL Server], date and time
- time data type [SQL Server]
ms.assetid: 30a6c681-8190-48e4-94d0-78182290a402
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: b6d6655b1640eff66182c78ea919849194d9714c
ms.openlocfilehash: fc0a9e68c9dc3ad664a4f091b73b073038c7f4c1
ms.contentlocale: ko-kr
ms.lasthandoff: 10/05/2017

---
# <a name="time-transact-sql"></a>time(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  시간을 정의합니다. 시간은 표준 시간대를 인식하지 않으며 24시간제를 기준으로 합니다.  
  
  > [!NOTE]  
  > Informatica 커넥터를 사용 하는 PDW 고객 Informatica 정보가 제공 됩니다. 
  
## <a name="time-description"></a>time 설명  
  
|속성|값|  
|--------------|-----------|  
|구문|**시간** [(*소수 두 번째 눈금*)]|  
|사용법|선언 @MyTime **time (7)**<br /><br /> 테이블 Table1 만들기 (Column1 **time (7)** )|  
|*소수 자릿수 초의*|초의 소수 부분 자릿수를 지정합니다.<br /><br /> 0에서 7 사이의 정수를 지정할 수 있습니다. Informatica에 대 한이 0에서 3 사이의 정수를 수 있습니다.<br /><br /> 기본 소수 자릿수 소수 자릿수는 7 (100ns)입니다.|  
|기본 문자열 리터럴 형식<br /><br /> (하위 클라이언트에 대해 사용됨)|h:mm: ss [.nnnnnnn] (h:mm: ss [.nnn] Informatica)<br /><br /> 자세한 내용은 뒷부분에 나오는 "하위 클라이언트에 대한 이전 버전과의 호환성" 섹션을 참조하세요.|  
|범위|23:59:59.9999999 (00:00:00.000 23:59:59.999 Informatica에 대 한를 통해)를 통해 이며|  
|요소 범위|hh는 0에서 23 사이에 속하는 두 자리 숫자로, 시를 나타냅니다.<br /><br /> mm은 0에서 59 사이에 속하는 두 자리 숫자로, 분을 나타냅니다.<br /><br /> ss는 0에서 59 사이에 속하는 두 자리 숫자로, 초를 나타냅니다.<br /><br /> n\*7 자리의 숫자로, 소수 자릿수 초를 나타내는 9999999 사이에 속하는 0에서 사이의 0이 됩니다. Informatica에 대 한 n\* 세 자리 숫자로, 0에서 999 사이의 0이 됩니다.|  
|문자 길이|최소 8 자리 (hh: mm:)를 최대 16 (hh:mm:ss.nnnnnnn). Informatica에 대 한 최대값은 12 (hh:mm:ss.nnn).|  
|전체 자릿수, 소수 자릿수<br /><br /> (사용자는 소수 자릿수만 지정)|아래 표를 참조 합니다.|  
|저장소 크기|초 소수 부분 자릿수 기본값 100ns를 기준으로 5바이트(고정)가 기본값입니다. Informatica, 기본값은 4 바이트를 1ms 소수 자릿수의 기본값 고정 정밀도 두 번째입니다.|  
|정확도|100 나노초 (Informatica에 1 밀리초)|  
|기본값|00:00:00<br /><br /> 이 값은 암시적으로 변환에 대 한 추가 되는 시간 부분에 대 한 사용 **날짜** 를 **datetime2** 또는 **datetimeoffset**합니다.|  
|사용자 정의 초 소수 부분 자릿수|예|  
|표준 시간대 오프셋 인식 및 유지|아니요|  
|일광 절약 시간제 인식|아니요|  
  
|지정한 소수 자릿수|결과(전체 자릿수, 소수 자릿수)|열 길이(바이트)|소수 자릿수<br /><br /> 초<br /><br /> 전체 자릿수|  
|---------------------|---------------------------------|-----------------------------|------------------------------------------|  
|**time**|(16,7) [(12,3)에 Informatica]|5 (Informatica에서 4)|7 (Informatica의 3)|  
|**time(0)**|(8,0)|3|0-2|  
|**time(1)**|(10,1)|3|0-2|  
|**time(2)**|(11,2)|3|0-2|  
|**time(3)**|(12,3)|4|3-4|  
|**time(4)**<br /><br /> Informatica에서 지원 되지 않습니다.|(13,4)|4|3-4|  
|**time(5)**<br /><br /> Informatica에서 지원 되지 않습니다.|(14,5)|5|5-7|  
|**time(6)**<br /><br /> Informatica에서 지원 되지 않습니다.|(15,6)|5|5-7|  
|**time(7)**<br /><br /> Informatica에서 지원 되지 않습니다.|(16,7)|5|5-7|  
  
## <a name="supported-string-literal-formats-for-time"></a>time에 지원되는 문자열 리터럴 형식  
 다음 표에서 유효한 문자열 리터럴 형식에 대 한는 **시간** 데이터 형식입니다.  
  
|SQL Server|Description|  
|----------------|-----------------|  
|hh:mm[:ss][:fractional seconds][AM][PM]<br /><br /> hh:mm[:ss][.fractional seconds][AM][PM]<br /><br /> hhAM[PM]<br /><br /> hh AM[PM]|시간 값 0은 AM 지정 여부와 관계없이 자정(AM) 이후 시간을 나타냅니다. 시간이 0일 경우 PM을 지정할 수 없습니다.<br /><br /> 01부터 11까지의 시간 값은 AM 또는 PM을 지정하지 않는 경우 오전을 나타냅니다. AM을 지정하면 이 값은 오전을 나타내고 PM을 지정하면 오후를 나타냅니다.<br /><br /> 시간 값 12는 AM 또는 PM을 지정하지 않는 경우 정오 이후의 시간을 나타냅니다. AM을 지정하면 이 값은 자정 이후의 시간을 나타내고 PM을 지정하면 정오 이후의 시간을 나타냅니다. 예를 들어 12:01은 12:01 PM과 마찬가지로 정오에서 1분 지난 시간이고 12:01 AM은 자정에서 1분 지난 시간입니다. 12:01 AM을 지정하는 것은 00:01 또는 00:01 AM을 지정하는 것과 같습니다.<br /><br /> 13부터 23까지의 시간 값은 AM 또는 PM을 지정하지 않는 경우 정오 이후의 시간을 나타냅니다. 또한 PM을 지정하는 경우에도 이 값은 정오 이후의 시간을 나타냅니다. 13부터 23까지의 시간 값을 사용할 경우 AM을 지정할 수 없습니다.<br /><br /> 시간 값 24는 유효하지 않습니다. 자정을 나타내려면 12:00 AM 또는 00:00을 사용하세요.<br /><br /> 밀리초 앞에는 콜론(:) 또는 마침표(.)가 올 수 있습니다. 콜론을 사용하면 숫자는 1/1000초를 의미합니다. 마침표를 사용하면 자릿수 하나는 1/10초를 의미하고 자릿수 두 개는 1/100초를 의미하며 자릿수 세 개는 1/1000초를 의미합니다. 예를 들어 12:30:20:1은 12:30분에서 20과 1/1000초가 지난 시간을 의미하고 12:30:20.1은 12:30분에서 20과 1/10초가 지난 시간을 의미합니다.|  
  
|ISO 8601|참고|  
|--------------|-----------|  
|hh:mm:ss<br /><br /> hh:mm[:ss][.fractional seconds]|hh는 0에서 14 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 시간(시간)을 나타냅니다.<br /><br /> mm은 0에서 59 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 추가 시간(분)을 나타냅니다.|  
  
|ODBC|참고|  
|----------|-----------|  
|{t 'hh:mm:ss[.fractional seconds]'}|ODBC API에 따라 다릅니다.|  
  
## <a name="compliance-with-ansi-and-iso-8601-standards"></a>ANSI 및 ISO 8601 표준 준수  
 ISO 8601(5.3.2 및 5.3)에서 정의된 대로 자정에 24시를 사용하는 형식과 59를 초과하는 초에 윤초를 사용하는 형식은 이전 버전과의 호환성과 기존 날짜 및 시간 형식과의 일관성을 유지하기 위해 지원되지 않습니다.  
  
 하위 클라이언트에 대해 사용되는 기본 문자열 리터럴 형식은 hh:mm:ss[.nnnnnnn]로 정의되는 SQL 표준 형식에 부합됩니다. 이러한 형식은 초 소수 부분 자릿수를 제외하고 TIME에 대한 ISO 8601의 정의와 유사합니다.  
  
##  <a name="BackwardCompatibilityforDownlevelClients"></a>하위 클라이언트에 대 한 이전 버전과 호환성  
 일부 하위 수준 클라이언트 지원 하지 않습니다는 **시간**, **날짜**, **datetime2** 및 **datetimeoffset** 데이터 형식입니다. 다음 표에서는 상위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 하위 클라이언트 간 형식 매핑을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|하위 클라이언트에 전달된 기본 문자열 리터럴 형식|하위 수준 ODBC|하위 수준 OLEDB|하위 수준 JDBC|하위 수준 SQLCLIENT|  
|-----------------------------------------|----------------------------------------------------------------|----------------------|-----------------------|----------------------|---------------------------|  
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetimeoffset**|YYYY-월-일 h:mm: ss [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
  
## <a name="converting-date-and-time-data"></a>Date 및 Time 데이터 변환  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터와 함께 CAST 및 CONVERT 함수를 사용 하는 방법에 대 한 정보를 참조 하십시오. [CAST 및 convert&#40; Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
### <a name="converting-timen-data-type-to-other-date-and-time-types"></a>time(n) 데이터 형식을 다른 Date 및 Time 형식으로 변환  
 이 섹션에서는 발생 하는 상황을 설명 때는 **시간** 데이터 형식을 다른 날짜 및 시간 데이터 형식으로 변환 됩니다.  
  
 변환 됩니다 때 **time (n)**, 시간, 분 및 초 복사 됩니다. 대상 전체 자릿수가 원본 전체 자릿수보다 작으면 초 소수 부분 자릿수가 대상 전체 자릿수에 맞게 반올림됩니다. 다음 예에서는 `time(4)` 값을 `time(3)` 값으로 변환한 결과를 보여 줍니다.  
  
```  
DECLARE @timeFrom time(4) = '12:34:54.1237';  
DECLARE @timeTo time(3) = @timeFrom;  
  
SELECT @timeTo AS 'time(3)', @timeFrom AS 'time(4)';  
  
--Results  
--time(3)      time(4)  
-------------- -------------  
--12:34:54.124 12:34:54.1237  
--  
--(1 row(s) affected)  
```  
  
 변환 하려는 경우  
                    **날짜**, 변환이 실패 및 오류 메시지 206이 발생 하는: "피연산자 유형 충돌: date 시간와 호환 되지 않습니다."입니다.  
  
 변환 됩니다 때 **datetime**, 시간, 분 및 두 번째 값이 복사 되 고 날짜 구성 요소가로 설정 되어 ' 1900-01-01'. 때 소수 자릿수 초의 전체 자릿수는 **time (n)** 값이 세 자리 보다 크면는 **datetime** 결과가 잘립니다. 다음 코드에서는 `time(4)` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime datetime= @time;  
SELECT @time AS '@time', @datetime AS '@datetime';  
  
--Result  
--@time         @datetime  
--------------- -----------------------  
--12:15:04.1237 1900-01-01 12:15:04.123  
--  
--(1 row(s) affected)  
  
```  
  
 변환 됩니다 때 **smalldatetime**, 날짜가 ' 1900에 설정 됩니다-01-01'에서 시간 및 분 값 올림 됩니다. 초 및 소수 자릿수 초는 0으로 설정됩니다. 다음 코드에서는 `time(4)` 값을 `smalldatetime` 값으로 변환한 결과를 보여 줍니다.  
  
```  
-- Shows rounding up of the minute value.  
DECLARE @time time(4) = '12:15:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';   
  
--Result  
@time            @smalldatetime  
---------------- -----------------------  
12:15:59.9999    1900-01-01 12:16:00--  
--(1 row(s) affected)  
  
-- Shows rounding up of the hour value.  
DECLARE @time time(4) = '12:59:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
  
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';  
@time            @smalldatetime  
---------------- -----------------------  
12:59:59.9999    1900-01-01 13:00:00  
  
(1 row(s) affected)  
  
```  
  
 변환 하려는 경우 **datetimeoffset (n)**, 날짜가 ' 1900에 설정 됩니다-01-01' 및 시간이 복사 됩니다. 표준 시간대 오프셋이 +00:00으로 설정됩니다. 때 소수 자릿수 초의 전체 자릿수는 **time (n)** 값의 전체 자릿수 보다 크면는 **datetimeoffset (n)** 값, 값이에 맞게 반올림 합니다. 다음 예에서는 `time(4)` 값을 `datetimeoffset(3)` 형식으로 변환한 결과를 보여 줍니다.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetimeoffset datetimeoffset(3) = @time;  
  
SELECT @time AS '@time', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@time         @datetimeoffset  
--------------- ------------------------------  
--12:15:04.1237 1900-01-01 12:15:04.124 +00:00  
--  
--(1 row(s) affected)  
  
```  
  
 변환할 때 **datetime2(n)**, 날짜가 ' 1900에 설정 됩니다-01-01' 시간 구성 요소가 복사 되 고, 표준 시간대 오프셋이 00시 설정 됩니다. 때 소수 자릿수 초의 전체 자릿수는 **datetime2(n)** 값 보다 크면는 **time (n)** 값, 값은 수에 맞게 반올림 합니다.  다음 예에서는 `time(4)` 값을 `datetime2(2)` 값으로 변환한 결과를 보여 줍니다.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime2 datetime2(3) = @time;  
  
SELECT @datetime2 AS '@datetime2', @time AS '@time';  
  
--Result  
--@datetime2              @time  
------------------------- -------------  
--1900-01-01 12:15:04.124 12:15:04.1237  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-timen"></a>문자열 리터럴을 time(n)으로 변환  
 문자열에 포함된 모든 부분의 형식이 올바른 경우 문자열 리터럴에서 날짜/시간 유형으로 변환할 수 있습니다. 그렇지 않으면 런타임 오류가 발생합니다. 날짜/시간 유형에서 문자열 리터럴로의 암시적 변환 또는 명시적 변환에 스타일을 지정하지 않은 경우 현재 세션의 기본 형식이 지정됩니다. 다음 표에서 문자열을 변환 하기 위한 규칙 리터럴을 **시간** 데이터 형식입니다.  
  
|입력 문자열 리터럴|변환 규칙|  
|--------------------------|---------------------|  
|ODBC DATE|ODBC 문자열 리터럴에 매핑되는 **datetime** 데이터 형식입니다. 모든 할당 연산에 ODBC DATETIME 리터럴에서 **시간**형식 간에 암시적 변환이 발생 합니다 **datetime** 과 이러한 형식 변환 규칙으로 정의 된 대로 합니다.|  
|ODBC TIME|위의 ODBC DATE 규칙을 참조하세요.|  
|ODBC DATETIME|위의 ODBC DATE 규칙을 참조하세요.|  
|DATE만|기본값이 제공됩니다.|  
|TIME만|중요하지 않음|  
|TIMEZONE만|기본값이 제공됩니다.|  
|DATE+TIME|입력 문자열의 TIME 부분이 사용됩니다.|  
|DATE+TIMEZONE|허용되지 않습니다.|  
|TIME+TIMEZONE|입력 문자열의 TIME 부분이 사용됩니다.|  
|DATE+TIME+TIMEZONE|로컬 DATETIME의 TIME 부분이 사용됩니다.|  
  
## <a name="examples"></a>예  
  
### <a name="a-comparing-date-and-time-data-types"></a>1. 날짜 및 시간 데이터 형식 비교  
 다음 예제에서는 문자열을 각각 캐스팅 한 결과를 비교 **날짜** 및 **시간** 데이터 형식입니다.  
  
```  
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
  
|데이터 형식|출력|  
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
###  <a name="ExampleB"></a> 2. time(7) 열에 유효한 시간 문자열 리터럴 삽입  
 다음 표에서 데이터 형식의 열에 삽입 될 수 있는 여러 문자열 리터럴과 **time (7)** 다음 해당 열에 저장 된 값을 사용 합니다.  
  
|문자열 리터럴 형식 유형|삽입되는 문자열 리터럴|저장되는 time(7) 값|Description|  
|--------------------------------|-----------------------------|------------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01:123AM'|01:01:01.1230000|콜론(:)이 초 소수 부분 자릿수의 전체 자릿수 앞에 오면 소수 자릿수는 세 자리를 초과할 수 없으며 초과할 경우 오류가 발생합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 AM'|01:01:01.1234567|AM 또는 PM을 지정하면 시간이 리터럴 AM 또는 PM 없이 24시간 형식으로 저장됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 PM'|13:01:01.1234567|AM 또는 PM을 지정하면 시간이 리터럴 AM 또는 PM 없이 24시간 형식으로 저장됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567PM'|13:01:01.1234567|AM 또는 PM 앞의 공백은 선택 사항입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01AM'|01:00:00.0000000|시간만 지정하면 다른 값은 모두 0이 됩니다.|  
|SQL Server|'01 AM'|01:00:00.0000000|AM 또는 PM 앞의 공백은 선택 사항입니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01'|01:01:01.0000000|초 소수 부분 자릿수의 전체 자릿수를 지정하지 않으면 데이터 형식에 따라 정의되는 각 자릿수는 0입니다.|  
|ISO 8601|'01:01:01.1234567'|01:01:01.1234567|ISO 8601을 따르려면 AM 또는 PM 대신 24시간 형식을 사용하세요.|  
|ISO 8601|'01:01:01.1234567 +01:01'|01:01:01.1234567|TZD(Time Zone Difference)는 선택 사항이며 입력할 수 있지만 저장되지 않습니다.|  
  
### <a name="c-inserting-time-string-literal-into-columns-of-each-date-and-time-date-type"></a>3. 각 date 및 time 날짜 형식의 열에 시간 문자열 리터럴 삽입  
 다음 표에서 첫 번째 열은 두 번째 열의 날짜 또는 시간 데이터 형식의 데이터베이스 테이블 열에 삽입될 시간 문자열 리터럴을 보여 줍니다. 세 번째 열은 데이터베이스 테이블 열에 저장될 값을 보여 줍니다.  
  
|삽입되는 문자열 리터럴|열 데이터 형식|열에 저장되는 값|Description|  
|-----------------------------|----------------------|------------------------------------|-----------------|  
|'12:12:12.1234567'|**time(7)**|12:12:12.1234567|초 소수 부분 자릿수의 전체 자릿수가 열에 대해 지정한 값을 초과하면 문자열이 오류 없이 잘립니다.|  
|'2007-05-07'|**date**|NULL|시간 값이 있으면 INSERT 문이 실패합니다.|  
|'12:12:12'|**smalldatetime**|1900-01-01 12:12:00|초 소수 부분 자릿수의 전체 자릿수 값이 있으면 INSERT 문이 실패합니다.|  
|'12:12:12.123'|**datetime**|1900-01-01 12:12:12.123|초 전체 자릿수가 세 자리를 초과하면 INSERT 문이 실패합니다.|  
|'12:12:12.1234567'|**datetime2(7)**|1900-01-01 12:12:12.1234567|초 소수 부분 자릿수의 전체 자릿수가 열에 대해 지정한 값을 초과하면 문자열이 오류 없이 잘립니다.|  
|'12:12:12.1234567'|**(7)**|1900-01-01 12:12:12.1234567 +00:00|초 소수 부분 자릿수의 전체 자릿수가 열에 대해 지정한 값을 초과하면 문자열이 오류 없이 잘립니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

