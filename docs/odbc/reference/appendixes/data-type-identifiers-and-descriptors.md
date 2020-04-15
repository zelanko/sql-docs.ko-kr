---
title: 데이터 유형 식별자 및 설명자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 02/02/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f65bc86213f99112daf17c67a4ca522490d32149
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284486"
---
# <a name="data-type-identifiers-and-descriptors"></a>데이터 형식 식별자 및 설명자
이 부록의 앞에 나와 있는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 및 C 데이터 [형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션에 나열된 데이터 형식은 "간결한" 데이터 형식입니다. 식별자와 데이터 형식 간에 일대일 대응이 있습니다. 그러나 설명자가 모든 경우에 단일 값을 사용하여 데이터 형식을 식별하는 것은 아닙니다. 경우에 따라 "자세한" 데이터 형식 및 형식 하위 코드를 사용합니다. datetime 및 interval 데이터 형식을 제외한 모든 데이터 형식의 경우 자세한 형식 식별자는 간결한 형식 식별자와 동일하며 SQL_DESC_DATETIME_INTERVAL_CODE 값은 0과 같습니다. 그러나 datetime 및 간격 데이터 형식의 경우 자세한 형식(SQL_DATETIME 또는 SQL_INTERVAL)이 SQL_DESC_TYPE 저장되고 간결한 형식이 SQL_DESC_CONCISE_TYPE 저장되고 각 간결한 형식에 대한 하위 코드가 SQL_DESC_DATETIME_INTERVAL_CODE 저장됩니다. 이러한 필드 중 하나를 설정하면 다른 필드에 영향을 줍니다. 이러한 필드에 대한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명을 참조하십시오.  
  
 일부 데이터 형식에 대해 SQL_DESC_TYPE 또는 SQL_DESC_CONCISE_TYPE 필드가 설정되면 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드는 데이터 형식에 해당하는 기본값으로 자동으로 설정됩니다. 자세한 내용은 [SQLSetDescField의](../../../odbc/reference/syntax/sqlsetdescfield-function.md)SQL_DESC_TYPE 필드에 대한 설명을 참조하십시오. 설정된 기본값 중 어느 라도 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField**에 대한 호출을 통해 설명자 필드를 명시적으로 설정해야 합니다.  
  
 다음 표에서는 간결한 형식 식별자, 자세한 형식 식별자 및 각 datetime 및 interval SQL 및 C 형식 식별자에 대한 하위 코드를 입력합니다. 이 표에서 와 같이 datetime 및 간격 데이터 형식의 경우 SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드에는 SQL 데이터 형식(구현 설명자) 및 C 데이터 형식(응용 프로그램 설명자)에 대해 동일한 매니페스트 상수가 있습니다.  
  
|간결한 SQL 유형|간결한 C형|자세한 유형|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
|SQL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
