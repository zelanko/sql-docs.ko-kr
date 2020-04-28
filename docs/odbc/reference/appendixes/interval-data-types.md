---
title: Interval 데이터 형식 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304969"
---
# <a name="interval-data-types"></a>간격 데이터 형식
간격은 두 날짜와 시간 사이의 차이로 정의 됩니다. 간격은 두 가지 방법 중 하나로 표현 됩니다. 하나는 연도와 정수 (월)를 기준으로 간격을 나타내는 *연도-월* 간격입니다. 나머지는 일, 분, 초를 기준으로 간격을 나타내는 *일 시간* 간격입니다. 이러한 두 가지 간격 유형은 고유 하며, 월은 다양 한 일 수를 가질 수 있기 때문에 혼합할 수 없습니다.  
  
 간격은 필드 집합으로 구성 됩니다. 필드 간에는 암시적인 순서가 지정 되어 있습니다. 예를 들어 연도별 간격에서 연도가 먼저 오고 그 뒤에 해당 월이 나옵니다. 마찬가지로, 일 대 분 간격으로 필드는 일, 시간 및 분 순서로 정렬 됩니다. 간격 유형의 첫 번째 필드를 *선행* 필드 또는 *상위* 필드 라고 합니다. 마지막 필드를 *후행* 필드 라고 합니다.  
  
 모든 간격에서 선행 필드는 양력 규칙에 따라 제한 되지 않습니다. 예를 들어 1 시간 간격으로 시간 필드는 일반적으로 0과 23 사이 (포함)로 제한 되지 않습니다. 선행 필드 뒤에 오는 후행 필드는 일반 달력의 일반적인 제약 조건을 따릅니다. 자세한 내용은이 부록의 뒷부분에 나오는 [양력의 제약 조건](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)을 참조 하세요.  
  
 13 개의 간격 SQL 데이터 형식 및 13 개의 간격 C 데이터 형식이 있습니다. 각 간격 C 데이터 형식은 동일한 구조 (SQL_INTERVAL_STRUCT)를 사용 하 여 간격 데이터를 포함 합니다. 자세한 내용은 다음 섹션인 [C Interval 구조](../../../odbc/reference/appendixes/c-interval-structure.md)를 참조 하세요. SQL 데이터 형식에 대 한 자세한 내용은 [Sql 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)을 참조 하세요. C 데이터 형식에 대 한 자세한 내용은 [c 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)을 참조 하세요.  
  
|유형 식별자|인스턴스|설명|  
|---------------------|-----------|-----------------|  
|MONTH|년-월|두 날짜 사이의 개월 수입니다.|  
|YEAR|년-월|두 날짜 사이의 연도 수입니다.|  
|YEAR_TO_MONTH|년-월|두 날짜 사이의 연도 및 월 수입니다.|  
|DAY|일-시간|두 날짜 사이의 일 수입니다.|  
|HOUR|일-시간|두 날짜/시간 사이의 시간 수입니다.|  
|MINUTE|일-시간|두 날짜/시간 사이의 시간 (분)입니다.|  
|SECOND|일-시간|두 날짜/시간 사이의 시간 (초)입니다.|  
|DAY_TO_HOUR|일-시간|두 날짜/시간 사이의 일/시간 수입니다.|  
|DAY_TO_MINUTE|일-시간|두 날짜/시간 사이의 일/시간/분 수입니다.|  
|DAY_TO_SECOND|일-시간|두 날짜/시간 사이의 일/시간/분/초 수입니다.|  
|HOUR_TO_MINUTE|일-시간|두 날짜/시간 사이의 시간/분 수입니다.|  
|HOUR_TO_SECOND|일-시간|두 날짜/시간 사이의 시간/분/초 수입니다.|  
|MINUTE_TO_SECOND|일-시간|두 날짜/시간 사이의 시간 (분)입니다.|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [C 간격 구조](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [간격 데이터 형식 전체 자릿수 ](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [간격 데이터 형식 길이](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [간격 리터럴](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
