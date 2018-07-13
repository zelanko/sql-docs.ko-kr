---
title: C에서 SQL로 변환을 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 638f3acea8ba4d9925851a26bd84ab20f76c38c9
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410081"
---
# <a name="conversions-from-c-to-sql"></a>C에서 SQL로의 변환
  이 항목에서는 C 형식에서 변환 하는 경우 고려해 야 할 문제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜/시간 형식입니다.  
  
 다음 표에서 설명하는 변환은 클라이언트에서 수행되는 변환에 해당합니다. 클라이언트가 매개 변수에 대해 소수 자릿수 초의 전체 자릿수를 서버에 정의된 것과 다르게 지정하는 경우 클라이언트 변환이 성공하더라도 서버는 `SQLExecute` 또는 `SQLExecuteDirect`가 호출될 때 오류를 반환합니다. 특히 ODBC는 모든 소수 자릿수 초 잘림을 오류로 처리하는 반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 반올림 동작을 수행합니다. 예를 들어 `datetime2(6)`를 `datetime2(2)`로 변환하는 경우 반올림이 수행됩니다. datetime 열 값은 1/300초로 반올림되며 smalldatetime 열은 서버에 의해 0초로 설정됩니다.  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|해당 사항 없음|해당 사항 없음|1,10,11|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|1,10,11|해당 사항 없음|해당 사항 없음|  
|SQL_C_CHAR/SQL_WCHAR(date)|9|9|9|9,6|9,5,6|해당 사항 없음|해당 사항 없음|  
|SQL_C_CHAR/SQL_WCHAR(time2)|9|9,3|9,10|9,7,10|9,5,7,10|해당 사항 없음|해당 사항 없음|  
|SQL_C_CHAR/SQL_WCHAR(datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|해당 사항 없음|해당 사항 없음|  
|SQL_C_CHAR/SQL_WCHAR(datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|해당 사항 없음|해당 사항 없음|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|-|변환이 지원되지 않습니다. SQLSTATE 07006 및 "제한된 데이터 형식 특성을 위반했습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.|  
|1|지정된 데이터가 유효하지 않으면 SQLSTATE 22007 "잘못된 날짜 시간 형식입니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.|  
|2|시간 필드는 0이어야 하며 그렇지 않으면 SQLSTATE 22008 및 "일부가 잘렸습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|3|소수 자릿수 초는 0이어야 하며 그렇지 않으면 SQLSTATE 22008 및 "일부가 잘렸습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|4|날짜 구성 요소가 무시됩니다.|  
|5|표준 시간대가 클라이언트의 표준 시간대 설정으로 지정됩니다.|  
|6|시간이 0으로 설정됩니다.|  
|7|날짜가 현재 날짜로 설정됩니다.|  
|8|시간이 클라이언트의 표준 시간대에서 UTC로 변환됩니다. 변환 중 오류가 발생하면 SQLSTATE 22008 및 "Datetime 필드 오버플로" 메시지가 포함된 진단 레코드가 생성됩니다.|  
|9|첫 번째로 발견되는 문장 부호 문자 및 나머지 구성 요소의 유무에 따라 문자열이 date, datetime, datetimeoffset 또는 time 값으로 구문 분석되고 변환됩니다. 그런 다음 위 표에서 이 프로세스에 의해 발견된 원본 형식에 대한 규칙에 따라 문자열이 대상 형식으로 변환됩니다. 데이터를 구분 분석하는 중에 오류가 발견되면 SQLSTATE 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다. datetime 및 smalldatetime 매개 변수의 경우 연도가 이러한 형식에서 지원하는 범위를 벗어나면 SQLSATE 22007 및 "잘못된 날짜 시간 형식입니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.<br /><br /> datetimeoffset의 경우 값은 UTC 변환이 요청되지 않더라도 UTC로 변환된 후의 범위 안에 포함되어야 합니다. 왜냐하면 TDS와 서버는 항상 datetimeoffset 값의 시간을 UTC에 맞게 정규화하므로 클라이언트에서 UTC로의 변환 후 시간 구성 요소가 지원 범위에 포함되는지 확인해야 하기 때문입니다. 값이 지원되는 UTC 범위 내에 포함되지 않으면 SQLSTATE 22007 및 "잘못된 날짜 시간 형식입니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.|  
|10|데이터 손실을 유발하는 잘림이 발생하면 SQLSTATE 22008 및 "잘못된 날짜 시간 형식입니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다. 이 오류는 값이 서버에서 사용된 UTC 범위로 표현할 수 있는 범위 밖에 있는 경우에도 발생합니다.|  
|11|데이터의 바이트 길이가 SQL 형식에 필요한 구조의 크기와 같지 않은 경우 SQLSTATE 22003 및 "숫자 값이 범위를 벗어났습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.|  
|12|바이트 길이가 4 또는 8인 데이터는 원시 TDS smalldatetime 또는 datetime 형식으로 서버에 전송되고, 바이트 길이가 SQL_TIMESTAMP_STRUCT의 크기와 정확히 일치하는 데이터는 TDS 형식의 datetime2로 변환됩니다.|  
|13|데이터 손실을 유발하는 잘림이 발생하면 SQLSTATE 22001 및 "문자열 데이터의 오른쪽이 잘렸습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.<br /><br /> 소수 자릿수 초 자릿수 (소수)는 대상 열의 크기는 다음에 따라 결정 됩니다.<br /><br /> **형식:** SQL_C_TYPE_TIMESTAMP<br /><br /> 암시된 소수 자릿수<br /><br /> 0<br /><br /> 19<br /><br /> 암시된 소수 자릿수<br /><br /> 1..9<br /><br /> 21..29<br /><br /> 그러나 SQL_C_TYPE_TIMESTAMP의 경우에는 소수 자릿수 초를 데이터 손실 없이 3자리로 나타낼 수 있고 열 크기가 23 이상인 경우 소수 자릿수 초의 자릿수는 정확히 3자리로 생성됩니다. 이 동작은 이전 ODBC 드라이버를 사용하여 개발된 응용 프로그램과의 호환성을 보장합니다.<br /><br /> 테이블의 범위보다 열 크기가 큰 경우 소수 자릿수가 9인 것으로 간주됩니다. 이 변환은 소수 자릿수 초의 자릿수를 ODBC에서 허용하는 최대값인 9자리까지 허용합니다.<br /><br /> 크기가 0인 열은 ODBC에서 변수 길이 문자 형식의 크기에 제한이 없음을 의미합니다(SQL_C_TYPE_TIMESTAMP의 3자리 규칙이 적용되지 않는 경우 9자리). 고정 길이 문자 형식의 열 크기를 0으로 지정하면 오류가 발생합니다.|  
|해당 사항 없음|기존 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 및 이전 동작이 유지됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
