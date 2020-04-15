---
title: SQL 적합성 수준(오라클용 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e283bbc13f0d0dda055b047b027f7b9816502df5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300683"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 적합성 수준(Oracle용 ODBC 드라이버)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클용 ODBC 드라이버는 최소 SQL 문법 및 코어 SQL 문법을 지원하며 SQL에 대한 다음 ODBC 확장을 지원합니다.  
  
-   날짜, 시간 및 타임스탬프 데이터  
  
-   왼쪽 및 오른쪽 외부 조인  
  
-   숫자 함수:  
  
    |||||  
    |-|-|-|-|  
    |Abs|로그|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|sign||  
    |Exp|Pi|sin||  
    |Floor|Power|sqrt||  
  
-   날짜 함수:  
  
    |||||  
    |-|-|-|-|  
    |커데이트 (주)|Dayofweek|Monthname|second|  
    |커타임|Dayofyear|minute|week|  
    |데이나메|Hour|now|year|  
    |데이오브월|월|quarter||  
  
-   문자열 함수:  
  
    |||||  
    |-|-|-|-|  
    |ASCII|Left|오른쪽|유케이스 (미국)의|  
    |Char|길이|Rtrim||  
    |Concat|Ltrim|Soundex||  
    |Lcase|Replace|substring||  
  
-   유형 변환 기능:  
  
    ||  
    |-|  
    |변환|  
  
-   시스템 기능:  
  
    ||  
    |-|  
    |이프널 (것)이|  
    |사용자|
