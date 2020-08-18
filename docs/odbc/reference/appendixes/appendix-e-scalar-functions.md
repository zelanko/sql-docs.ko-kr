---
description: '부록 E: 스칼라 함수'
title: '부록 E: 스칼라 함수 | Microsoft Docs'
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
ms.openlocfilehash: 4a814de22df4a97e3c3b3abd0ddc30266fe02a30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411439"
---
# <a name="appendix-e-scalar-functions"></a>부록 E: 스칼라 함수
ODBC는 다음과 같은 유형의 스칼라 함수를 지정 하며,이 부록의 해당 섹션에서 제공 하는 각 함수 형식에 대 한 자세한 정보를 제공 합니다. 함수 설명에는 관련 된 구문이 포함 되어 있습니다.  
  
 이 부록에는 다음 항목이 포함 되어 있습니다.  
  
-   [문자열 함수](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [숫자 함수](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [시간, 날짜 및 간격 함수](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [시스템 함수](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [명시적 데이터 형식 변환 함수](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 함수](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC에서는 스칼라 함수에서 반환 값에 대 한 데이터 형식을 지정 하지 않습니다. 함수는 일반적으로 데이터 소스와 관련 되어 있기 때문입니다. 응용 프로그램은 가능 하면 항상 CONVERT 스칼라 함수를 사용 하 여 데이터 형식 변환을 강제로 수행 해야 합니다.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 및 SQL-92 스칼라 함수  
 이 부록의 표에는 SQL-92에 맞게 ODBC 3.0에 추가 된 함수가 포함 되어 있습니다. ODBC에 정의 된 것 처럼 특정 형식의 스칼라 함수에 대해 추가 된 이러한 함수는 각 섹션에 나와 있습니다.  
  
 ODBC 및 SQL-92은 스칼라 함수를 다르게 분류 합니다. ODBC에서 스칼라 함수를 인수 형식으로 분류 합니다. SQL-92는 반환 값으로 분류 합니다. 예를 들어 extract 함수는 c #에서 timedate.cpl 함수로 분류 됩니다. 추출 필드 인수는 datetime 키워드이 고 extract 원본 인수는 datetime 또는 interval 식 이기 때문입니다. 반면에 SQL-92는 숫자 스칼라 함수로 EXTRACT를 분류 합니다. 반환 값은 숫자 이기 때문입니다.  
  
 응용 프로그램은 **SQLGetInfo**를 호출 하 여 드라이버가 지 원하는 스칼라 함수를 확인할 수 있습니다. 정보 유형은 ODBC와 스칼라 함수의 SQL-92 분류에 모두 포함 됩니다. 이러한 분류는 서로 다르기 때문에 일부 스칼라 함수에 대 한 지원은 ODBC 및 SQL-92에 해당 하지 않는 정보 형식에 표시 될 수 있습니다. 예를 들어 ODBC에서 추출에 대 한 지원은 SQL_TIMEDATE_FUNCTIONS 정보 형식으로 표시 됩니다. 반면에 SQL-92의 추출에 대 한 지원은 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 정보 형식으로 표시 됩니다.
