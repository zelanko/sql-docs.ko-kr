---
title: "날짜 (Transact SQL) | Microsoft Docs"
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
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c5d3a52b6163f375850b22e27baf9a858ef8ed8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="date-transact-sql"></a>date(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜를 정의합니다.
  
## <a name="date-description"></a>date 설명
  
|속성|값|  
|--------------|-----------|  
|구문|**date**|  
|사용법|선언 @MyDate **날짜**<br /><br /> 만들 테이블 Table1 (Column1 **날짜** )|  
|기본 문자열 리터럴 형식<br /><br /> (하위 클라이언트에 대해 사용됨)|YYYY-MM-DD<br /><br /> 자세한 내용은 뒷부분에 나오는 "하위 클라이언트에 대한 이전 버전과의 호환성" 섹션을 참조하세요.|  
|범위|0001-01-01부터 9999-12-31 (시점은 1582-10-15부터 9999-12-31 Informatica에 대 한)<br /><br /> 1 년 1 월 1 일 년 12 월 31 일 까지의 CE에서 9999 CE (12 월 31 일 시점은 1582 년 10 월 15 일 CE, 9999 CE Informatica에 대 한)|  
|요소 범위|YYYY는 0001에서 9999 사이에 속하는 4자리 숫자로, 연도를 나타냅니다. Informatica, YYYY을 시점은 1582에서 9999 까지의 범위로 제한 됩니다.<br /><br /> MM은 01에서 12 사이에 속하는 두 자리 숫자로, 지정한 연도의 월을 나타냅니다.<br /><br /> DD는 월에 따라 01에서 31 사이에 속하는 두 자리 숫자로, 특정 월의 일을 나타냅니다.|  
|문자 길이|10자리|  
|전체 자릿수, 소수 자릿수|10, 0|  
|저장소 크기|3바이트(고정)|  
|저장소 구조|1, 3바이트 정수로 날짜를 저장합니다.|  
|정확도|1일|  
|기본값|1900-01-01<br /><br /> 이 값은 암시적으로 변환에 대 한 추가 되는 날짜 부분에 대 한 사용 **시간** 를 **datetime2** 또는 **datetimeoffset**합니다.|  
|달력|일반 달력|  
|사용자 정의 초 소수 부분 자릿수|아니요|  
|표준 시간대 오프셋 인식 및 유지|아니요|  
|일광 절약 시간제 인식|아니요|  
  
## <a name="supported-string-literal-formats-for-date"></a>날짜에 대 한 지원 되는 문자열 리터럴 형식
다음 표에 유효한 문자열 리터럴 형식에 대 한는 **날짜** 데이터 형식입니다.
  
|숫자|Description|  
|-------------|-----------------|  
|mdy<br /><br /> [m]m/dd/[yy]yy<br /><br /> [m]m-dd-[yy]yy<br /><br /> [m]m.dd.[yy]yy<br /><br /> myd<br /><br /> mm/[yy]yy/dd<br /><br /> mm-[yy]yy/dd<br /><br /> [m]m.[yy]yy.dd<br /><br /> dmy<br /><br /> dd/[m]m/[yy]yy<br /><br /> dd-[m]m-[yy]yy<br /><br /> dd.[m]m.[yy]yy<br /><br /> dym<br /><br /> dd/[yy]yy/[m]m<br /><br /> dd-[yy]yy-[m]m<br /><br /> dd.[yy]yy.[m]m<br /><br /> ymd<br /><br /> [yy]yy/[m]m/dd<br /><br /> [yy]yy-[m]m-dd<br /><br /> [yy]yy-[m]m-dd|[m]m, dd, [yy]yy는 슬래시(/), 하이픈(-) 또는 마침표(.)로 구분된 문자열에서 월, 일, 연도를 나타냅니다.<br /><br /> 네 자리 또는 두 자리 연도만 지원됩니다. 가능하면 네 자리 연도를 사용하세요. 사용 하는 정수 0001에서 9999 까지의 두 자리 연도 네 자리 연도로 해석 하기 위한 구분 연도 지정 하려면는 [두 자리 연도 구성 cutoff 서버 구성 옵션](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)합니다.<br /><br /> **참고!** Informatica, YYYY을 시점은 1582에서 9999 까지의 범위로 제한 됩니다.<br /><br /> 마지막 두 자리와 같거나 작은 두 자리 연도는 구분 연도와 같은 세기 연도입니다. 두 자리 연도가 구분 연도의 마지막 두 자리보다 크면 구분 연도보다 하나 이전의 세기로 해석됩니다. 예를 들어 두 자리 연도 구분이 2049(기본값)이면 두 자리 연도 49는 2049로 해석되고 두 자리 연도 50은 1950으로 해석됩니다.<br /><br /> 기본 날짜 형식은 현재 언어 설정에 따라 결정됩니다. 사용 하 여 날짜 형식을 변경할 수는 [언어 설정](../../t-sql/statements/set-language-transact-sql.md) 및 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 문.<br /><br /> **ydm** 형식에 지원 되지 않습니다 **날짜**합니다.|  
  
|알파벳|Description|  
|------------------|-----------------|  
|mon [dd][,] yyyy<br /><br /> mon dd[,] [yy]yy<br /><br /> mon yyyy [dd]<br /><br /> [dd] mon[,] yyyy<br /><br /> dd mon[,][yy]yy<br /><br /> dd [yy]yy mon<br /><br /> [dd] yyyy mon<br /><br /> yyyy mon [dd]<br /><br /> yyyy [dd] mon|**mon** 전체 월 이름 또는 현재 언어에서 월의 약어를 나타냅니다. 쉼표는 선택 사항이며 대문자는 무시됩니다.<br /><br /> 모호성을 피하려면 4자리 연도를 사용하세요.<br /><br /> 일이 생략된 경우 해당 월의 첫째 날이 사용됩니다.|  
  
|ISO 8601|설명|  
|--------------|----------------|  
|YYYY-MM-DD<br /><br /> YYYYMMDD|SQL 표준과 같습니다. 이는 유일하게 국제 표준으로 정의된 형식입니다.|  
  
|구분되지 않음|Description|  
|-----------------|-----------------|  
|[yy]yymmdd<br /><br /> yyyy[mm][dd]|**날짜** 데이터는 4, 6, 또는 8 자리로 지정할 수 있습니다. 6 자리 또는 8 자리 문자열은 항상로 해석 **ymd**합니다. 월과 일은 항상 두 자리여야 합니다. 4자리 문자열은 연도로 해석됩니다.|  
  
|ODBC|Description|  
|----------|-----------------|  
|{ d 'yyyy-mm-dd' }|ODBC API에 따라 다릅니다.|  
  
|W3C XML 형식|Description|  
|--------------------|-----------------|  
|yyyy-mm-ddTZD|XML/SOAP을 사용할 경우 지원됩니다.<br /><br /> TZD는 표준 시간대 지정자(Z나 +hh:mm 또는 -hh:mm)입니다.<br /><br /> -hh: mm 표준 시간대 오프셋을 나타냅니다. hh는 0에서 14 사이에 속하는 두 자리 숫자로, 표준 시간대 오프셋의 시간(시간)을 나타냅니다.<br />-MM은 0에서 59 사이에 속하는, 표준 시간대 오프셋의 분 수를 나타내는 두 자리 숫자로, 합니다.<br />-+ (더하기) 또는-(빼기)는 표준 시간대 오프셋의 필수 기호입니다. 이는 현지 시간을 가져오기 위해 UTC(Coordinated Universal Time)에서 표준 시간대 오프셋을 더했는지 또는 뺐는지를 나타냅니다. 올바른 표준 시간대 오프셋 범위는 -14:00에서 +14:00 사이입니다.|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 및 ISO 8601 호환성  
**날짜** 일반 달력에 대 한 ANSI SQL 표준 정의 준수: "NOTE 85-Datetime 데이터 형식을 날짜부터 9999 – 12 – 31 날짜 범위 0001 – 01 – 01 CE에 저장 하면 일반 달력 형식의에서 CE."
  
하위 클라이언트에 대해 사용되는 기본 문자열 리터럴 형식은 YYYY-MM-DD로 정의되는 SQL 표준 형식을 따릅니다. 이 형식은 DATE에 대한 ISO 8601 정의와 같습니다.
  
> [!NOTE]  
>  Informatica, 범위는 시점은 1582-10-15 (시점은 1582 년 10 월 15 일 CE) 9999-12-31 (12 월 31 일에서 9999 CE)를 제한 합니다.  
  
## <a name="backward-compatibility-for-down-level-clients"></a>하위 클라이언트에 대 한 이전 버전과 호환성
일부 하위 수준 클라이언트 지원 하지 않습니다는 **시간**, **날짜**, **datetime2** 및 **datetimeoffset** 데이터 형식입니다. 다음 표에서는 상위 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 하위 클라이언트 간 형식 매핑을 보여 줍니다.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식|하위 클라이언트에 전달된 기본 문자열 리터럴 형식|하위 수준 ODBC|하위 수준 OLEDB|하위 수준 JDBC|하위 수준 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
|**datetimeoffset**|YYYY-월-일 h:mm: ss [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 또는 SQL_VARCHAR|DBTYPE_WSTR 또는 DBTYPE_STR|Java.sql.String|String 또는 SqString|  
  
## <a name="converting-date-and-time-data"></a>날짜 및 시간 데이터를 변환합니다.
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 날짜 및 시간 데이터 형식을 변환할 때 날짜나 시간으로 인식되지 않는 값은 모두 무시됩니다. 날짜 및 시간 데이터와 함께 CAST 및 CONVERT 함수를 사용 하는 방법에 대 한 정보를 참조 하십시오. [CAST 및 convert&#40; Transact SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
변환 됩니다 때 **time (n)**, 변환이 실패 및 오류 메시지 206이 발생 하는: "피연산자 유형 충돌: 날짜 시간와 호환 되지 않습니다."입니다.
  
변환 하려는 경우 **datetime**, 날짜가 복사 되 고 시간 구성 요소가 00:00:00.000로 설정 됩니다. 다음 코드에서는 `date` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.  
  
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
  
변환의 경우 **smalldatetime**때는 **날짜** 값이 범위에는 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), 날짜 구성 요소가 복사 되 고 시간 구성 요소가로 설정 되어 00시: 00입니다. 때는 **날짜** 의 범위 밖에 있는 값이는 **smalldatetime** 값, 오류 메시지 242가 발생 하는: "변환은 **날짜** 데이터 형식에  **smalldatetime** 범위를 벗어난 값;에서 결과 데이터 형식 및 **smalldatetime** 값은 NULL로 설정 합니다. 다음 코드에서는 `date` 값을 `smalldatetime` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환 됩니다 때 **datetimeoffset (n)**, 날짜가 복사 되 고 시간은 00: 00.0000000 + 00시 설정 됩니다. 다음 코드에서는 `date` 값을 `datetimeoffset(3)` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환 하려는 경우 **datetime2(n)**, 날짜 구성 요소가 복사 되 고 시간 구성 요소 (n) 값에 관계 없이 00:00:00.00로 설정 됩니다. 다음 코드에서는 `date` 값을 `datetime2(3)` 값으로 변환한 결과를 보여 줍니다.
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.00  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-date-to-other-date-and-time-types"></a>다른 날짜 및 시간 형식으로 변환 하는 동안 날짜
이 섹션에서는 발생 하는 상황을 설명 때는 **날짜** 데이터 형식을 다른 날짜 및 시간 데이터 형식으로 변환 됩니다.
  
변환 됩니다 때 **time (n)**, 변환이 실패 및 오류 메시지 206이 발생 하는: "피연산자 유형 충돌: 날짜 시간와 호환 되지 않습니다."입니다.
  
변환 하려는 경우 **datetime**, 날짜가 복사 됩니다. 다음 코드에서는 `date` 값을 `datetime` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환 됩니다 때 **smalldatetime**, **날짜** 값이 범위에는 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), 날짜 구성 요소가 복사 되 고 시간 구성 요소가로 설정 되어 00:00:00.000 합니다. 경우는 **날짜** 값의 범위를 벗어납니다.이 **smalldatetime** 값, 오류 메시지 242가 발생 하는: "변환 날짜 데이터 형식의 smalldatetime 데이터 형식 발생 범위를 벗어난 값입니다."; 및 **smalldatetime** 값은 NULL로 설정 합니다. 다음 코드에서는 `date` 값을 `smalldatetime` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환할 **datetimeoffset (n)**, 날짜가 복사 되 고 시간은 00: 00.0000000 + 00시 설정 됩니다. 다음 코드에서는 `date` 값을 `datetimeoffset(3)` 값으로 변환한 결과를 보여 줍니다.
  
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
  
변환 됩니다 때 **datetime2(n)**, 날짜 구성 요소가 복사 되 고 시간 구성 요소가 00:00. 000000로 설정 됩니다. 다음 코드에서는 `date` 값을 `datetime2(3)` 값으로 변환한 결과를 보여 줍니다.
  
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
문자열에 포함된 모든 부분의 형식이 올바른 경우 문자열 리터럴에서 날짜/시간 유형으로 변환할 수 있습니다. 그렇지 않으면 런타임 오류가 발생합니다. 날짜/시간 유형에서 문자열 리터럴로의 암시적 변환 또는 명시적 변환에 스타일을 지정하지 않은 경우 현재 세션의 기본 형식이 지정됩니다. 다음 표에서 문자열을 변환 하기 위한 규칙 리터럴을 **날짜** 데이터 형식입니다.
  
|입력 문자열 리터럴|**date**|  
|---|---|
|ODBC DATE|ODBC 문자열 리터럴에 매핑되는 **datetime** 데이터 형식입니다. 모든 할당 연산에 ODBC DATETIME 리터럴에서 **날짜** 형식 간에 암시적 변환이 발생 **datetime** 과 이러한 형식 변환 규칙으로 정의 된 대로 합니다.|  
|ODBC TIME|이전 ODBC DATE 규칙을 참조하세요.|  
|ODBC DATETIME|이전 ODBC DATE 규칙을 참조하세요.|  
|DATE만|중요하지 않음|  
|TIME만|기본값이 제공됩니다.|  
|TIMEZONE만|기본값이 제공됩니다.|  
|DATE+TIME|입력 문자열의 DATE 부분이 사용됩니다.|  
|DATE+TIMEZONE|허용되지 않습니다.|  
|TIME+TIMEZONE|기본값이 제공됩니다.|  
|DATE+TIME+TIMEZONE|로컬 DATETIME의 DATE 부분이 사용됩니다.|  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>참고 항목
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

