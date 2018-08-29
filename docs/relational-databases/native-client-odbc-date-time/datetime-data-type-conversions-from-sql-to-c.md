---
title: SQL에서 C로 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4133ce5044ceaf20dddafe6599456c415d085ed6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069821"
---
# <a name="datetime-data-type-conversions-from-sql-to-c"></a>날짜/시간 데이터 형식을 SQL에서 C로 변환
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜/시간 형식을 C 형식으로 변환할 때 고려할 문제를 설명합니다.  
  
## <a name="conversions"></a>변환  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|@shouldalert|@shouldalert|@shouldalert|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|@shouldalert|@shouldalert|@shouldalert|  
|SQL_TYPE_DATE|확인|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|확인|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|확인|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|확인|21|16|16|  
  
## <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|확인|변환 문제가 발생하지 않습니다.|  
|@shouldalert|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이전의 규칙이 적용됩니다.|  
|2|선행 공백과 후행 공백이 무시됩니다.|  
|3|문자열이 날짜, 시간, 표준 시간대 또는 표준 시간대 오프셋으로 구문 분석되고 소수 자릿수 초에 대해 9자리까지 허용합니다. 표준 시간대 오프셋이 구문 분석되는 경우 시간이 클라이언트 표준 시간대로 변환됩니다. 이 변환 중에 오류가 발생 하는 경우 SQLSTATE 22018 및 "Datetime 필드 오버플로" 메시지가 포함 된 진단 레코드가 생성 됩니다.|  
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
  
 이 항목의 표에서는 클라이언트로 반환된 형식과 바인딩 형식 간의 변환에 대해 설명합니다. 출력 매개 변수에 대 한에서 서버 유형을 지정 하는 경우 SQLBindParameter 서버의 실제 형식과 일치 하지 않습니다 서버에서 변환 하는 암시적 변환을 수행할지 하며 클라이언트에 반환 된 형식이 SQLBindParameter을 통해 지정 된 형식과 일치 합니다. 따라서 서버의 변환 규칙이 앞의 표에서 설명된 내용과 다를 경우 예기치 못한 변환 결과가 나타날 수 있습니다. 예를 들어 기본 날짜를 입력해야 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 날짜를 사용하지 않고 1900-1-1을 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
