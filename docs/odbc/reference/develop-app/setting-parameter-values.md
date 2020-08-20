---
description: 매개 변수 값 설정
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af2992ea66601ec0ae4804e327863e6abb285d73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476425"
---
# <a name="setting-parameter-values"></a>매개 변수 값 설정
매개 변수 값을 설정 하기 위해 응용 프로그램은 매개 변수에 바인딩된 변수의 값만 설정 합니다. 문이 실행 되기 전에 설정 된 경우이 값이 설정 된 경우에는 중요 하지 않습니다. 응용 프로그램은 변수를 바인딩하기 전이나 후에 값을 설정할 수 있으며, 원하는 횟수 만큼 값을 변경할 수 있습니다. 문이 실행 될 때 드라이버는 단순히 변수의 현재 값을 검색 합니다. 이는 준비 된 문이 두 번 이상 실행 되는 경우에 특히 유용 합니다. 응용 프로그램은 문이 실행 될 때마다 변수의 일부 또는 전체에 대 한 새 값을 설정 합니다. 이에 대 한 예는이 섹션의 앞부분에 나오는 [실행 준비](../../../odbc/reference/develop-app/prepared-execution-odbc.md)를 참조 하세요.  
  
 **SQLBindParameter**에 대 한 호출에서 길이/표시기 버퍼가 바인딩된 경우 문이 실행 되기 전에 다음 값 중 하나로 설정 되어야 합니다.  
  
-   바인딩된 변수에 있는 데이터의 바이트 길이입니다. 드라이버는 변수가 문자 또는 이진 인 경우에만이 길이를 확인 합니다 (*ValueType* 은 SQL_C_CHAR 또는 SQL_C_BINARY).  
  
-   SQL_NTS. 데이터는 null로 끝나는 문자열입니다.  
  
-   SQL_NULL_DATA. 데이터 값이 NULL이 고 드라이버가 바인딩된 변수 값을 무시 합니다.  
  
-   SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다. 매개 변수 값은 **Sqlputdata**를 사용 하 여 전송 됩니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [Long 데이터 보내기](../../../odbc/reference/develop-app/sending-long-data.md)를 참조 하십시오.  
  
 다음 표에서는 응용 프로그램에서 다양 한 매개 변수 값에 대해 설정 하는 길이/표시기 버퍼와 바인딩된 변수의 값을 보여 줍니다.  
  
|매개 변수<br /><br /> 값|매개 변수<br /><br /> SQL<br /><br /> 데이터 형식|변수 (C)<br /><br /> 데이터 형식|의 값<br /><br /> 바인딩됨<br /><br /> 변수|의 값<br /><br /> 길이/표시기<br /><br /> 버퍼 [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS 또는 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS 또는 2|  
|오후 1 시|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13, 0, 0 [b]|--|  
|오후 1 시|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13:00:00 '} \ 0 [a], [c]|SQL_NTS 또는 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\ 0"은 null 종료 문자를 나타냅니다. Null 종료 문자는 길이/표시기 버퍼의 값이 SQL_NTS 경우에만 필요 합니다.  
  
 [b]이 목록에 있는 숫자는 TIME_STRUCT 구조체의 필드에 저장 된 숫자입니다.  
  
 [c] 문자열에 ODBC 날짜 이스케이프 절이 사용 됩니다. 자세한 내용은 [날짜, 시간 및 타임 스탬프 리터럴](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)을 참조 하세요.  
  
 [d] 드라이버는 항상이 값을 확인 하 여 SQL_NULL_DATA와 같은 특수 한 값 인지 확인 해야 합니다.  
  
 실행 시 드라이버에서 매개 변수 값을 사용 하는 것은 드라이버에 따라 달라 집니다. 필요한 경우 드라이버는 바인딩된 변수의 C 데이터 형식 및 바이트 길이에서 매개 변수의 SQL 데이터 형식, 전체 자릿수 및 소수 자릿수로 값을 변환 합니다. 대부분의 경우 드라이버는 데이터 원본에 값을 보냅니다. 경우에 따라 값의 형식을 텍스트로 지정 하 고 문을 데이터 원본에 보내기 전에 SQL 문에 삽입 합니다.
