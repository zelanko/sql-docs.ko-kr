---
title: "설명자 필드 규칙 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 049208450144fdd1c1d3b902093517627486ccf9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-field-conformance"></a>설명자 필드 규칙
다음 표에서이 잘 정의 된 각 ODBC 설명자 헤더 필드의 규칙 수준과 보여 줍니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|핵심|  
|SQL_DESC_ARRAY_SIZE|핵심|  
|SQL_DESC_ARRAY_STATUS_PTR|코어 (용 APD, IPR, 및 IRD); 수준 1 ()|  
|SQL_DESC_BIND_OFFSET_PTR|핵심|  
|SQL_DESC_BIND_TYPE|핵심|  
|SQL_DESC_COUNT|핵심|  
|SQL_DESC_ROWS_PROCESSED_PTR|핵심|  
  
 다음 표는 각 ODBC 설명자 레코드 필드에서이 잘 정의의 규칙 수준과를 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|수준 2|  
|SQL_DESC_BASE_COLUMN_NAME|핵심|  
|SQL_DESC_BASE_TABLE_NAME|수준 1|  
|SQL_DESC_CASE_SENSITIVE|핵심|  
|SQL_DESC_CATALOG_NAME|수준 2|  
|SQL_DESC_CONCISE_TYPE|핵심|  
|SQL_DESC_DATA_PTR|핵심|  
|SQL_DESC_DATETIME_INTERVAL_ 코드|코어 [1]|  
|SQL_DESC_DATETIME_INTERVAL_ 정밀도|코어 [1]|  
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
|DESC_PARAMETER_TYPE|코어/수준 2 [2]|  
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
  
 [이러한 레코드 필드에 대 한 지원 되는 1]은 드라이버는 해당 데이터 형식을 지원 하는 경우에 필요 합니다.  
  
 [2] 핵심 수준 규칙에 대 한 드라이버 SQL_PARAM_INPUT을 지원 해야 합니다. 수준 2 인터페이스 규칙에 대 한 드라이버 및 지원 해야 SQL_PARAM_INPUT_OUTPUT SQL_PARAM_OUTPUT 합니다.

