---
title: "Interval 데이터 형식을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6a1b1a7320feef3cff6d63ce5ca6a22be6329169
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="interval-data-types"></a>Interval 데이터 형식
간격은 두 날짜 및 시간 간의 차이로 정의 됩니다. 간격으로 두 가지 방법 중 하나로 표현 됩니다. 하나는 *년-월* 간격 연도 및 월의 정수가 측면에서 표현 하는 간격입니다. 다른 하나는 한 *하루 시간* 간격 (일), 분 및 초 측면에서 표현 하는 간격입니다. 이러한 두 가지 유형의 간격으로 고유 하 고 월 일 수가 다양 한 여러 있을 수 있으므로 혼합할 수 없습니다.  
  
 시간 간격이 필드 집합으로 구성 됩니다. 필드는 암시적 순서는. 예를 들어 연도-월 간격으로 연도 되어 월별로 합니다. 마찬가지로, 하루 분 간격 필드 순서 일, 시간 및 분에 있습니다. 간격 유형의 첫 번째 필드 라고는 *선행* 필드 또는 *상위* 필드입니다. 마지막 필드 라고는 *후행* 필드입니다.  
  
 모든 간격에서 선행 필드 규칙 일반 달력에 제한 되지 않습니다. 예를 들어 시간-분 간격의 시간 필드 제한이 이므로 일반적으로 0에서 23 (포함) 사이 여야 합니다. 선행 필드 이후의 후행 필드에는 일반 달력의 일반적인 제약 조건을 따릅니다. 자세한 내용은 참조 [일반 달력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)이 부록의 뒷부분에 나오는 합니다.  
  
 13 간격 SQL 데이터 형식 및 13 간격 C 데이터 형식. 각 C interval 데이터 형식을 SQL_INTERVAL_STRUCT, 동일한 구조를를 사용 하 여 간격 데이터를 포함 시키십시오. (자세한 내용은 다음 섹션을 참조 하십시오. [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md).) SQL 데이터 형식에 대 한 자세한 내용은 참조 하십시오. [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)C 데이터 형식에 대 한 자세한 내용은 참조는; [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md)합니다.  
  
|유형 식별자|클래스|Description|  
|---------------------|-----------|-----------------|  
|MONTH|년-월|두 날짜 사이의 개월 수입니다.|  
|YEAR|년-월|두 날짜 사이의 연도 수입니다.|  
|YEAR_TO_MONTH|년-월|년 및 두 날짜 사이의 개월 수입니다.|  
|DAY|주간 시간|두 날짜 사이의 일 수입니다.|  
|HOUR|주간 시간|두 시간의 날짜/시간입니다.|  
|MINUTE|주간 시간|두 시간 (분) 날짜/시간입니다.|  
|SECOND|주간 시간|두 시간 (초) 날짜/시간입니다.|  
|DAY_TO_HOUR|주간 시간|두 날짜/시간 날짜/시간입니다.|  
|DAY_TO_MINUTE|주간 시간|일/시간/분 두 수가 날짜/시간입니다.|  
|DAY_TO_SECOND|주간 시간|일/시간/분/초 두 수가 날짜/시간입니다.|  
|HOUR_TO_MINUTE|주간 시간|두 시간/분 수 날짜/시간입니다.|  
|HOUR_TO_SECOND|주간 시간|두 시간/분/초 수 날짜/시간입니다.|  
|MINUTE_TO_SECOND|주간 시간|두 분/초 수 날짜/시간입니다.|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [간격 데이터 형식 전체 자릿수 ](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [간격 리터럴](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
