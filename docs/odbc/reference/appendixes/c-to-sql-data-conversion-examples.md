---
title: C에서 SQL 데이터 변환 예제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e475abb699c7fa7240ca6eb39b1b32f1730d33c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125742"
---
# <a name="c-to-sql-data-conversion-examples"></a>C에서 SQL로 데이터 변환 예제
다음 예에서는 드라이버가 C 데이터를 SQL 데이터로 변환 하는 방법을 보여 줍니다.  
  
|C 형식 식별자|C 데이터 값|SQL 유형<br /><br /> identifier|열<br /><br /> length|SQL 데이터<br /><br /> 값|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|해당 없음|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde...z|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|8 [b]|1234.56|해당 없음|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56 \ 0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|해당 없음|1234.56|해당 없음|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|해당 없음|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|해당 없음|----|22003|  
|SQL_C_TYPE_DATE|1992 년 12 월 31 일 [c]|SQL_CHAR|10|1992-12-31|해당 없음|  
|SQL_C_TYPE_DATE|1992 년 12 월 31 일 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992 년 12 월 31 일 [c]|SQL_TIMESTAMP|해당 없음|1992-12-31 00:00:00.0|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|1992, 12, 31, 23, 45, 55, 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|해당 없음|  
|SQL_C_TYPE_TIMESTAMP|1992, 12, 31, 23, 45, 55, 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992, 12, 31, 23, 45, 55, 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\ 0"은 null 종료 바이트를 나타냅니다. Null 종료 바이트는 데이터 길이가 SQL_NTS 경우에만 필요 합니다.  
  
 [b] 숫자에 대 한 바이트 외에 부호에 1 바이트가 필요 하 고 소수점에 다른 바이트가 필요 합니다.  
  
 [c]이 목록에 있는 숫자는 SQL_DATE_STRUCT 구조체의 필드에 저장 된 숫자입니다.  
  
 [d]이 목록에 있는 숫자는 SQL_TIMESTAMP_STRUCT 구조체의 필드에 저장 된 숫자입니다.
