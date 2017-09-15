---
title: "SQL에서 C 데이터 변환 예 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7dd7b514ce4788a035e6f230f3d0a87a94440f2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-data-conversion-examples"></a>SQL에서 C 데이터 변환 예제
다음 표에 표시 된 예제 드라이버 C 데이터를 SQL 데이터를 변환 하는 방법을 보여 줍니다.  
  
|SQL 유형<br /><br /> 식별자(identifier)|SQL data<br /><br /> value|C 형식<br /><br /> 식별자(identifier)|버퍼<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|n/a|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56\0 [a]|n/a|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|무시됨|1234.56|n/a|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|무시됨|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|무시됨|----|22003|  
SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|무시됨|1.2345678|n/a|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|무시됨|1.234567|n/a|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|무시됨|1.|n/a|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31\0 [a]|n/a|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|무시됨|1992,12,31, 0,0,0,0 [b]|n/a|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12\0 [a]|n/a|  
SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1\0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\0" null 종료 바이트를 나타냅니다. 드라이버는 항상 null로 끝냅니다 SQL_C_CHAR 데이터입니다.  
  
 [이 목록에 있는 b]는 숫자는 TIMESTAMP_STRUCT 구조체의 필드에 저장 된 숫자입니다.
