---
title: ODBC 날짜 및 시간 향상을 위한 데이터 형식 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], data type support
- ODBC, date/time improvements
ms.assetid: 8e0d9ba2-3ec1-4680-86e3-b2590ba8e2e9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 49f5e5d90a24aed8a717edb2f1c4efe4a2fd5e07
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705506"
---
# <a name="data-type-support-for-odbc-date-and-time-improvements"></a>ODBC 날짜 및 시간 기능 향상을 위한 데이터 형식 지원
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식을 지원하는 ODBC 형식에 대한 정보를 제공합니다.  
  
## <a name="data-type-mapping-in-parameters-and-resultsets"></a>매개 변수 및 결과 집합의 데이터 형식 매핑  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC에는 ODBC 데이터 형식(SQL_TYPE_TIMESTAMP 및 SQL_TIMESTAMP) 외에 새 서버 유형을 노출하기 위한 두 개의 새로운 데이터 형식이 추가되었습니다.  
  
-   SQL_SS_TIME2  
  
-   SQL_SS_TIMESTAMPOFFSET  
  
 다음 표는 데이터 전체 서버 유형 매핑을 보여 줍니다. 이 표의 일부 셀에는 두 개의 항목이 포함되어 있는데, 이 경우 첫 번째 항목은 ODBC 3.0 값이고 두 번째 항목은 ODBC 2.0 값입니다.  
  
|SQL Server 데이터 형식|SQL 데이터 형식|값|  
|--------------------------|-------------------|-----------|  
|DateTime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93(sql.h)<br /><br /> 11(sqlext.h)|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93(sql.h)<br /><br /> 11(sqlext.h)|  
|날짜|SQL_TYPE_DATE<br /><br /> SQL_DATE|91 (sql .h)<br /><br /> 9 (sqlext .h)|  
|Time|SQL_SS_TIME2|-154 (SQLNCLI)|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|-155(SQLNCLI.h)|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93(sql.h)<br /><br /> 11(sqlext.h)|  
  
 다음 표에서는 해당되는 구조 및 ODBC C 형식을 보여 줍니다. ODBC는 드라이버 정의 C 형식을 허용하지 않으므로 time 및 datetimeoffset에 대해서는 SQL_C_BINARY가 이진 구조로 사용됩니다.  
  
|SQL 데이터 형식|메모리 레이아웃|기본 C 데이터 형식|값(sqlext.h)|  
|-------------------|-------------------|-------------------------|------------------------|  
|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|SQL_TIMESTAMP_STRUCT<br /><br /> TIMESTAMP_STRUCT|SQL_C_TYPE_TIMESTAMP<br /><br /> SQL_C_TIMESTAMP|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|  
|SQL_TYPE_DATE<br /><br /> SQL_DATE|SQL_DATE_STRUCT<br /><br /> DATE_STRUCT|SQL_C_TYPE_DATE<br /><br /> SQL_C_DATE|SQL_TYPE_DATE<br /><br /> SQL_DATE|  
|SQL_SS_TIME2|SQL_SS_TIME2_STRUCT|SQL_C_SS_TIME2<br /><br /> SQL_C_BINARY(ODBC 3.5 및 이전)|0x4000(sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
|SQL_SS_TIMESTAMPOFFSET|SQL_SS_TIMESTAMPOFFSET_STRUCT|SQL_C_SS_TIMESTAMPOFFSET<br /><br /> SQL_C_BINARY(ODBC 3.5 및 이전)|0x4001(sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
  
 SQL_C_BINARY 바인딩이 지정된 경우 맞춤 검사가 수행되며 잘못된 맞춤에 대해서는 오류가 보고됩니다. 이 오류에 대한 SQLSTATE는 IM016이 되며 메시지는 "잘못된 구조체 맞춤"입니다.  
  
## <a name="data-formats-strings-and-literals"></a>데이터 형식: 문자열 및 리터럴  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식, ODBC 데이터 형식, 그리고 ODBC 문자열 리터럴 간의 매핑을 보여 줍니다.  
  
|SQL Server 데이터 형식|ODBC 데이터 형식|클라이언트 변환을 위한 문자열 형식|  
|--------------------------|--------------------|------------------------------------------|  
|DateTime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'yyyy-mm-dd hh:mm:ss[.999]'<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Datetime에 대해 최대 3자리의 소수 자릿수 초를 지원합니다.|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'yyyy-mm-dd hh:hh:ss'<br /><br /> 이 데이터 형식의 정확도는 1분 단위입니다. 초 구성 요소 부분은 출력 시 0이 되고, 입력 시 서버에 의해 반올림됩니다.|  
|날짜|SQL_TYPE_DATE<br /><br /> SQL_DATE|'yyyy-mm-dd'|  
|Time|SQL_SS_TIME2|'hh:mm:ss[.9999999]'<br /><br /> 필요한 경우 소수 자릿수 초를 일곱 자리까지 지정할 수 있습니다.|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|' yyyy-mm-dd hh: mm: ss [. 9999999] '<br /><br /> 필요한 경우 소수 자릿수 초를 일곱 자리까지 지정할 수 있습니다.|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|'yyyy-mm-dd hh:mm:ss[.9999999] +/- hh:mm'<br /><br /> 필요한 경우 소수 자릿수 초를 일곱 자리까지 지정할 수 있습니다.|  
  
 날짜/시간 리터럴에 대한 ODBC 이스케이프 시퀀스에는 변경 내용이 없습니다.  
  
 결과의 소수 자릿수 초는 항상 콜론(:)이 아닌 점(.)을 사용합니다.  
  
 애플리케이션에 반환되는 문자열 값은 지정된 열에 대해 항상 동일합니다. 연도, 월, 일, 시, 분 및 초 구성 요소의 앞부분에는 최대 너비까지 0이 채워지며, datetime 값에서 날짜와 시간 사이에는 하나의 공백이 있습니다. datetimeoffset 값의 시간과 시간대 오프셋 사이에도 하나의 공백이 있습니다. 시간대 오프셋 앞에는 항상 부호가 옵니다. 오프셋이 0인 경우 더하기(+) 부호가 사용됩니다. 필요한 경우 소수 자릿수 초의 뒷부분은 열에 정의된 전체 자릿수까지 0으로 채워집니다. datetime 열의 경우 소수 자릿수 초는 3자리입니다. smalldatetime 열의 경우 소수 자릿수 초의 자릿수가 정의되지 않으며 초는 항상 0이 됩니다.  
  
 빈 문자열은 유효한 날짜/시간 리터럴이 아니며 NULL 값을 나타내지 않습니다. 빈 문자열을 날짜/시간 값으로 변환하려고 시도하면 "캐스트 사양의 문자 값이 올바르지 않습니다"라는 메시지와 함께 SQLState 22018 오류가 발생합니다.  
  
 문자열 매개 변수는 같은 형식의 문자열로 변환해야 합니다. 단, 0시 0분 시간대의 부호는 더하기 또는 빼기 모두 될 수 있으며, 소수 자릿수 초의 뒤에는 최대 9자리까지 0이 올 수 있습니다. 시간 구성 요소는 소수 자릿수 초의 자릿수 없이 소수점으로 끝날 수 있습니다.  
  
 현재 드라이버는 문장 부호 문자 앞뒤에 추가 공백을 허용하며, 시간과 시간대 오프셋 사이의 공백은 선택 사항입니다. 그러나 이 부분은 향후 릴리스에서 변경될 수 있으므로 현재 동작에 의존하도록 애플리케이션을 작성하면 안 됩니다.  
  
## <a name="data-formats-data-structures"></a>데이터 형식: 데이터 구조  
 아래 설명된 구조에서 ODBC는 일반 달력에서 비롯된 다음과 같은 제약 사항을 지정합니다.  
  
-   월 범위는 1에서 12까지입니다.  
  
-   일 필드의 범위는 1에서 해당 월의 일 수까지이며, 윤년을 고려하여 연도 및 월 필드와 일관성을 유지해야 합니다.  
  
-   시 범위는 0에서 23까지입니다.  
  
-   분 범위는 0에서 59까지입니다.  
  
-   초 범위는 0에서 61.9까지입니다. 이는 항성시와의 동기화를 유지하기 위한 최대 2초의 윤초를 허용합니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 윤초가 허용되지 않으므로 초 값이 59보다 클 경우 서버 오류가 발생합니다.  
  
 다음과 같은 기존 ODBC 구조체 구현은 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식을 지원하도록 수정되었습니다. 단, 정의는 변경되지 않았습니다.  
  
-   DATE_STRUCT  
  
-   TIME_STRUCT  
  
-   TIMESTAMP_STRUCT  
  
 다음은 두 개의 새로운 구조체입니다.  
  
-   SQL_SS_TIME2_STRUCT  
  
-   SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
### <a name="sql_ss_time2_struct"></a>SQL_SS_TIME2_STRUCT  
 이 구조체는 32비트와 64비트 운영 체제 모두에서 12바이트까지 채워집니다.  
  
```  
typedef struct tagSS_TIME2_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
} SQL_SS_TIME2_STRUCT;  
```  
  
### <a name="sql_ss_timestampoffset_struct"></a>SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
```  
typedef struct tagSS_TIMESTAMPOFFSET_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
   SQLSMALLINT timezone_hour;  
   SQLSMALLINT timezone_minute;  
} SQL_SS_TIMESTAMPOFFSET_STRUCT;  
```  
  
 `timezone_hour`가 음수인 경우 `timezone_minute`는 음수 또는 0이어야 합니다. `timezone_hour`가 양수인 경우 `timezone_minute`는 양수 또는 0이어야 합니다. `timezone_hour`가 0인 경우 `timezone_minute`는 -59에서 +59까지의 어떤 수라도 될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;날짜 및 시간 기능 향상](date-and-time-improvements-odbc.md)  
  
  
