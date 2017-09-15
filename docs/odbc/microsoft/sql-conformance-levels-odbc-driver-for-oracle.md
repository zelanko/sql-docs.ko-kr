---
title: "SQL 받는 규칙 수준 (ODBC Driver for Oracle) | Microsoft Docs"
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ada0aaa75fe63313395b6e727c3bc86bf639704e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 받는 규칙 수준 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 ODBC Driver for Oracle 최소 SQL 문법 및 핵심 SQL 문법을 지원 하 고도 다음과 같은 ODBC 확장 SQL 지원 합니다.  
  
-   Date, time 및 timestamp 데이터  
  
-   왼쪽 및 오른쪽 우선 외부 조인  
  
-   숫자 함수:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |최대값|Log10|second|truncate|  
    |Cos|Mod|로그인||  
    |Exp|pi|sin||  
    |floor|Power|sqrt||  
  
-   날짜 함수:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|이제|year|  
    |dayofmonth|Month|분기||  
  
-   문자열 함수:  
  
    |||||  
    |-|-|-|-|  
    |ascii|왼쪽|오른쪽|ucase|  
    |Char|길이|rtrim||  
    |Concat|Ltrim|soundex||  
    |Lcase|바꾸기|substring||  
  
-   형식 변환 함수:  
  
    ||  
    |-|  
    |변환|  
  
-   시스템 함수:  
  
    ||  
    |-|  
    |Ifnull|  
    |사용자|
