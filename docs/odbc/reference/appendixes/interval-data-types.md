---
title: 간격 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 930a848ea01d128cb248c7929408ce7510937ad9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188895"
---
# <a name="interval-data-types"></a>간격 데이터 형식
간격 두 날짜 및 시간 간의 차이 따라 정의 됩니다. 간격으로 두 가지 방법 중 하나로 표현 됩니다. 하나는 *연-월* 간격 연도 및 월의 정수가 측면에서 표현 하는 간격입니다. 다른 하나는 한 *날짜-시간* 간격 (일), 분 및 초를 기준으로 표현 하는 간격입니다. 이러한 두 가지 유형의 간격 명확 하 고 월 일의 다양 한 숫자를 포함할 수 있으므로 혼합할 수 없습니다.  
  
 간격 필드의 집합으로 구성 됩니다. 필드 간에 암시적 순서가지 않습니다. 예를 들어 연도-월 간격에서 연도 먼저, 달 뒤에 됩니다. 마찬가지로, 고 일 분 간격으로 필드는 주문 날짜, 시간 및 분입니다. 간격 유형의 첫 번째 필드 라고 합니다 *선행* 필드와 *상위* 필드. 마지막 필드 라고 합니다 *후행* 필드입니다.  
  
 모든 간격에서 선행 필드는 일반 달력의 규칙에 의해 제한 되지 않습니다. 예를 들어, 한 시간-분 간격의 시간 필드는 일반적으로 0에서 23 (포함) 사이 여야 제한 되지 않습니다. 선행 필드 이후의 후행 필드에는 일반 달력의 일반적인 제약 조건을 따릅니다. 자세한 내용은 [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)이 부록의 뒷부분에 나오는.  
  
 13 간격 SQL 데이터 형식 및 13 간격 C 데이터 형식이 있습니다. 각 C는 interval 데이터 형식을 데이터 간격을 포함 하도록 SQL_INTERVAL_STRUCT, 동일한 구조를 사용 합니다. (자세한 내용은 다음 섹션을 참조 하세요 [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md).) SQL 데이터 형식에 대 한 자세한 내용은 참조 하세요. [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md); C 데이터 형식에 대 한 자세한 내용은 참조 하십시오 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)합니다.  
  
|유형 식별자|클래스|Description|  
|---------------------|-----------|-----------------|  
|MONTH|년-월|두 날짜 사이의 개월 수입니다.|  
|YEAR|년-월|두 날짜 사이의 연도 수입니다.|  
|YEAR_TO_MONTH|년-월|년 및 두 날짜 사이의 개월 수입니다.|  
|DAY|날짜-시간|두 날짜 사이의 일 수입니다.|  
|HOUR|날짜-시간|두 시간의 날짜/시간입니다.|  
|MINUTE|날짜-시간|날짜/시간 간 시간 (분) 수입니다.|  
|SECOND|날짜-시간|날짜/시간 간 시간 (초) 수입니다.|  
|DAY_TO_HOUR|날짜-시간|두 날짜/시간의 날짜/시간입니다.|  
|DAY_TO_MINUTE|날짜-시간|일/시간/분 두 날짜/시간입니다.|  
|DAY_TO_SECOND|날짜-시간|일/시간/분/시간 (초) 두 날짜/시간입니다.|  
|HOUR_TO_MINUTE|날짜-시간|시간/시간 (분) 두 날짜/시간입니다.|  
|HOUR_TO_SECOND|날짜-시간|시간/분/시간 (초) 두 날짜/시간입니다.|  
|MINUTE_TO_SECOND|날짜-시간|분/시간 (초) 두 날짜/시간입니다.|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [간격 데이터 형식 전체 자릿수 ](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [간격 리터럴](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
