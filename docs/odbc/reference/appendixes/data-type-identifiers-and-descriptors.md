---
title: 데이터 형식 식별자 및 설명자 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
- descriptors [ODBC], data types
- verbose data types [ODBC]
- data types [ODBC], descriptors
- concise data types [ODBC]
ms.assetid: f0077c9b-8eb2-4b5f-8c4c-7436fdef37ab
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9d36c0308ae7afb12541a0f33f4d2b417dfb15e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-identifiers-and-descriptors"></a>데이터 형식 식별자 및 설명자
데이터 형식에 나열 된는 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 및 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 이 부록 앞부분의 섹션은 "간결한" 데이터 형식: 각 식별자 단일 데이터 형식을 참조 합니다. 식별자 및 데이터 형식 간의 한 일 대응이 됩니다. 하지만 설명자는 작업을 수행할에 있지 않은 모든 경우 데이터 형식을 식별 하는 단일 값을 사용 합니다. 일부 경우에는 "verbose" 데이터 형식 및 형식 하위 코드 사용 합니다. 날짜/시간 및 간격 데이터 형식 제외한 모든 데이터 형식에 대 한 자세한 정보 표시 형식 식별자가 있는 간결한 형식 식별자와 동일 하 고 값을 SQL_DESC_DATETIME_INTERVAL_CODE의 값은 0과 같습니다. 그러나 날짜/시간 및 간격 데이터 형식의 SQL_DESC_TYPE에 저장 됩니다 (SQL_DATETIME 또는 sql_interval 인) 자세한 정보 표시 유형, SQL_DESC_CONCISE_TYPE, 간결한 형식은 저장 됩니다 및 각 간결한 형식에 대 한 하위 코드 값을 SQL_DESC_DATETIME_INTERVAL_CODE에 저장 됩니다. 이러한 필드 중 하나를 설정 다른 영향을 줍니다. 이러한 필드에 대 한 자세한 내용은 참조는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명 합니다.  
  
 일부 데이터 형식에 대 한 SQL_DESC_TYPE 또는 SQL_DESC_CONCISE_TYPE 필드 설정 되 면 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_LENGTH, SQL_DESC_PRECISION, 및 SQL_DESC_SCALE 필드 적용 되는 데이터에 대 한 기본값을 하도록 자동 설정 됩니다. 입력 합니다. 자세한 내용은 참조의 SQL_DESC_TYPE 필드에 대 한 설명을 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 응용 프로그램에 대 한 호출을 통해 설명자 필드를 명시적으로 설정 해야 적절 한 설정 된 기본값 중 하나라도 없으면 **SQLSetDescField**합니다.  
  
 다음 표에서 간결한 형식 식별자, 자세한 정보 표시 유형 식별자 및 각 날짜/시간 및 간격 SQL 및 C 형식 식별자에 대 한 하위 형식 코드를 보여 줍니다. SQL_DESC_TYPE 및 값을 SQL_DESC_DATETIME_INTERVAL_CODE 필드 (구현 설명자)에서 SQL 데이터 형식 및 응용 프로그램 (에서 C 데이터 형식에 동일한 매니페스트 상수는 날짜/시간 및 간격 데이터 형식의 경우이 테이블에 따르면 설명자)입니다.  
  
|간결한 SQL 유형|간단한 C 형식|자세한 정보 표시 유형|DATETIME_INTERVAL_CODE|  
|----------------------|--------------------|------------------|------------------------------|  
|SQL_TYPE_DATE|SQL_C_TYPE_DATE|SQL_DATETIME|SQL_CODE_DATE|  
|SQL_TYPE_TIME|SQL_C_TYPE_TIME|SQL_DATETIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_DATETIME|SQL_CODE_TIMESTAMP|  
|SQL_INTERVAL_MONTH|SQL_C_INTERVAL_MONTH|SQL_INTERVAL|SQL_CODE_MONTH|  
|SQL_INTERVAL_YEAR|SQL_C_INTERVAL_YEAR|SQL_INTERVAL|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_INTERVAL|SQL_CODE_YEAR_TO_MONTH|  
QL_INTERVAL_DAY|SQL_C_INTERVAL_DAY|SQL_INTERVAL|SQL_CODE_DAY|  
|SQL_INTERVAL_HOUR|SQL_C_INTERVAL_HOUR|SQL_INTERVAL|SQL_CODE_HOUR|  
|SQL_INTERVAL_MINUTE|SQL_C_INTERVAL_MINUTE|SQL_INTERVAL|SQL_CODE_MINUTE|  
|SQL_INTERVAL_SECOND|SQL_C_INTERVAL_SECOND|SQL_INTERVAL|SQL_CODE_SECOND|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_C_INTERVAL_DAY_TO_HOUR|SQL_INTERVAL|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE|SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_INTERVAL|SQL_CODE_DAY_TO_MINUTE|  
QL_INTERVAL_DAY_TO_SECOND|SQL_C_INTERVAL_DAY_TO_SECOND|SQL_INTERVAL|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR_TO_MINUTE|SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_INTERVAL|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND|SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_INTERVAL|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE_TO_SECOND|SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_INTERVAL|SQL_CODE_MINUTE_TO_SECOND|
