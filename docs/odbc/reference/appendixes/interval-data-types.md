---
title: 간격 데이터 유형 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee4a6e845e0bc0830f514b2e768075dd75bcf6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304969"
---
# <a name="interval-data-types"></a>간격 데이터 형식
간격은 두 날짜와 시간 사이의 차이로 정의됩니다. 간격은 두 가지 방법 중 하나로 표현됩니다. 하나는 연도 및 *일수의* 측면에서 간격을 표현하는 연도 월 간격입니다. 다른 하나는 *일,* 분 및 초 단위로 간격을 표현하는 일 시간 간격입니다. 이 두 가지 유형의 간격은 서로 다르며 월마다 일 수가 달라질 수 있기 때문에 혼합할 수 없습니다.  
  
 간격은 필드 집합으로 구성됩니다. 필드 간에 암시적 순서가 있습니다. 예를 들어 연도간 간격에서 연도가 먼저 오고 그 다음에 월이 옵니다. 마찬가지로, 일-분 간격으로 필드는 순서 일, 시간 및 분입니다. 간격 형식의 첫 번째 필드를 *선행* 필드 또는 *고차* 필드라고 합니다. 마지막 필드를 *후행* 필드라고 합니다.  
  
 모든 간격에서 선행 필드는 [그레고리오 력]의 규칙에 의해 제한되지 않습니다. 예를 들어, 1시간에서 분 간격으로 시간 필드는 평소와 같이 0에서 23(포함)으로 제한되지 않습니다. 선행 필드 다음에 이어지는 후행 필드는 일반 달력의 일반적인 제약 조건을 따릅니다. 자세한 내용은 이 부록의 다음 [부분의 그레고리오력 달력의 제약 조건을](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)참조하십시오.  
  
 13 간격 SQL 데이터 형식과 13 간격 C 데이터 형식이 있습니다. 각 간격 C 데이터 형식은 동일한 구조인 SQL_INTERVAL_STRUCT 사용하여 간격 데이터를 포함합니다. (자세한 내용은 다음 섹션, [C 간격 구조를](../../../odbc/reference/appendixes/c-interval-structure.md)참조하십시오.) SQL 데이터 형식에 대한 자세한 내용은 [SQL 데이터 형식을](../../../odbc/reference/appendixes/sql-data-types.md)참조하십시오. C 데이터 형식에 대한 자세한 내용은 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md)참조하십시오.  
  
|유형 식별자|클래스|설명|  
|---------------------|-----------|-----------------|  
|MONTH|연도 월|두 날짜 사이의 월 수입니다.|  
|YEAR|연도 월|두 날짜 사이의 연도 수입니다.|  
|YEAR_TO_MONTH|연도 월|두 날짜 사이의 연도 및 월 수입니다.|  
|DAY|낮 시간|두 날짜 사이의 일 수입니다.|  
|HOUR|낮 시간|두 날짜/시간 사이의 시간 수입니다.|  
|MINUTE|낮 시간|두 날짜/시간 사이의 분 수입니다.|  
|SECOND|낮 시간|두 날짜/시간 사이의 초 수입니다.|  
|DAY_TO_HOUR|낮 시간|두 날짜 /시간 사이의 일 / 시간 수입니다.|  
|DAY_TO_MINUTE|낮 시간|날짜/시간 사이의 일/시간/분 수입니다.|  
|DAY_TO_SECOND|낮 시간|날짜/시간 사이의 일/시간/분/초 수입니다.|  
|HOUR_TO_MINUTE|낮 시간|두 날짜/시간 사이의 시간/분 수입니다.|  
|HOUR_TO_SECOND|낮 시간|두 날짜/시간 사이의 시간/분/초 수입니다.|  
|MINUTE_TO_SECOND|낮 시간|두 날짜/시간 사이의 분/초 수입니다.|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [간격 데이터 형식 전체 자릿수 ](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [간격 리터럴](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
