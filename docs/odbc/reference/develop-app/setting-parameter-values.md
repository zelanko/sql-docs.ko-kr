---
title: 매개 변수 값 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66811d2364db546c3bddd787c1e0794f936f97c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729161"
---
# <a name="setting-parameter-values"></a>매개 변수 값 설정
매개 변수의 값을 설정 하려면 응용 프로그램 매개 변수를 바인딩할 변수의 값을 간단히 설정 합니다. 이 중요 하지 않습니다이 값을 설정 하면 문이 실행 되기 전에 설정 됩니다. 응용 프로그램 변수 바인딩 전후 값을 설정할 수 및 원하는 횟수 만큼 값을 변경할 수 있습니다. 문이 실행 될 경우 드라이버는 단순히 변수의 현재 값을 검색 합니다. 준비 된 문을 한 번 이상 실행 될 때 특히 유용 응용 프로그램 새 값 설정 변수의 일부 또는 전부에 대 한 문이 실행 될 때마다 합니다. 이 예제를 보려면 [실행 준비](../../../odbc/reference/develop-app/prepared-execution-odbc.md)이 섹션의 앞부분에 나오는.  
  
 길이/표시기 버퍼에 대 한 호출에 바인딩된 경우 **SQLBindParameter**를 문이 실행 되기 전에 다음 값 중 하나로 설정 되어야 합니다.  
  
-   바인딩된 변수에 데이터의 바이트 길이입니다. 드라이버 변수 문자 또는 이진 인 경우에이 길이 확인 합니다 (*ValueType* SQL_C_CHAR 또는 SQL_C_BINARY).  
  
-   SQL_NTS 합니다. 데이터를 null로 끝나는 문자열입니다.  
  
-   SQL_NULL_DATA로 합니다. 데이터 값이 NULL 이면 및 드라이버에 바인딩된 변수 값을 무시 합니다.  
  
-   SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다. 매개 변수의 값이 함께 보낼 **SQLPutData**합니다. 자세한 내용은 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)이 섹션의 뒷부분에 나오는.  
  
 다음 표에서 바인딩된 변수 및 매개 변수 값의 다양 한 응용 프로그램을 설정 하는 길이/표시기 버퍼의 값을 보여 줍니다.  
  
|매개 변수<br /><br /> value|매개 변수<br /><br /> (SQL)<br /><br /> 데이터 형식|Variable (C)<br /><br /> 데이터 형식|값<br /><br /> 바인딩됨<br /><br /> 변수|값<br /><br /> 길이/표시기<br /><br /> 버퍼 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS 또는 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|[a] 10\0|SQL_NTS 또는 2|  
|오후 1 시|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|오후 1 시|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a], [c]|SQL_NTS 또는 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" null 종료 문자를 나타냅니다. Null 종료 문자는 길이/표시기 버퍼의 값은 SQL_NTS 하는 경우에 필요 합니다.  
  
 [b]이이 목록에서 숫자는 TIME_STRUCT 구조의 필드에 저장 된 숫자입니다.  
  
 [c]에서 문자열에는 ODBC 날짜 이스케이프 절을 사용합니다. 자세한 내용은 [날짜, 시간 및 타임 스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)합니다.  
  
 [d] 드라이버 SQL_NULL_DATA 같은 특수 값 여부를 확인 하기 위해이 값을 항상 확인 해야 합니다.  
  
 실행 시 매개 변수 값을 사용 하 여 수행 하는 드라이버는 드라이버에 따라 다릅니다. 필요한 경우 드라이버는 값에서에서 변환 합니다 바인딩된 변수의 C 데이터 유형 및 바이트 길이 SQL 데이터 형식, 전체 자릿수 및 소수 자릿수 매개 변수입니다. 대부분의 경우에서 드라이버는 데이터 소스에 값 다음 보냅니다. 경우에 따라 텍스트 값의 서식을 지정 하 고 데이터 원본에 문을 보낼 전에 SQL 문을 삽입 합니다.
