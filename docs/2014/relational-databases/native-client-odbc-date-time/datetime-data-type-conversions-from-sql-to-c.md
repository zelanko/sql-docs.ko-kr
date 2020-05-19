---
title: SQL에서 C로 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8ef4d3f57f70641b738b21f86d55021e14606d57
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705478"
---
# <a name="conversions-from-sql-to-c"></a>SQL에서 C로 변환
  다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜/시간 형식을 C 형식으로 변환할 때 고려할 문제를 설명합니다.  
  
## <a name="conversions"></a>변환  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2, 3, 4, 5|2, 3, 6, 7, 8|2, 3, 9, 10, 11|2, 3, 6, 7|2, 3, 9, 10, 11|1|1|1|  
|SQL_WCHAR|2, 3, 4, 5|2, 3, 6, 7, 8|2, 3, 9, 10, 11|2, 3, 6, 7|2, 3, 9, 10, 11|1|1|1|  
|SQL_TYPE_DATE|정상|12|13|12|13, 23|14|16|16|  
|SQL_SS_TIME2|12|8|15|정상|10, 23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7, 8|정상|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18, 22|7, 8, 20|20|7, 20|정상|21|16|16|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|정상|변환 문제가 발생하지 않습니다.|  
|1|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전의 규칙이 적용됩니다.|  
|2|선행 공백과 후행 공백이 무시됩니다.|  
|3|문자열이 날짜, 시간, 표준 시간대 또는 표준 시간대 오프셋으로 구문 분석되고 소수 자릿수 초에 대해 9자리까지 허용합니다. 표준 시간대 오프셋이 구문 분석되는 경우 시간이 클라이언트 표준 시간대로 변환됩니다. 이 변환 중에 오류가 발생 하면 SQLSTATE 22018 및 "Datetime 필드 오버플로" 라는 메시지가 포함 된 진단 레코드가 생성 됩니다.|  
|4|값이 유효한 날짜, 타임스탬프 또는 타임스탬프 오프셋 값이 아니면 SQLSTATE 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|5|시간이 0이 아니면 SQLSTATE 01S07 및 "일부가 잘렸습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|6|값이 유효한 시간, 타임스탬프 또는 타임스탬프 오프셋 값이 아니면 SQLSTATE 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|7|날짜 구성 요소가 무시됩니다.|  
|8|소수 자릿수 초가 0이 아니면 SQLSTATE 01S07 및 "일부가 잘렸습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|9|값이 유효한 날짜, 시간, 타임스탬프 또는 타임스탬프 오프셋 값이 아니면 SQLSTATE 22018 및 "캐스트 사양의 문자 값이 올바르지 않습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|10|값이 유효한 시간이 아니면 날짜 구성 요소가 현재 클라이언트 날짜로 설정됩니다.|  
|11|값이 유효한 날짜가 아니면 시간이 0으로 설정됩니다.|  
|12|SQLSTATE 07006 및 "제한된 데이터 형식 특성을 위반했습니다"라는 메시지가 표시되고 진단 레코드가 생성됩니다.|  
|13|시간이 0으로 설정됩니다.|  
|14|버퍼의 크기가 작아 SQL_DATE_STRUCT를 수용할 수 없으면 SQLSTATE 22003 및 "숫자 값이 범위를 벗어났습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|15|날짜가 현재 클라이언트 날짜로 설정됩니다.|  
|16|버퍼의 크기가 작아 변환된 문자열 중 소수 자릿수 초만 수용할 수 있는 경우 잘림이 발생하고 SQLSTATE 22001 및 '문자열 데이터의 오른쪽이 잘렸습니다.'라는 메시지가 포함된 진단 레코드가 생성됩니다. 버퍼의 크기가 작아 문자열 값을 날짜, 시간 또는 오프셋 구성 요소가 잘리지 않게 수용할 수 없으면 SQLSTATE 22003 및 "숫자 값이 범위를 벗어났습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다. 날짜 및 타임스탬프 오프셋의 경우 변환된 문자열의 가장 오른쪽 부분에 소수 자릿수 초가 포함되어 있지 않으므로 SQLSTATE 01004가 생성될 수 없습니다. 따라서 잘림이 발생하여 데이터가 손실됩니다.|  
|17|버퍼의 크기가 작아 SQL_SS_TIME2_STRUCT를 수용할 수 없으면 SQLSTATE 22003 및 "숫자 값이 범위를 벗어났습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|18|시간이 0이 아니면 SQLSTATE 01S07 및 "일부가 잘렸습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|19|서버 유형이 datetime 또는 smalldatetime이면 값이 TDS 연결 형식에 해당하며 smalldatetime은 4바이트 값이고 datetime은 8바이트 값입니다.<br /><br /> 서버 유형이 datetime2이면 값이 SQL_TIMESTAMP_STRUCT로 반환됩니다. 버퍼의 크기가 작아 반환된 값을 수용할 수 없으면 SQLSTATE 22003 및 "숫자 값이 범위를 벗어났습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|20|시간이 클라이언트 표준 시간대로 변환됩니다. 변환 중 오류가 발생하면 SQLSTATE 22008 및 "Datetime 필드 오버플로" 메시지가 포함된 진단 레코드가 생성됩니다.|  
|21|버퍼의 크기가 작아 SQL_SS_TIMESTAMPOFFSET_STRUCT를 수용할 수 없으면 값이 SQL_SS_TIMESTAMPOFFSET_STRUCT로 반환됩니다. 그렇지 않으면 SQLSTATE 22003 및 "숫자 값이 범위를 벗어났습니다"라는 메시지가 포함된 진단 레코드가 생성됩니다.|  
|22|날짜가 추출되기 전에 값이 클라이언트 표준 시간대로 변환됩니다. 따라서 타임스탬프 오프셋 형식에 대한 다른 변환에서 일관성이 유지됩니다. 변환 중 오류가 발생하면 SQLSTATE 22008 및 "Datetime 필드 오버플로" 메시지가 포함된 진단 레코드가 생성됩니다. 이로 인해 날짜가 단순 잘림으로 얻은 값과 달라집니다.|  
  
 이 항목의 표에서는 클라이언트로 반환된 형식과 바인딩 형식 간의 변환에 대해 설명합니다. 출력 매개 변수의 경우 SQLBindParameter에 지정 된 서버 형식이 서버의 실제 형식과 일치 하지 않으면 서버에 의해 암시적 변환이 수행 되며 클라이언트로 반환 되는 형식은 SQLBindParameter를 통해 지정 된 형식과 일치 합니다. 따라서 서버의 변환 규칙이 앞의 표에 나열 된 것과 다를 경우 예기치 않은 변환 결과가 발생할 수 있습니다. 예를 들어 기본 날짜를 입력해야 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 날짜를 사용하지 않고 1900-1-1을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;날짜 및 시간 기능 향상](date-and-time-improvements-odbc.md)  
  
  
