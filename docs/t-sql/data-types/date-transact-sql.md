---
description: date(Transact-SQL)
title: date(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- date_TSQL
- date
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], date
- date and time [SQL Server], date
- dates [SQL Server], data types
- date data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: c963e8b4-5a85-4bd0-9d48-3f8da8f6516b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0d6246c3b8318ae2596dfd1f4240692be7941e49
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175953"
---
# <a name="date-transact-sql"></a>date(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜를 정의합니다.

## <a name="date-description"></a>date 설명
  
|속성|값|  
|--------------|-----------|  
|구문|**date**|  
|사용|DECLARE \@MyDate **date**<br /><br /> CREATE TABLE Table1(Column1 **date**)|  
|기본 문자열 리터럴 형식<br /><br /> (하위 클라이언트에 대해 사용됨)|YYYY-MM-DD<br /><br /> 자세한 내용은 뒷부분에 나오는 "하위 클라이언트에 대한 이전 버전과의 호환성" 섹션을 참조하세요.|  
|범위|0001-01-01부터 9999-12-31까지(Informatica의 경우 1582-10-15부터 9999-12-31)<br /><br /> CE(서기) 1년 1월 1일부터 CE 9999년 12월 31일까지(Informatica의 경우 CE 1582년 10월 15일부터 CE 9999년 12월 31일까지)|  
|요소 범위|YYYY는 0001에서 9999 사이에 속하는 4자리 숫자로, 연도를 나타냅니다. Informatica의 경우, YYYY는 1582에서 9999까지의 범위로 제한됩니다.<br /><br /> MM은 01에서 12 사이에 속하는 두 자리 숫자로, 지정한 연도의 월을 나타냅니다.<br /><br /> DD는 월에 따라 01에서 31 사이에 속하는 두 자리 숫자로, 특정 월의 일을 나타냅니다.|  
|문자 길이|10자리|  
|전체 자릿수, 소수 자릿수|10, 0|  
|스토리지 크기|3바이트(고정)|  
|스토리지 구조|1, 3바이트 정수로 날짜를 저장합니다.|  
|정확도|1일|  
|기본값|1900-01-01<br /><br /> 이 값은 **time**에서 **datetime2** 또는 **datetimeoffset**으로의 암시적 변환을 위해 추가되는 날짜 부분에 사용됩니다.|  
|달력|일반 달력|  
|사용자 정의 초 소수 부분 자릿수|예|  
|표준 시간대 오프셋 인식 및 유지|예|  
|일광 절약 시간제 인식|예|  
  
## <a name="supported-string-literal-formats-for-date"></a>date에 대해 지원되는 문자열 리터럴 형식
다음 표에서는 **date** 데이터 형식에 대해 유효한 문자열 리터럴 형식을 보여줍니다.
  
|숫자|Description|  
|-------------|-----------------|  
|mdy<br /><br /> [m]m/dd/[yy]yy<br /><br /> [m]m-dd-[yy]yy<br /><br /> [m]m.dd.[yy]yy<br /><br /> myd<br /><br /> mm/[yy]yy/dd<br /><br /> mm-[yy]yy/dd<br /><br /> [m]m.[yy]yy.dd<br /><br /> dmy<br /><br /> dd/[m]m/[yy]yy<br /><br /> dd-[m]m-[yy]yy<br /><br /> dd.[m]m.[yy]yy<br /><br /> dym<br /><br /> dd/[yy]yy/[m]m<br /><br /> dd-[yy]yy-[m]m<br /><br /> dd.[yy]yy.[m]m<br /><br /> ymd<br /><br /> [yy]yy/[m]m/dd<br /><br /> [yy]yy-[m]m-dd<br /><br /> [yy]yy-[m]m-dd|[m]m, dd, [yy]yy는 슬래시(/), 하이픈(-) 또는 마침표(.)로 구분된 문자열에서 월, 일, 연도를 나타냅니다.<br /><br /> 네 자리 또는 두 자리 연도만 지원됩니다. 가능하면 네 자리 연도를 사용하세요. 두 자리 연도를 4자리 연도로 해석할 구분 연도를 0001부터 9999까지의 정수 중에서 지정하려면 [두 자리 연도 구분 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 사용합니다.<br /><br /> **참고!** Informatica의 경우, YYYY는 1582에서 9999까지의 범위로 제한됩니다.<br /><br /> 마지막 두 자리와 같거나 작은 두 자리 연도는 구분 연도와 같은 세기 연도입니다. 두 자리 연도가 구분 연도의 마지막 두 자리보다 크면 구분 연도보다 하나 이전의 세기로 해석됩니다. 예를 들어 두 자리 연도 구분이 2049(기본값)이면 두 자리 연도 49는 2049로 해석되고 두 자리 연도 50은 1950으로 해석됩니다.<br /><br /> 기본 날짜 형식은 현재 언어 설정에 따라 결정됩니다. [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 및 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 문을 사용하여 날짜 형식을 변경할 수 있습니다.<br /><br /> **ydm** 형식은 **date**에 대해 지원되지 않습니다.|  
  
|알파벳|Description|  
|------------------|-----------------|  
|mon [dd][,] yyyy<br /><br /> mon dd[,] [yy]<br /><br /> mon yyyy [dd]<br /><br /> [dd] mon[,] yyyy<br /><br /> dd mon[,][yy]yy<br /><br /> dd [yy]yy mon<br /><br /> [dd] yyyy mon<br /><br /> yyyy mon [dd]<br /><br /> yyyy [dd] mon|**mon**은 현재 언어에서 지정된 월의 전체 이름 또는 약어를 나타냅니다. 쉼표는 선택 사항이며 대문자는 무시됩니다.<br /><br /> 모호성을 피하려면 4자리 연도를 사용하세요.<br /><br /> 일이 생략된 경우 해당 월의 첫째 날이 사용됩니다.|  
  
|ISO 8601|Description|  
|--------------|----------------|  
|YYYY-MM-DD<br /><br /> YYYYMMDD|SQL 표준과 같습니다. 이 형식은 유일하게 국제 표준으로 정의된 형식입니다.|  
  
|구분되지 않음|Description|  
|-----------------|-----------------|  
|[yy]yymmdd<br /><br /> yyyy[mm][dd]|**date** 데이터는 4자리, 6자리 또는 8자리로 지정할 수 있습니다. 6자리 또는 8자리 문자열은 항상 **ymd**로 해석됩니다. 월과 일은 항상 두 자리여야 합니다. 4자리 문자열은 연도로 해석됩니다.|  
  
|ODBC|Description|  
|----------|-----------------|  
|{ d 'yyyy-mm-dd' }|ODBC API에 따라 다릅니다.|  
  
|W3C XML 형식|Description|  
|--------------------|-----------------|  
|yyyy-mm-ddTZD|XML/SOAP을 사용할 경우 지원됩니다.<br /><br /> TZD는 표준 시간대 지정자(Z나 +hh:mm 또는 -hh:mm)입니다.<br /><br /> - hh:mm은 표준 시간대 오프셋을 나타냅니다. hh는 0에서 14 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 시간(시간)을 나타냅니다.<br />- MM은 0에서 59 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 추가 시간(분)을 나타냅니다.<br />- +(더하기) 또는 -(빼기)는 표준 시간대 오프셋의 필수 기호입니다. 이 기호는 현지 시간을 가져오기 위해 UTC(협정 세계시)에서 표준 시간대 오프셋을 더했는지 또는 뺐는지를 나타냅니다. 올바른 표준 시간대 오프셋 범위는 -14:00에서 +14:00 사이입니다.|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 및 ISO 8601 호환성  
**날짜**는 일반 달력에 대한 ANSI SQL 표준 정의를 준수합니다. "NOTE 85 - Datetime 데이터 형식을 사용하면 일반 달력 형식의 날짜를 0001–01–01 CE에서 9999-12-31 CE 사이에 속하는 날짜 범위에 저장할 수 있습니다."를 따릅니다.
  
하위 클라이언트에 대해 사용되는 기본 문자열 리터럴 형식은 YYYY-MM-DD로 정의되는 SQL 표준 형식을 따릅니다. 이 형식은 DATE에 대한 ISO 8601 정의와 같습니다.
  
> [!NOTE]  
>  Informatica의 경우 범위는 1582-10-15(CE 1582년 10월 15일)부터 9999-12-31(CE 9999년 12월 31일)까지로 제한됩니다.  
  
## <a name="backward-compatibility-for-down-level-clients"></a>하위 클라이언트에 대한 이전 버전과의 호환성
일부 하위 클라이언트는 **time**, **date**, **datetime2** 및 **datetimeoffset** 데이터 형식을 지원하지 않습니다. 다음 표에서는 상위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 하위 클라이언트 간 형식 매핑을 보여 줍니다.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|하위 클라이언트에 전달된 기본 문자열 리터럴 형식|하위 수준 ODBC|하위 수준 OLEDB|하위 수준 JDBC|하위 수준 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
  
## <a name="converting-date-and-time-data"></a>date 및 time 데이터 변환
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터에 CAST 및 CONVERT 함수를 사용하는 방법은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.  
  
### <a name="converting-date-to-other-date-and-time-types"></a>date을 다른 날짜 및 시간 형식으로 변환

이 섹션에서는 **date** 데이터 형식을 다른 날짜 및 시간 데이터 형식으로 변환할 때 어떤 일이 발생하는지를 설명합니다.
  
변환이 **time(n)** 에서 일어나는 경우 이 변환이 실패하고, "피연산자 유형 충돌: date는 time과 호환되지 않습니다"라는 오류 메시지 206이 발생합니다.
  
변환이 **datetime**에서 일어나는 경우 날짜가 복사 됩니다. 다음 코드에서는 `date` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
변환이 **smalldatetime**에서 일어나는 경우 **date** 값이 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 범위 안에 있으면 날짜 구성 요소가 복사되고 시간 구성 요소는 00:00:00.000으로 설정됩니다. **날짜** 값이 **smalldatetime** 값의 범위 밖에 있으면, “data 데이터 형식을 smalldatetime 데이터 형식으로 변환하는 중 값 범위를 벗어났습니다.”라는 오류 메시지 242가 발생하고 **smalldatetime** 값이 NULL로 설정됩니다. 다음 코드에서는 `date` 값을 `smalldatetime` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
변환이 **datetimeoffset(n)** 에서 일어나는 경우 날짜가 복사되고 시간은 00:00.0000000 +00:00으로 설정됩니다. 다음 코드에서는 `date` 값을 `datetimeoffset(3)` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
변환이 **datetime2(n)** 에서 일어나는 경우 날짜 구성 요소가 복사되고 시간 구성 요소는 00:00.000000으로 설정됩니다. 다음 코드에서는 `date` 값을 `datetime2(3)` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @date date = '1912-10-25'  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-date"></a>문자열 리터럴을 date로 변환
문자열에 포함된 모든 부분의 형식이 유효한 경우 문자열 리터럴에서 날짜/시간 유형으로 변환할 수 있습니다. 그렇지 않으면 런타임 오류가 발생합니다. 날짜 및 시간 형식에서 문자열 리터럴로의 암시적 변환 또는 명시적 변환에 스타일을 지정하지 않은 경우 현재 세션의 기본 형식이 지정됩니다. 다음 표에서는 문자열 리터럴을 **date** 데이터 형식으로 변환하는 규칙을 보여 줍니다.
  
|입력 문자열 리터럴|**date**|  
|---|---|
|ODBC DATE|ODBC 문자열 리터럴은 **datetime** 데이터 형식으로 매핑됩니다. ODBC DATETIME 리터럴에서 **date** 형식으로 할당하면 **datetime**과 변환 규칙이 정의하는 형식 간에 암시적 변환이 발생합니다.|  
|ODBC TIME|이전 ODBC DATE 규칙을 참조하세요.|  
|ODBC DATETIME|이전 ODBC DATE 규칙을 참조하세요.|  
|DATE만|중요하지 않음|  
|TIME만|기본값이 제공됩니다.|  
|TIMEZONE만|기본값이 제공됩니다.|  
|DATE+TIME|입력 문자열의 DATE 부분이 사용됩니다.|  
|DATE+TIMEZONE|허용되지 않습니다.|  
|TIME+TIMEZONE|기본값이 제공됩니다.|  
|DATE+TIME+TIMEZONE|로컬 DATETIME의 DATE 부분이 사용됩니다.|  
  
## <a name="examples"></a>예제  
다음 예에서는 문자열을 각 날짜 및 시간 데이터 형식으로 캐스팅하는 결과를 비교합니다.
  
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
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  

SQL Server 2008에서 처음 도입되었습니다.

## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
