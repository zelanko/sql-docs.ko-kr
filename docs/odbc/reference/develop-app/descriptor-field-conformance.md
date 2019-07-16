---
title: 설명자 필드 적합성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afdb1f18ad641224d13373436dd58f1919a3d280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952341"
---
# <a name="descriptor-field-conformance"></a>설명자 필드 적합성
다음 표에서이 방법이 잘 정의 된 각 ODBC 설명자 헤더 필드의 규칙 수준은 보여 줍니다.  
  
|함수|적합성 수준|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|코어 (APD, IPR, 및 IRD); 수준 1 ()|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 다음 표에서이 방법이 잘 정의 된 각 ODBC 설명자 레코드 필드의 규칙 수준은 보여 줍니다.  
  
|함수|적합성 수준|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|수준 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|수준 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|수준 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|SQL_DESC_DATETIME_INTERVAL_ CODE|Core [1]|  
|SQL_DESC_DATETIME_INTERVAL_ PRECISION|Core [1]|  
|SQL_DESC_DISPLAY_SIZE|Core|  
|SQL_DESC_FIXED_PREC_SCALE|Core|  
|SQL_DESC_INDICATOR_PTR|Core|  
|SQL_DESC_LABEL|수준 2|  
|SQL_DESC_LENGTH|Core|  
|SQL_DESC_LITERAL_PREFIX|Core|  
|SQL_DESC_LITERAL_SUFFIX|Core|  
|SQL_DESC_LOCAL_TYPE_NAME|Core|  
|SQL_DESC_NAME|Core|  
|SQL_DESC_NULLABLE|Core|  
|SQL_DESC_OCTET_LENGTH|Core|  
|SQL_DESC_OCTET_LENGTH_PTR|Core|  
|SQL_DESC_PARAMETER_TYPE|코어/수준 2 [2]|  
|SQL_DESC_PRECISION|Core|  
|SQL_DESC_ROWVER|수준 1|  
|SQL_DESC_SCALE|Core|  
|SQL_DESC_SCHEMA_NAME|수준 1|  
|SQL_DESC_SEARCHABLE|Core|  
|SQL_DESC_TABLE_NAME|수준 1|  
|SQL_DESC_TYPE|Core|  
|SQL_DESC_TYPE_NAME|Core|  
|SQL_DESC_UNNAMED|Core|  
|SQL_DESC_UNSIGNED|Core|  
|SQL_DESC_UPDATABLE|Core|  
  
 [이러한 레코드 필드에 대 한 지원 되는 1]는 드라이버는 해당 데이터 형식을 지원 하는 경우에 필요 합니다.  
  
 [2] 핵심 수준 규칙에 대 한 드라이버 SQL_PARAM_INPUT을 지원 해야 합니다. 수준 2 인터페이스 적합성을 위해 SQL_PARAM_INPUT_OUTPUT 및 SQL_PARAM_OUTPUT 드라이버 지원도 해야 합니다.
