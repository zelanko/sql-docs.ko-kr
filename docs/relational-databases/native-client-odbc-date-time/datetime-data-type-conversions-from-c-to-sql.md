---
title: C에서 SQL로의 변환 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f8161ea07e394192e972caf4f772d9e7def36e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301794"
---
# <a name="datetime-data-type-conversions-from-c-to-sql"></a>날짜/시간 데이터 형식을 C에서 SQL로 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 C 형식에서 날짜/시간 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유형으로 변환할 때 고려해야 할 문제를 나열합니다.  
  
 다음 표에서 설명하는 변환은 클라이언트에서 수행되는 변환에 해당합니다. 클라이언트가 서버에 정의된 것과 다른 매개 변수에 대해 분수 초 정밀도를 지정하는 경우 클라이언트 변환이 성공할 수 있지만 **SQLExecute** 또는 **SQLExecuteDirect가** 호출될 때 서버가 오류를 반환합니다. 특히 ODBC는 분수 초의 모든 잘림을 오류로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 처리하는 반면 동작은 반올림됩니다. 예를 들어 반올림은 **datetime2(6)에서** **datetime2(2)로**이동하면 발생합니다. datetime 열 값은 1/300초로 반올림되며 smalldatetime 열은 서버에 의해 0초로 설정됩니다.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|해당 없음|해당 없음|1,10,11|해당 없음|해당 없음|해당 없음|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|해당 없음|해당 없음|해당 없음|해당 없음|1,10,11|해당 없음|해당 없음|  
|SQL_C_CHAR/SQL_WCHAR(date)|9|9|9|9,6|9,5,6|해당 없음|해당 없음|  
|SQL_C_CHAR/SQL_WCHAR(time2)|9|9,3|9,10|9,7,10|9,5,7,10|해당 없음|해당 없음|  
|SQL_C_CHAR/SQL_WCHAR(datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|해당 없음|해당 없음|  
|SQL_C_CHAR/SQL_WCHAR(datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|해당 없음|해당 없음|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|해당 없음|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
-   **-**: 변환이 지원되지 않습니다. SQLSTATE 07006 및 "제한된 데이터 형식 특성을 위반했습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.  
  
-   **1**: 제공된 데이터가 유효하지 않으면 SQLSTATE 22007 및 "잘못된 datetime 형식"이라는 메시지와 함께 진단 레코드가 생성됩니다.  
  
-   **2**: 시간 필드가 0이어야하거나 SQLSTATE 22008 및 "분수 잘림"이라는 메시지와 함께 진단 레코드가 생성됩니다.  
  
-   **3**: 분수 초가 0이어야 하거나 SQLSTATE 22008 및 "분수 잘림"이라는 메시지로 진단 레코드가 생성됩니다.  
  
-   **4**: 날짜 구성 요소가 무시됩니다.  
  
-   **5**: 시간대가 클라이언트의 시간대 설정으로 설정됩니다.  
  
-   **6**: 시간이 0으로 설정됩니다.  
  
-   **7**: 날짜가 현재 날짜로 설정됩니다.  
  
-   **8**: 시간이 클라이언트의 시간대에서 UTC로 변환됩니다. 변환 중 오류가 발생하면 SQLSTATE 22008 및 "Datetime 필드 오버플로" 메시지가 포함된 진단 레코드가 생성됩니다.  
  
-   **9**: 문자열은 발생한 첫 번째 문장 부호 문자와 나머지 구성 요소의 존재 여부에 따라 구문 분석되고 날짜, 날짜 시간, 날짜 시간 오프셋 또는 시간 값으로 변환됩니다. 그런 다음 위 표에서 이 프로세스에 의해 발견된 원본 형식에 대한 규칙에 따라 문자열이 대상 형식으로 변환됩니다. 데이터를 구분 분석하는 중에 오류가 발견되면 SQLSTATE 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다. datetime 및 smalldatetime 매개 변수의 경우 연도가 이러한 형식에서 지원하는 범위를 벗어나면 SQLSATE 22007 및 "잘못된 날짜 시간 형식입니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.  
  
     datetimeoffset의 경우 값은 UTC 변환이 요청되지 않더라도 UTC로 변환된 후의 범위 안에 포함되어야 합니다. 왜냐하면 TDS와 서버는 항상 datetimeoffset 값의 시간을 UTC에 맞게 정규화하므로 클라이언트에서 UTC로의 변환 후 시간 구성 요소가 지원 범위에 포함되는지 확인해야 하기 때문입니다. 값이 지원되는 UTC 범위 내에 포함되지 않으면 SQLSTATE 22007 및 "잘못된 날짜 시간 형식입니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.  
  
-   **10**: 데이터 손실이 있는 잘림이 발생하면 SQLSTATE 22008 및 "잘못된 시간 형식"이라는 메시지와 함께 진단 레코드가 생성됩니다. 이 오류는 값이 서버에서 사용된 UTC 범위로 표현할 수 있는 범위 밖에 있는 경우에도 발생합니다.  
  
-   **11**: 데이터의 바이트 길이가 SQL 형식에 필요한 구조체의 크기와 같지 않으면 SQLSTATE 22003 및 "숫자 값 범위"라는 메시지와 함께 진단 레코드가 생성됩니다.  
  
-   **12**: 데이터의 바이트 길이가 4 또는 8이면 데이터는 원시 TDS smalldatetime 또는 datetime 형식으로 서버로 전송됩니다. 바이트 길이가 SQL_TIMESTAMP_STRUCT의 크기와 정확히 일치하는 데이터는 TDS 형식의 datetime2로 변환됩니다.  
  
-   **13**: 데이터 손실이 있는 잘림이 발생하면 SQLSTATE 22001및 "문자열 데이터, 오른쪽 잘린"이라는 메시지와 함께 진단 레코드가 생성됩니다.  
  
     분수 초 자릿수(축척)는 다음 표에 따라 대상 열의 크기에서 결정됩니다.  
  
    ||||  
    |-|-|-|  
    |Type|암시된 소수 자릿수<br /><br /> 0|암시된 소수 자릿수<br /><br /> 1..9|  
    |SQL_C_TYPE_TIMESTAMP|19|21..29|  
  
     그러나 SQL_C_TYPE_TIMESTAMP의 경우에는 소수 자릿수 초를 데이터 손실 없이 3자리로 나타낼 수 있고 열 크기가 23 이상인 경우 소수 자릿수 초의 자릿수는 정확히 3자리로 생성됩니다. 이 동작은 이전 ODBC 드라이버를 사용하여 개발된 애플리케이션과의 호환성을 보장합니다.  
  
     테이블의 범위보다 열 크기가 큰 경우 소수 자릿수가 9인 것으로 간주됩니다. 이 변환은 소수 자릿수 초의 자릿수를 ODBC에서 허용하는 최대값인 9자리까지 허용합니다.  
  
     크기가 0인 열은 ODBC에서 변수 길이 문자 형식의 크기에 제한이 없음을 의미합니다(SQL_C_TYPE_TIMESTAMP의 3자리 규칙이 적용되지 않는 경우 9자리). 고정 길이 문자 형식의 열 크기를 0으로 지정하면 오류가 발생합니다.  
  
-   **해당/ A** [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] : 기존 및 이전 동작이 유지됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;날짜 및 시간 개선](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
