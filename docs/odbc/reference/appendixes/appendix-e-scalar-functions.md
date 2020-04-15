---
title: '부록 E: 스칼라 기능 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea354a7f882bd1a75c5f16fb19350d69ca11d375
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292493"
---
# <a name="appendix-e-scalar-functions"></a>부록 E: 스칼라 함수
ODBC는 이 부록의 해당 섹션에 제공되는 각 함수 유형에 대한 자세한 정보와 함께 다음과 같은 스칼라 함수 유형을 지정합니다. 함수 설명에는 연결된 구문이 포함됩니다.  
  
 이 부록에는 다음 항목이 포함되어 있습니다.  
  
-   [문자열 함수](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [숫자 함수](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [시간, 날짜 및 간격 함수](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [시스템 기능](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 함수](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC는 함수가 데이터 원본에 따라 다르기 때문에 스칼라 함수에서 반환 값에 대한 데이터 형식을 요구하지 않습니다. 응용 프로그램은 데이터 형식 변환을 강제로 적용하기 위해 가능하면 CONVERT 스칼라 함수를 사용해야 합니다.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 및 SQL-92 스칼라 기능  
 이 부록의 테이블에는 SQL-92에 맞게 ODBC 3.0에 추가된 함수가 포함되어 있습니다. ODBC에 정의된 대로 특정 유형의 스칼라 함수에 대해 추가된 함수는 각 섹션에 표시됩니다.  
  
 ODBC 및 SQL-92는 스칼라 함수를 다르게 분류합니다. ODBC는 스칼라 함수를 인수 유형으로 분류합니다. SQL-92는 반환 값으로 분류합니다. 예를 들어 EXTRACT 함수는 추출 필드 인수가 datetime 키워드이고 추출 소스 인수는 datetime 또는 간격 식이기 때문에 ODBC에 의해 시간 날짜 함수로 분류됩니다. 반면 SQL-92는 반환 값이 숫자이기 때문에 EXTRACT를 숫자 스칼라 함수로 분류합니다.  
  
 응용 프로그램은 **SQLGetInfo**를 호출하여 드라이버가 지원하는 스칼라 함수를 결정할 수 있습니다. 정보 유형은 ODBC 및 SQL-92 스칼라 함수 분류에 모두 포함됩니다. 이러한 분류는 다르기 때문에 일부 스칼라 함수에 대한 지원은 ODBC 및 SQL-92에 해당하지 않는 정보 유형으로 표시될 수 있습니다. 예를 들어, ODBC에서 추출에 대한 지원은 SQL_TIMEDATE_FUNCTIONS 정보 유형으로 표시됩니다. SQL-92에서 추출에 대 한 지원, 다른 한편으로는, SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 정보 유형으로 표시 됩니다.
