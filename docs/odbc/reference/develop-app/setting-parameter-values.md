---
title: 매개 변수 값 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0e41f775ef6640f4f82aa16cea038becc305bf5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setting-parameter-values"></a>매개 변수 값 설정
응용 프로그램은 매개 변수 값을 설정 하려면 단순히 매개 변수에 바인딩된 변수 값을 설정 합니다. 이 중요 하지 않습니다이 값을 설정 하는 경우 문을 실행 하기 전에 설정 됩니다. 이전 또는 변수를 바인딩한 후 응용 프로그램 값을 설정할 수 및 원하는 횟수 만큼 값을 변경할 수는 있습니다. 문이 실행 되는 경우 드라이버는 단순히 변수의 현재 값을 검색 합니다. 준비 된 문을 두 번 이상; 실행 될 때 특히 유용 응용 프로그램이 새 값을 설정 일부 또는 모든 변수는 문이 실행 될 때마다 합니다. 이 예제를 보려면 [실행 준비](../../../odbc/reference/develop-app/prepared-execution-odbc.md)이 섹션의 앞부분에 나오는 합니다.  
  
 길이/표시기 버퍼에 대 한 호출에 바인딩된 경우 **SQLBindParameter**, 문을 실행 하기 전에 다음 값 중 하나로 설정 되어야 합니다.  
  
-   바인딩된 변수에서 데이터의 바이트 길이입니다. 드라이버 변수 문자 또는 이진 인 경우에이 길이 확인 (*ValueType* SQL_C_CHAR 또는 SQL_C_BINARY).  
  
-   SQL_NTS 합니다. 데이터는 null로 끝나는 문자열.  
  
-   SQL_NULL_DATA 합니다. 데이터 값이 NULL 이면 및 드라이버를 바인딩된 변수로의 값을 무시 합니다.  
  
-   SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다. 매개 변수의 값이 함께 보낼 **SQLPutData**합니다. 자세한 내용은 참조 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 다음 표에서 바인딩된 변수 및 다양 한 매개 변수 값에 대 한 응용 프로그램을 설정 하는 길이/표시기 버퍼의 값을 보여 줍니다.  
  
|매개 변수<br /><br /> value|매개 변수<br /><br /> (SQL)<br /><br /> 데이터 형식|Variable (C)<br /><br /> 데이터 형식|값<br /><br /> 바인딩됨<br /><br /> 변수|값<br /><br /> 길이/표시기<br /><br /> 버퍼 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS 또는 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0 [a]|SQL_NTS 또는 2|  
|오후 1|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|오후 1|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a], [c + +]|SQL_NTS 또는 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" null 종료 문자를 나타냅니다. Null 종결 문자는 길이/표시기 버퍼의 값은 SQL_NTS 하는 경우에 필요 합니다.  
  
 [이 목록에 있는 b]는 숫자는 TIME_STRUCT 구조체의 필드에 저장 된 숫자입니다.  
  
 [문자열 c]에서 ODBC 날짜 이스케이프 절을 사용합니다. 자세한 내용은 참조 [Date, Time 및 Timestamp 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)합니다.  
  
 [이 값을 SQL_NULL_DATA 같은 특수 한 값을 확인 d] 드라이버를 항상 확인 해야 합니다.  
  
 실행 시 매개 변수 값으로 드라이버를 수행 하는 작업은 드라이버에 따라 다릅니다. 필요에 따라 드라이버가 값 SQL 데이터 형식, 전체 자릿수 및 소수 자릿수가 매개 변수를에 바인딩된 변수로의 C 데이터 형식 및 바이트 길이에서 변환 합니다. 대부분의 경우 드라이버 그런 다음 데이터 원본에 값을 보냅니다. 경우에 따라이 클래스는 텍스트로 값의 서식을 데이터 원본에는 문을 보내기 전에 SQL 문에 삽입 합니다.
