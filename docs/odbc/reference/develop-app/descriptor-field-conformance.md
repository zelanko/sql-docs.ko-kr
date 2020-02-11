---
title: 설명자 필드 규칙 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952341"
---
# <a name="descriptor-field-conformance"></a>설명자 필드 적합성
다음 표에서는 잘 정의 된 각 ODBC 설명자 헤더 필드의 규칙 수준을 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|코어|  
|SQL_DESC_ARRAY_SIZE|코어|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (APD, IPR 및 IRD의 경우) 수준 1 (기타)|  
|SQL_DESC_BIND_OFFSET_PTR|코어|  
|SQL_DESC_BIND_TYPE|코어|  
|SQL_DESC_COUNT|코어|  
|SQL_DESC_ROWS_PROCESSED_PTR|코어|  
  
 다음 표에서는 잘 정의 된 각 ODBC 설명자 레코드 필드의 규칙 수준을 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Level 2|  
|SQL_DESC_BASE_COLUMN_NAME|코어|  
|SQL_DESC_BASE_TABLE_NAME|수준 1|  
|SQL_DESC_CASE_SENSITIVE|코어|  
|SQL_DESC_CATALOG_NAME|Level 2|  
|SQL_DESC_CONCISE_TYPE|코어|  
|SQL_DESC_DATA_PTR|코어|  
|SQL_DESC_DATETIME_INTERVAL_ 코드|코어 [1]|  
|SQL_DESC_DATETIME_INTERVAL_ 정밀도|코어 [1]|  
|SQL_DESC_DISPLAY_SIZE|코어|  
|SQL_DESC_FIXED_PREC_SCALE|코어|  
|SQL_DESC_INDICATOR_PTR|코어|  
|SQL_DESC_LABEL|Level 2|  
|SQL_DESC_LENGTH|코어|  
|SQL_DESC_LITERAL_PREFIX|코어|  
|SQL_DESC_LITERAL_SUFFIX|코어|  
|SQL_DESC_LOCAL_TYPE_NAME|코어|  
|SQL_DESC_NAME|코어|  
|SQL_DESC_NULLABLE|코어|  
|SQL_DESC_OCTET_LENGTH|코어|  
|SQL_DESC_OCTET_LENGTH_PTR|코어|  
|SQL_DESC_PARAMETER_TYPE|코어/수준 2 [2]|  
|SQL_DESC_PRECISION|코어|  
|SQL_DESC_ROWVER|수준 1|  
|SQL_DESC_SCALE|코어|  
|SQL_DESC_SCHEMA_NAME|수준 1|  
|SQL_DESC_SEARCHABLE|코어|  
|SQL_DESC_TABLE_NAME|수준 1|  
|SQL_DESC_TYPE|코어|  
|SQL_DESC_TYPE_NAME|코어|  
|SQL_DESC_UNNAMED|코어|  
|SQL_DESC_UNSIGNED|코어|  
|SQL_DESC_UPDATABLE|코어|  
  
 [1] 이러한 레코드 필드에 대 한 지원은 드라이버가 해당 데이터 형식을 지 원하는 경우에만 필요 합니다.  
  
 [2] 코어 수준 규칙의 경우 드라이버가 SQL_PARAM_INPUT을 지원 해야 합니다. 수준 2 인터페이스 규칙의 경우 드라이버는 SQL_PARAM_INPUT_OUTPUT 및 SQL_PARAM_OUTPUT도 지원 해야 합니다.
