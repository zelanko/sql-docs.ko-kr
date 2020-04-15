---
title: C에서 SQL 데이터 변환 예제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e21654f183946675c63cee10a3c08754e1508f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291993"
---
# <a name="c-to-sql-data-conversion-examples"></a>C에서 SQL로 데이터 변환 예제
다음 예제에서는 드라이버가 C 데이터를 SQL 데이터로 변환하는 방법을 보여 줍니다.  
  
|C 유형 식별자|C 데이터 값|SQL 유형<br /><br /> identifier|열<br /><br /> length|SQL data<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|6|abcdef|해당 없음|  
|SQL_C_CHAR|abcdef\0[a]|SQL_CHAR|5|Abcde|22001|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|8[b]|1234.56|해당 없음|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0[a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|해당 없음|1234.56|해당 없음|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|해당 없음|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|해당 없음|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|10|1992-12-31|해당 없음|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_TIMESTAMP|해당 없음|1992-12-31 00:00:00.0|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0"은 null 종료 바이트를 나타냅니다. 널 종료 바이트는 데이터의 길이가 SQL_NTS 경우에만 필요합니다.  
  
 [b] 숫자의 바이트 외에도 기호에 대해 1바이트가 필요하고 소수점에 대해 다른 바이트가 필요합니다.  
  
 [c] 이 목록의 숫자는 SQL_DATE_STRUCT 구조의 필드에 저장된 숫자입니다.  
  
 [d] 이 목록의 숫자는 SQL_TIMESTAMP_STRUCT 구조의 필드에 저장된 숫자입니다.
