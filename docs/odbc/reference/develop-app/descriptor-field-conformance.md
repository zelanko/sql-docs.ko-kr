---
title: 설명자 필드 적합성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce33adfdbfceef56936b22c549b6762521b4798
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305934"
---
# <a name="descriptor-field-conformance"></a>설명자 필드 적합성
다음 표는 각 ODBC 설명자 헤더 필드의 적합성 수준을 나타내며, 이 필드는 잘 정의되어 있습니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|핵심|  
|SQL_DESC_ARRAY_SIZE|핵심|  
|SQL_DESC_ARRAY_STATUS_PTR|코어(APD, IPR 및 IRD용); 레벨 1 (ARD용)|  
|SQL_DESC_BIND_OFFSET_PTR|핵심|  
|SQL_DESC_BIND_TYPE|핵심|  
|SQL_DESC_COUNT|핵심|  
|SQL_DESC_ROWS_PROCESSED_PTR|핵심|  
  
 다음 표는 각 ODBC 설명자 레코드 필드의 적합성 수준을 나타내며, 이 필드는 잘 정의되어 있습니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|수준 2|  
|SQL_DESC_BASE_COLUMN_NAME|핵심|  
|SQL_DESC_BASE_TABLE_NAME|수준 1|  
|SQL_DESC_CASE_SENSITIVE|핵심|  
|SQL_DESC_CATALOG_NAME|수준 2|  
|SQL_DESC_CONCISE_TYPE|핵심|  
|SQL_DESC_DATA_PTR|핵심|  
|SQL_DESC_DATETIME_INTERVAL_ 코드|코어[1]|  
|SQL_DESC_DATETIME_INTERVAL_ 정밀도|코어[1]|  
|SQL_DESC_DISPLAY_SIZE|핵심|  
|SQL_DESC_FIXED_PREC_SCALE|핵심|  
|SQL_DESC_INDICATOR_PTR|핵심|  
|SQL_DESC_LABEL|수준 2|  
|SQL_DESC_LENGTH|핵심|  
|SQL_DESC_LITERAL_PREFIX|핵심|  
|SQL_DESC_LITERAL_SUFFIX|핵심|  
|SQL_DESC_LOCAL_TYPE_NAME|핵심|  
|SQL_DESC_NAME|핵심|  
|SQL_DESC_NULLABLE|핵심|  
|SQL_DESC_OCTET_LENGTH|핵심|  
|SQL_DESC_OCTET_LENGTH_PTR|핵심|  
|SQL_DESC_PARAMETER_TYPE|코어/레벨 2[2]|  
|SQL_DESC_PRECISION|핵심|  
|SQL_DESC_ROWVER|수준 1|  
|SQL_DESC_SCALE|핵심|  
|SQL_DESC_SCHEMA_NAME|수준 1|  
|SQL_DESC_SEARCHABLE|핵심|  
|SQL_DESC_TABLE_NAME|수준 1|  
|SQL_DESC_TYPE|핵심|  
|SQL_DESC_TYPE_NAME|핵심|  
|SQL_DESC_UNNAMED|핵심|  
|SQL_DESC_UNSIGNED|핵심|  
|SQL_DESC_UPDATABLE|핵심|  
  
 [1] 드라이버가 해당 데이터 형식을 지원하는 경우에만 이러한 레코드 필드에 대한 지원이 필요합니다.  
  
 [2] 코어 레벨 적합성의 경우 운전자는 SQL_PARAM_INPUT 지원해야 합니다. 레벨 2 인터페이스 준수의 경우 드라이버는 SQL_PARAM_INPUT_OUTPUT SQL_PARAM_OUTPUT 지원해야 합니다.
