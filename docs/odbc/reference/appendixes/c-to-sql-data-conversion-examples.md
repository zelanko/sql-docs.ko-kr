---
title: SQL 데이터 변환 예제 C | Microsoft Docs
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
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f51dd54f01bacd5c36da84c71061fd71f072bc17
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-data-conversion-examples"></a>C to SQL 데이터 변환 예제
다음 예에서는 드라이버 SQL 데이터 C 데이터를 변환 하는 방법을 보여 줍니다.  
  
|C 형식 식별자|C 데이터 값|SQL 유형<br /><br /> 식별자(identifier)|열<br /><br /> length|SQL data<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|n/a|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8 [b]|1234.56|n/a|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/a|1234.56|n/a|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/a|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/a|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c + +]|SQL_CHAR|10|1992-12-31|n/a|  
|SQL_C_TYPE_DATE|1992,12,31 [c + +]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c + +]|SQL_TIMESTAMP|n/a|1992-12-31 00:00:00.0|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/a|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0" null 종료 바이트를 나타냅니다. Null 종료 바이트는 데이터의 길이 SQL_NTS 하는 경우에 필요 합니다.  
  
 [b] 외에 숫자에 대 한 바이트를 1 바이트는 기호에 대 한 필수 이며 다른 바이트는 소수점에 필요 합니다.  
  
 [이 목록에 있는 c]는 숫자는 SQL_DATE_STRUCT 구조체의 필드에 저장 된 숫자입니다.  
  
 [이 목록에 있는 d]에서 숫자는 SQL_TIMESTAMP_STRUCT 구조체의 필드에 저장 된 숫자입니다.
