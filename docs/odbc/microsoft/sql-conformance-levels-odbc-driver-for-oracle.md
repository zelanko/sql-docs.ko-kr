---
title: SQL 적합성 수준 (Oracle 용 ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0bf63b831dace7678f5d3fdf952a9d6d5f60aa6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313385"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 적합성 수준(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 ODBC 드라이버는 최소 SQL 문법 및 핵심 SQL 문법을 지원 및 SQL의 다음 ODBC 확장도 지원:  
  
-   날짜, 시간 및 타임 스탬프 데이터  
  
-   왼쪽 및 오른쪽 우선 외부 조인  
  
-   숫자 함수:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |ceiling|Log10|second|truncate|  
    |Cos|Mod|sign||  
    |Exp|Pi|sin||  
    |floor|Power|sqrt||  
  
-   날짜 함수:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|이제|year|  
    |Dayofmonth|Month|분기||  
  
-   문자열 함수:  
  
    |||||  
    |-|-|-|-|  
    |Ascii|왼쪽|오른쪽|Ucase|  
    |Char|길이|rtrim||  
    |Concat|Ltrim|Soundex||  
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
