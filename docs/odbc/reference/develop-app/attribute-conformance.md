---
title: 특성 적합성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2880a35f4bdc997cc037cdd0d60720267ff4a58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306404"
---
# <a name="attribute-conformance"></a>특성 적합성
다음 표는 각 ODBC 환경 특성의 적합성 수준을 나타내며, 이 특성은 잘 정의되어 있습니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|핵심|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] 이것은 선택적 기능이며 준수 수준에 포함되지 않습니다.  
  
 다음 표는 각 ODBC 연결 특성의 적합성 수준을 나타내며, 이 특성은 잘 정의되어 있습니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|핵심|  
|SQL_ATTR_ASYNC_ENABLE|레벨 1/레벨 2[1]|  
|SQL_ATTR_AUTO_IPD|수준 2|  
|SQL_ATTR_AUTOCOMMIT|수준 1|  
|SQL_ATTR_CONNECTION_DEAD|수준 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|수준 2|  
|SQL_ATTR_CURRENT_CATALOG|수준 2|  
|SQL_ATTR_LOGIN_TIMEOUT|수준 2|  
|SQL_ATTR_ODBC_CURSORS|핵심|  
|SQL_ATTR_PACKET_SIZE|수준 2|  
|SQL_ATTR_QUIET_MODE|핵심|  
|SQL_ATTR_TRACE|핵심|  
|SQL_ATTR_TRACEFILE|핵심|  
|SQL_ATTR_TRANSLATE_LIB|핵심|  
|SQL_ATTR_TRANSLATE_OPTION|핵심|  
|SQL_ATTR_TXN_ISOLATION|레벨 1/레벨 2[2]|  
  
 [1] 연결 수준 비동기(수준 1에 필요)를 지원하는 응용 프로그램은 **SQLSetConnectAttr을**호출하여 SQL_TRUE 이 특성 설정을 지원해야 합니다. **SQLSetStmtAttr**을 통해 기본값이 아닌 값으로 특성을 설정할 수 없습니다. 문 수준 비동기(수준 2에 필요)를 지원하는 응용 프로그램은 두 함수 중 하나를 사용하는 SQL_TRUE 이 특성 설정을 지원해야 합니다.  
  
 [2] 레벨 1 인터페이스 적합성의 경우 드라이버는 드라이버 정의 기본값 외에 하나의 값을 지원해야 합니다(SQL_DEFAULT_TXN_ISOLATION 옵션으로 **SQLGetInfo를** 호출하여 사용 가능). 수준 2 인터페이스 준수의 경우 드라이버는 SQL_TXN_SERIALIZABLE 지원해야 합니다.  
  
 다음 표는 각 ODBC 문 특성의 적합성 수준을 나타내며, 이 특성은 잘 정의되어 있습니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|핵심|  
|SQL_ATTR_APP_ROW_DESC|핵심|  
|SQL_ATTR_ASYNC_ENABLE|레벨 1/레벨 2[1]|  
|SQL_ATTR_CONCURRENCY|레벨 1/레벨 2[2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|수준 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|수준 2|  
|SQL_ATTR_CURSOR_TYPE|코어/레벨 2[3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|수준 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|수준 2|  
|SQL_ATTR_IMP_PARAM_DESC|핵심|  
|SQL_ATTR_IMP_ROW_DESC|핵심|  
|SQL_ATTR_KEYSET_SIZE|수준 2|  
|SQL_ATTR_MAX_LENGTH|수준 1|  
|SQL_ATTR_MAX_ROWS|수준 1|  
|SQL_ATTR_METADATA_ID|핵심|  
|SQL_ATTR_NOSCAN|핵심|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|핵심|  
|SQL_ATTR_PARAM_BIND_TYPE|핵심|  
|SQL_ATTR_PARAM_OPERATION_PTR|핵심|  
|SQL_ATTR_PARAM_STATUS_PTR|핵심|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|핵심|  
|SQL_ATTR_PARAMSET_SIZE|핵심|  
|SQL_ATTR_QUERY_TIMEOUT|수준 2|  
|SQL_ATTR_RETRIEVE_DATA|수준 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|핵심|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|핵심|  
|SQL_ATTR_ROW_BIND_TYPE|핵심|  
|SQL_ATTR_ROW_NUMBER|수준 1|  
|SQL_ATTR_ROW_OPERATION_PTR|수준 1|  
|SQL_ATTR_ROW_STATUS_PTR|핵심|  
|SQL_ATTR_ROWS_FETCHED_PTR|핵심|  
|SQL_ATTR_SIMULATE_CURSOR|수준 2|  
|SQL_ATTR_USE_BOOKMARKS|수준 2|  
  
 [1] 연결 수준 비동기(수준 1에 필요)를 지원하는 응용 프로그램은 **SQLSetConnectAttr을**호출하여 SQL_TRUE 이 특성 설정을 지원해야 합니다. **SQLSetStmtAttr**을 통해 기본값이 아닌 값으로 특성을 설정할 수 없습니다. 문 수준 비동기(수준 2에 필요)를 지원하는 응용 프로그램은 두 함수 중 하나를 사용하는 SQL_TRUE 이 특성 설정을 지원해야 합니다.  
  
 [2] 레벨 2 인터페이스 적합성의 경우 드라이버는 SQL_CONCUR_READ_ONLY 하나 이상의 다른 값을 지원해야 합니다.  
  
 [3] 레벨 1 인터페이스 적합성의 경우 드라이버는 SQL_CURSOR_FORWARD_ONLY 하나 이상의 다른 값을 지원해야 합니다. 수준 2 인터페이스 준수의 경우 드라이버는 이 문서에 정의된 모든 값을 지원해야 합니다.
