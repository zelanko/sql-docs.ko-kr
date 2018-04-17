---
title: '부록 e: 스칼라 함수 | Microsoft Docs'
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
ms.topic: article
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ee9e2ab75f22ae3090d87d5c232f88423df9360
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="appendix-e-scalar-functions"></a>부록 e: 스칼라 함수
ODBC이 부록의이 내용의 해당 섹션에서 제공 되는 이러한 함수 형식의 각각에 대 한 세부 정보가 포함 된 다음과 같은 유형의 스칼라 함수를 지정 합니다. 함수 설명에 관련 된 구문을 포함합니다.  
  
 이 부록의 내용에는 다음 항목이 포함 되어 있습니다.  
  
-   [문자열 함수](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [숫자 함수](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [시간, 날짜 및 간격 함수](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [시스템 함수](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 함수](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 함수가 데이터 원본에 따른 특정 경우가 많기 때문에 ODBC 스칼라 함수에서 반환 값에 대 한 데이터 형식을 필요 하지 않습니다. 응용 프로그램 데이터 형식 변환을 강제 실행 가능 하면 CONVERT 스칼라 함수를 사용 해야 합니다.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 및 SQL 92 스칼라 함수  
 이 부록의 내용 테이블에는 s Q l-92에 맞게 ODBC 3.0에서 추가 된 기능이 포함 됩니다. ODBC에 정의 된 특정 유형의 스칼라 함수에 대 한 추가 된 이러한 함수는 각 섹션에 표시 됩니다.  
  
 ODBC 및 SQL 92의 스칼라 함수를 다르게 분류합니다. ODBC 스칼라 함수 인수; 유형별로 분류 반환 값을 분류 하는 SQL 92 합니다. 예를 들어 함수 추출으로 분류 됩니다 timedate 함수 ODBC에 필드 추출 인수 datetime 키워드 며 추출 원본 인수는 날짜/시간 또는 간격 식 때문입니다. SQL 92 반면에 추출으로 분류 스칼라 함수를 숫자 반환 값은 숫자입니다.  
  
 응용 프로그램에 스칼라 함수를 호출 하 여 드라이버가 지 원하는 결정할 수 **SQLGetInfo**합니다. 정보 유형이 ODBC 및 SQL 92 분류 스칼라 함수에 대 한 포함 됩니다. 이러한 분류가 다르기 때문에 일부 스칼라 함수에 대 한 지원 ODBC 및 s Q l 92와 일치 하지 않는 정보 유형이에 표시 될 수 있습니다. 예를 들어 ODBC에서 추출에 대 한 지원은 SQL_TIMEDATE_FUNCTIONS 정보 유형을;로 표시 됩니다. 반면에 SQL 92에서 추출에 대 한 지원 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 정보 유형으로 표시 됩니다.
