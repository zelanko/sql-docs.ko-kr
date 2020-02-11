---
title: SQL 규칙 수준 (Oracle 용 ODBC 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 241f4f3da12f63c15d917a0e47cb13ad0e96e6e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063351"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 적합성 수준(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 용 ODBC 드라이버는 최소 SQL 문법 및 핵심 SQL 문법을 지원 하 고 SQL에 대 한 다음 ODBC 확장도 지원 합니다.  
  
-   날짜, 시간 및 타임 스탬프 데이터  
  
-   왼쪽 및 오른쪽 우선 외부 조인  
  
-   숫자 함수:  
  
    |||||  
    |-|-|-|-|  
    |Abs|로그|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|sign||  
    |Exp|Pi|sin||  
    |Floor|거듭제곱|sqrt||  
  
-   날짜 함수:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|now|year|  
    |Dayofmonth|Month|quarter||  
  
-   문자열 함수:  
  
    |||||  
    |-|-|-|-|  
    |ASCII|Left|오른쪽|ucase|  
    |Char|길이|rtrim||  
    |Concat|Ltrim|soundex||  
    |Lcase|Replace|substring||  
  
-   형식 변환 함수:  
  
    ||  
    |-|  
    |변환|  
  
-   시스템 함수:  
  
    ||  
    |-|  
    |Ifnull|  
    |사용자|
