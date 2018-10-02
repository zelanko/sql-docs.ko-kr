---
title: datetime(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- datetime_TSQL
- datetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetime
- dates [SQL Server], data types
- datetime data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: 9bd1cc5b-227b-4032-95d6-7581ddcc9924
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3e83229dde185bb4744e89fabbf88ddf3cabaa3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720391"
---
# <a name="datetime-transact-sql"></a>datetime(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

소수 자릿수 초가 있는 24시간제 기준의 시간과 결합된 날짜를 정의합니다.
  
> [!NOTE]  
>  새 작업에 대해 **time**, **date**, **datetime2** 및 **datetimeoffset** 데이터 형식을 사용합니다. 이러한 데이터 형식은 SQL 표준에 맞는 형식으로, 이식성이 높습니다. **time**, **datetime2** 및 **datetimeoffset**은 초의 정밀도를 높여줍니다. 전 세계에 배포되는 응용 프로그램의 경우 **datetimeoffset**을 사용하면 표준 시간대가 지원됩니다.  
  
## <a name="datetime-description"></a>datetime 설명  
  
|속성|값|  
|---|---|
|구문|**datetime**|  
|사용법|DECLARE \@MyDatetime **datetime**<br /><br /> CREATE TABLE Table1(Column1 **datetime**)|  
|기본 문자열 리터럴 형식<br /><br /> (하위 클라이언트에 대해 사용됨)|해당 사항 없음|  
|날짜 범위|01.01.53부터 31.12.99까지|  
|시간 범위|00:00:00부터 23:59:59.997까지|  
|표준 시간대 오프셋 범위|없음|  
|요소 범위|YYYY는 1753부터 9999까지의 4자리 숫자로, 연도를 나타냅니다.<br /><br /> MM은 01에서 12 사이에 속하는 두 자리 숫자로, 지정한 연도의 월을 나타냅니다.<br /><br /> DD는 월에 따라 01에서 31 사이에 속하는 두 자리 숫자로, 지정한 월의 일을 나타냅니다.<br /><br /> hh는 00에서 23 사이에 속하는 두 자리 숫자로, 시를 나타냅니다.<br /><br /> mm은 00에서 59 사이에 속하는 두 자리 숫자로, 분을 나타냅니다.<br /><br /> ss는 00에서 59 사이에 속하는 두 자리 숫자로, 초를 나타냅니다.<br /><br /> n*은 0에서 999 사이에 속하는 세 자리 숫자로, 소수 자릿수 초를 나타냅니다.|  
|문자 길이|최소 19자리부터 최대 23자리까지|  
|저장소 크기|8바이트|  
|정확도|.000, .003 또는 .007초 단위로 반올림됩니다.|  
|기본값|1900-01-01 00:00:00|  
|달력|일반 달력(전체 연도 범위를 포함하지는 않음)|  
|사용자 정의 초 소수 부분 자릿수|아니오|  
|표준 시간대 오프셋 인식 및 유지|아니오|  
|일광 절약 시간제 인식|아니오|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>datetime에 대해 지원되는 문자열 리터럴 형식  
다음 표에는 **datetime**에 대해 지원되는 문자열 리터럴 형식이 나와 있습니다. ODBC를 제외하고 **datetime** 문자열 리터럴은 작은따옴표(')로 묶입니다(예: 'string_literaL'). **us_english** 환경이 아닌 경우 문자열 리터럴은 N'string_literaL' 형식이어야 합니다.
  
|숫자|설명|  
|---|---|
|날짜 형식:<br /><br /> [0]4/15/[19]96 -- (mdy)<br /><br /> [0]4-15-[19]96 -- (mdy)<br /><br /> [0]4.15.[19]96 -- (mdy)<br /><br /> [0]4/[19]96/15 -- (myd)<br /><br /> 15/[0]4/[19]96 -- (dmy)<br /><br /> 15/[19]96/[0]4 -- (dym)<br /><br /> [19]96/15/[0]4 -- (ydm)<br /><br /> [19]96/[0]4/15 -- (ymd)<br /><br /> 시간 형식:<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|지정된 숫자 월을 사용하여 날짜 데이터를 지정할 수 있습니다. 예를 들어 5/20/97은 1997년 5월 20일을 나타냅니다. 숫자 날짜 형식을 사용할 경우에는 문자열에 슬래시 기호(/), 하이픈(-) 또는 마침표(.)를 구분 기호로 사용하여 년, 월, 일을 지정합니다. 이 문자열은 다음과 같은 형식이어야 합니다.<br /><br /> *number separator number separator number [time] [time]*<br /><br /> <br /><br /> 언어를 **us_english**로 설정하면 기본 날짜 순서는 mdy(월, 일, 년)입니다. [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 문을 사용하여 날짜 순서를 변경할 수 있습니다.<br /><br /> SET DATEFORMAT 설정에 따라 날짜 값의 해석 방법이 결정됩니다. 순서가 설정과 다르면 값이 범위를 벗어나므로 날짜로 해석되지 않거나 잘못 해석됩니다. 예를 들어 12/10/08은 DATEFORMAT 설정에 따라 6가지 날짜 중 하나로 해석될 수 있습니다. 네 부분으로 된 연도는 년으로 해석됩니다.|  
  
|알파벳|설명|  
|---|---|
|Apr[il] [15][,] 1996<br /><br /> Apr[il] 15[,] [19]96<br /><br /> Apr[il] 1996 [15]<br /><br /> [15] Apr[il][,] 1996<br /><br /> 15 Apr[il][,][19]96<br /><br /> 15 [19]96 apr[il]<br /><br /> [15] 1996 apr[il]<br /><br /> 1996 APR[IL] [15]<br /><br /> 1996 [15] APR[IL]|전체 월 이름으로 지정된 월을 사용하여 날짜 데이터를 지정할 수 있습니다. 예를 들어 April 또는 현재 언어에서 정해진 월 약어(Apr)를 사용할 수 있습니다. 쉼표는 선택 사항이며 대문자는 무시됩니다.<br /><br /> 다음은 알파벳 날짜 형식 사용에 대한 몇 가지 지침입니다.<br /><br /> 1) 날짜 및 시간 데이터는 작은따옴표(')로 묶습니다. 영어 이외의 다른 언어에서는 N'을 사용합니다.<br /><br /> 2) 대괄호로 묶인 문자는 선택 사항입니다.<br /><br /> 3) 연도의 마지막 두 자리만 지정하는 경우 이 값이 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) 구성 옵션 값의 마지막 두 자리보다 작으면 구분 연도와 같은 세기로 간주됩니다. 이 옵션 값보다 크거나 같은 값은 구분 연도 전의 세기로 간주됩니다. 예를 들어 **two digit year cutoff**가 2050(기본값)이면 25는 2025로 해석되고 50은 1950으로 해석됩니다. 모호성을 피하려면 4자리 연도를 사용하세요.<br /><br /> 4) 일이 생략된 경우 해당 월의 첫째 날이 사용됩니다.<br /><br /> <br /><br /> 월을 알파벳 형식으로 지정하면 SET DATEFORMAT 세션 설정이 적용되지 않습니다.|  
  
|ISO 8601|설명|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.mmm]<br /><br /> YYYYMMDD[ hh:mm:ss[.mmm]]|예:<br /><br /> 1) 2004-05-23T14:25:10<br /><br /> 2) 2004-05-23T14:25:10.487<br /><br /> <br /><br /> ISO 8601 형식을 사용하려면 각 요소를 이 형식으로 지정해야 합니다. 여기에는 형식에 표시되는 **T**, 콜론(:), 마침표(.)도 포함됩니다.<br /><br /> 대괄호는 초의 소수 구성 요소가 선택 사항임을 나타냅니다. 시간 구성 요소는 24시간 형식으로 지정됩니다.<br /><br /> T는 **datetime** 값의 시간 시작 부분을 나타냅니다.<br /><br /> ISO 8601 형식을 사용할 때의 이점은 이 형식이 명확한 사양을 가진 국제 표준이라는 점입니다. 또한 이 형식은 SET DATEFORMAT 또는 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 설정에 영향을 받지 않습니다.|  
  
|구분되지 않음|설명|  
|---|---|
|YYYYMMDD hh:mm:ss[.mmm]||  
  
|ODBC|설명|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|ODBC API는 이스케이프 시퀀스를 정의하여 ODBC가 타임스탬프 데이터를 호출하는 날짜 및 시간 값을 나타냅니다. 이 ODBC 타임스탬프 형식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원하는 OLE DB 언어 정의(DBGUID-SQL)에서도 지원됩니다. ADO, OLE DB 및 ODBC 기반 API를 사용하는 응용 프로그램에서는 이 ODBC 타임스탬프 형식을 사용하여 날짜 및 시간을 나타낼 수 있습니다.<br /><br /> ODBC 타임스탬프 이스케이프 시퀀스의 형식은 다음과 같습니다. { *literal_type* '*constant_value*' }.<br /><br /> <br /><br /> - *literal_type*은 이스케이프 시퀀스의 유형을 지정합니다. 타임스탬프에는 다음과 같은 3개의 *literal_type* 지정자가 있습니다.<br />1) d = 날짜만<br />2) t = 시간만<br />3) ts = 타임스탬프(시간+날짜)<br /><br /> <br /><br /> - '*constant_value*'는 이스케이프 시퀀스의 값입니다. *constant_value*는 각 *literal_type*에 대해 이러한 형식을 따라야 합니다.<br />d : yyyy-mm-dd<br />t : hh:mm:ss[.fff]<br />ts : yyyy-mm-dd hh:mm:ss[.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>datetime 초 소수 부분 자릿수 반올림  
다음 표에서와 같이 **datetime** 값은 .000, .003 또는 .007초 단위로 반올림됩니다.
  
|사용자 지정 값|시스템 저장 값|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 및 ISO 8601 호환성  
**datetime**은 ANSI 또는 ISO 8601 규격이 아닙니다.
  
##  <a name="_datetime"></a> Date 및 Time 데이터 변환  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터에 CAST 및 CONVERT 함수를 사용하는 방법은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>다른 날짜 및 시간 형식을 datetime 데이터 형식으로 변환 
이 섹션에서는 다른 날짜/시간 데이터 형식이 **datetime** 데이터 형식으로 변환하면 어떤 일이 발생하는지를 설명합니다.  
  
**date**에서 변환되는 경우 년, 월, 일이 복사됩니다. 시간 구성 요소는 00:00:00.000으로 설정됩니다. 다음 코드에서는 `date` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
**time(n)** 에서 변환되는 경우 시간 구성 요소가 복사되고 날짜 구성 요소는 '1900-01-01'로 설정됩니다. **time(n)** 값의 소수 자릿수가 세 자리보다 크면 값이 이에 맞게 잘립니다. 다음 예에서는 `time(4)` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
**smalldatetime**에서 변환되는 경우 시간과 분이 복사됩니다. 초 및 소수 자릿수 초는 0으로 설정됩니다. 다음 코드에서는 `smalldatetime` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
**datetimeoffset(n)** 에서 변환되는 경우 날짜 및 시간 구성 요소가 복사됩니다. 표준 시간대는 잘립니다. **datetimeoffset(n)** 값의 소수 자릿수가 세 자리보다 크면 값이 잘립니다. 다음 예에서는 `datetimeoffset(4)` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
변환이 **datetime2(n)** 에서 일어나는 경우 날짜 및 시간이 복사됩니다. **datetime2(n)** 값의 소수 자릿수가 세 자리보다 크면 값이 잘립니다. 다음 예에서는 `datetime2(4)` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
```sql
DECLARE @datetime2 datetime2(4) = '1968-10-23 12:45:37.1237';  
DECLARE @datetime datetime = @datetime2;  
  
SELECT @datetime AS '@datetime', @datetime2 AS '@datetime2';  
  
--Result  
--@datetime               @datetime2  
------------------------- ------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237  
```  
  
## <a name="examples"></a>예  
다음 예에서는 문자열을 각 **date** 및 **time** 데이터 형식으로 캐스팅하는 결과를 비교합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
