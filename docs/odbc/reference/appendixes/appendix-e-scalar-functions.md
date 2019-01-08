---
title: '부록 e: 스칼라 함수 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71c80efdb2f4a87537d472ee4b6dc6bdc65af70f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540513"
---
# <a name="appendix-e-scalar-functions"></a>부록 e: 스칼라 함수
ODBC이이 부록의 해당 섹션에 제공 된 이러한 함수 형식을 각각에 대 한 자세한 정보를 사용 하 여 다음과 같은 유형의 스칼라 함수를 지정 합니다. 함수 설명에는 연결 된 구문 포함 됩니다.  
  
 이 부록에는 다음 항목에 있습니다.  
  
-   [문자열 함수](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [숫자 함수](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [시간, 날짜 및 간격 함수](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [시스템 함수](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 함수](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 함수는 데이터 소스 관련 경우가 많기 때문에 ODBC 스칼라 함수에서 반환 값에 대 한 데이터 형식을 위임 하지 않습니다. 응용 프로그램 데이터 형식 변환에 적용할 가능한 CONVERT 스칼라 함수를 사용 해야 합니다.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 및 SQL-92 스칼라 함수  
 이 부록의 표에서 SQL-92에 맞게 ODBC 3.0에서 추가 된 함수를 포함 합니다. ODBC에 정의 된 대로 특정 유형의 스칼라 함수에 대 한 추가 이러한 함수는 각 섹션에 표시 됩니다.  
  
 ODBC 및 SQL-92 다르게 해당 스칼라 함수를 분류 합니다. ODBC 스칼라 함수 인수 형식으로 분류 SQL-92 반환 값으로 분류합니다. 예를 들어, EXTRACT 함수 timedate 함수로 의해 분류 ODBC 필드 추출 인수는 datetime 키워드 이므로 추출 원본 인수는 datetime 또는 간격 식입니다. SQL-92와 다른 한편으로 추출으로 분류 숫자 스칼라 함수인 경우 반환 값은 숫자입니다.  
  
 응용 프로그램에서 드라이버를 호출 하 여 지원 되는 스칼라 함수를 확인할 수 있습니다 **SQLGetInfo**합니다. 정보 유형 ODBC 및 SQL-92 분류 스칼라 함수에 대 한 포함 됩니다. 이러한 분류 다른 이기 때문에 일부 스칼라 함수에 대 한 지원 정보 유형 해당 하지 않는 ODBC 및 SQL-92에에서 표시 될 수 있습니다. 예를 들어 ODBC에서 추출에 대 한 지원을 나타난 SQL_TIMEDATE_FUNCTIONS 정보 형식 반면에 SQL-92에 추출에 대 한 지원은 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 정보 형식으로 표시 됩니다.
