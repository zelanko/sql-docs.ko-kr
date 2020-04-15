---
title: 매개 변수 값 설정 | 마이크로 소프트 문서
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
ms.openlocfilehash: 923fd57f4308fb72aca2f829ccb9d7b884c12546
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299833"
---
# <a name="setting-parameter-values"></a>매개 변수 값 설정
매개 변수의 값을 설정하려면 응용 프로그램은 매개 변수에 바인딩된 변수의 값을 단순히 설정합니다. 문이 실행되기 전에 설정된 한 이 값을 설정할 때는 중요하지 않습니다. 응용 프로그램은 변수를 바인딩하기 전이나 후에 값을 설정할 수 있으며 원하는 만큼 값을 변경할 수 있습니다. 문이 실행되면 드라이버는 변수의 현재 값을 검색하기만 하면 됩니다. 이 기능은 준비된 명령문이 두 번 이상 실행될 때 특히 유용합니다. 응용 프로그램은 문이 실행될 때마다 변수의 일부 또는 전부에 대해 새 값을 설정합니다. 이 예제에서는 준비된 [실행](../../../odbc/reference/develop-app/prepared-execution-odbc.md)을 참조 하십시오.  
  
 길이/표시기 버퍼가 **SQLBindParameter**호출에 바인딩된 경우 문이 실행되기 전에 다음 값 중 하나로 설정해야 합니다.  
  
-   바인딩된 변수의 데이터의 바이트 길이입니다. 드라이버는 변수가 문자 또는*이진(ValueType이* SQL_C_CHAR 또는 SQL_C_BINARY)인 경우에만 이 길이를 확인합니다.  
  
-   SQL_NTS. 데이터는 null 종료 된 문자열입니다.  
  
-   SQL_NULL_DATA. 데이터 값은 NULL이며 드라이버는 바인딩된 변수의 값을 무시합니다.  
  
-   SQL_DATA_AT_EXEC 또는 SQL_LEN_DATA_AT_EXEC 매크로의 결과입니다. 매개 변수의 값은 **SQLPutData**. 자세한 내용은 [긴 데이터 전송을](../../../odbc/reference/develop-app/sending-long-data.md)참조하세요.  
  
 다음 표에서는 바인딩된 변수의 값과 응용 프로그램이 다양한 매개 변수 값에 대해 설정하는 길이/표시기 버퍼를 보여 주며 있습니다.  
  
|매개 변수<br /><br /> value|매개 변수<br /><br /> (SQL)<br /><br /> 데이터 형식|가변(C)<br /><br /> 데이터 형식|의 값<br /><br /> 바인딩됨<br /><br /> 변수|의 값<br /><br /> 길이/표시기<br /><br /> 버퍼[d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0[a]|SQL_NTS 또는 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0[a]|SQL_NTS 또는 2|  
|오후 1시|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0[b]|--|  
|오후 1시|SQL_TYPE_TIME|SQL_C_CHAR|{t '13:00:00'}\0[a], [c]|SQL_NTS 또는 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0"은 null 종료 문자를 나타냅니다. 널 종료 문자는 길이/표시기 버퍼의 값이 SQL_NTS 경우에만 필요합니다.  
  
 [b] 이 목록의 숫자는 TIME_STRUCT 구조의 필드에 저장된 숫자입니다.  
  
 [c] 문자열은 ODBC 날짜 이스케이프 절을 사용합니다. 자세한 내용은 [날짜, 시간 및 타임스탬프 리터럴을](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)참조하십시오.  
  
 [d] 드라이버는 항상 이 값을 확인하여 SQL_NULL_DATA 같은 특별한 값인지 확인해야 합니다.  
  
 실행 시 매개 변수 값으로 드라이버가 수행하는 일은 드라이버에 따라 다릅니다. 필요한 경우 드라이버는 C 데이터 형식과 바인딩된 변수의 바이트 길이에서 값을 SQL 데이터 형식, 정밀도 및 매개 변수의 배율로 변환합니다. 대부분의 경우 드라이버는 값을 데이터 원본으로 보냅니다. 경우에 따라 값을 텍스트로 서식을 지정하고 데이터 원본에 문을 보내기 전에 SQL 문에 삽입합니다.
