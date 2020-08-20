---
description: 데이터 형식 식별자 및 설명자
title: 데이터 형식 식별자 및 설명자 | Microsoft Docs
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
ms.openlocfilehash: dce52118099ff4be572231e7f44f28a4cfca5ea7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466223"
---
# <a name="data-type-identifiers-and-descriptors"></a>데이터 형식 식별자 및 설명자
이 부록 앞부분의 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 및 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션에 나열 된 데이터 형식은 "간결한" 데이터 형식입니다. 각 식별자는 단일 데이터 형식을 참조 합니다. 식별자와 데이터 형식이 일대일로 대응 됩니다. 그러나 설명자는 모든 경우에 단일 값을 사용 하 여 데이터 형식을 식별 합니다. 일부 경우에는 "verbose" 데이터 형식 및 형식 하위 코드를 사용 합니다. Datetime 및 interval 데이터 형식을 제외한 모든 데이터 형식의 경우 자세한 형식 식별자는 간결한 형식 식별자와 같으며 SQL_DESC_DATETIME_INTERVAL_CODE의 값은 0과 같습니다. 그러나 datetime 및 interval 데이터 형식의 경우 자세한 형식 (SQL_DATETIME 또는 SQL_INTERVAL)이 SQL_DESC_TYPE에 저장 되 고 간결한 형식이 SQL_DESC_CONCISE_TYPE에 저장 되며 각 간결한 형식의 하위 코드가 SQL_DESC_DATETIME_INTERVAL_CODE에 저장 됩니다. 이러한 필드 중 하나를 설정 하면 다른 필드에 영향을 줍니다. 이러한 필드에 대 한 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명을 참조 하세요.  
  
 일부 데이터 형식에 대해 SQL_DESC_TYPE 또는 SQL_DESC_CONCISE_TYPE 필드를 설정 하면 데이터 형식에 적용 가능한 대로 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드가 기본값으로 자동 설정 됩니다. 자세한 내용은 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)의 SQL_DESC_TYPE 필드에 대 한 설명을 참조 하세요. 설정 된 기본값이 적절 하지 않은 경우 응용 프로그램은 **SQLSetDescField**를 호출 하 여 설명자 필드를 명시적으로 설정 해야 합니다.  
  
 다음 표에서는 각 datetime 및 interval SQL 및 C 형식 식별자에 대 한 간결한 형식 식별자, 자세한 형식 식별자 및 형식 하위 코드를 보여 줍니다. 이 표에 나와 있는 것 처럼 datetime 및 interval 데이터 형식의 경우 SQL_DESC_TYPE 및 SQL_DESC_DATETIME_INTERVAL_CODE 필드는 SQL 데이터 형식 (구현 설명자의 경우) 및 C 데이터 형식 (응용 프로그램 설명자) 모두에 대해 동일한 매니페스트 상수를 가집니다.  
  
|간결한 SQL 형식|간결한 C 형식|자세한 유형|DATETIME_INTERVAL_CODE|  
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
