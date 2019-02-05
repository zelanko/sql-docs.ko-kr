---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1d8f0a79f9bcd08fc74bc9d5e7fd52da4a2709
ms.sourcegitcommit: cebfa2610ea36e3c5ad510c214590035ecb499c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689896"
---
# <a name="data-type-identifiers-and-descriptors"></a>데이터 형식 식별자 및 설명자
데이터 형식에 나열 된 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 및 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 이 부록 앞부분에서의 섹션은 "간결 하 게" 데이터 형식: 각 식별자 단일 데이터 형식을 참조 합니다. 식별자 및 데이터 형식 간의 한 일 대응이 됩니다. 그러나 설명자, 수행 되지 모든 사례 데이터 형식을 식별 하려면 단일 값을 사용 합니다. 경우에 따라 "verbose" 데이터 형식 및 형식 하위 코드를 사용합니다. 날짜/시간 및 간격 데이터 형식 제외한 모든 데이터 형식에 대 한 자세한 정보 표시 형식 식별자 간결한 형식 식별자와 동일 이며 SQL_DESC_DATETIME_INTERVAL_CODE의 값은 0과 같습니다. 그러나 날짜/시간 및 간격 데이터 형식에 대해 (SQL_DATETIME 또는 sql_interval 인) 형식을 verbose SQL_DESC_TYPE에 저장 됩니다, 간결한 형식 SQL_DESC_CONCISE_TYPE에 저장 됩니다 및 하위 코드가 각 간결한 형식에 대 한 값을 SQL_DESC_DATETIME_INTERVAL_CODE에 저장 됩니다. 이러한 필드 중 하나를 설정 다른 영향을 줍니다. 이러한 필드에 대 한 자세한 내용은 참조는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명 합니다.  
  
 SQL_DESC_TYPE 또는 SQL_DESC_CONCISE_TYPE 필드는 일부 데이터 형식에 대해 설정 되 면 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, 자릿수가 SQL_DESC_PRECISION, 및 자릿수가 SQL_DESC_SCALE 필드는 자동으로 기본값으로 설정, 데이터에 대해 적용 가능한 형식입니다. 자세한 내용은의 SQL_DESC_TYPE 필드에 대 한 설명을 참조 하세요 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 응용 프로그램에 대 한 호출을 통해 설명자 필드를 명시적으로 설정 해야 적절 한 기본 값 집합 중 하나라도 없으면 **SQLSetDescField**합니다.  
  
 다음 표에서 간결한 형식 식별자, 자세한 정보 표시 형식 식별자 및 각 날짜/시간 및 간격 SQL C 형식 식별자에 대 한 하위 형식 코드를 보여 줍니다. SQL_DESC_TYPE 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 (구현 설명자)에서 SQL 데이터 형식 및 C 데이터 형식 (응용 프로그램에에서 대 한 동일한 매니페스트 상수는 표에 나와 있듯이이, datetime 및 간격 데이터 형식에 대 한 설명자)입니다.  
  
|간단한 SQL 형식|간단한 C 형식|자세한 정보 표시 형식|DATETIME_INTERVAL_CODE|  
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
