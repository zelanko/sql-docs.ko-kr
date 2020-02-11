---
title: 특성 규칙 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71f0da7bbd7ef1a37a1f48539c7230bff0ceda15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909909"
---
# <a name="attribute-conformance"></a>특성 적합성
다음 표는 잘 정의 된 각 ODBC 환경 특성의 규칙 수준을 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|코어|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1]이 기능은 선택적 기능이 며 규칙 수준의 일부가 아닙니다.  
  
 다음 표는 잘 정의 된 각 ODBC 연결 특성의 규칙 수준을 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|코어|  
|SQL_ATTR_ASYNC_ENABLE|수준 1/수준 2 [1]|  
|SQL_ATTR_AUTO_IPD|Level 2|  
|SQL_ATTR_AUTOCOMMIT|수준 1|  
|SQL_ATTR_CONNECTION_DEAD|수준 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|Level 2|  
|SQL_ATTR_CURRENT_CATALOG|Level 2|  
|SQL_ATTR_LOGIN_TIMEOUT|Level 2|  
|SQL_ATTR_ODBC_CURSORS|코어|  
|SQL_ATTR_PACKET_SIZE|Level 2|  
|SQL_ATTR_QUIET_MODE|코어|  
|SQL_ATTR_TRACE|코어|  
|SQL_ATTR_TRACEFILE|코어|  
|SQL_ATTR_TRANSLATE_LIB|코어|  
|SQL_ATTR_TRANSLATE_OPTION|코어|  
|SQL_ATTR_TXN_ISOLATION|수준 1/수준 2 [2]|  
  
 [1] 연결 수준 비동기를 지 원하는 응용 프로그램 (수준 1에 필요) **SQLSetConnectAttr**;를 호출 하 여이 특성을 SQL_TRUE로 설정 하는 것을 지원 해야 합니다. 특성은 **SQLSetStmtAttr**를 통해 기본값이 아닌 다른 값으로 설정할 필요가 없습니다. 문 수준 비동기 (수준 2에 필요)를 지 원하는 응용 프로그램은 두 함수를 사용 하 여이 특성을 SQL_TRUE로 설정 하는 것을 지원 해야 합니다.  
  
 [2] 수준 1 인터페이스 규칙의 경우 드라이버는 드라이버 정의 기본값 (SQL_DEFAULT_TXN_ISOLATION 옵션으로 **SQLGetInfo** 를 호출 하 여 사용 가능) 외에도 하나의 값을 지원 해야 합니다. 수준 2 인터페이스 규칙의 경우 드라이버는 SQL_TXN_SERIALIZABLE도 지원 해야 합니다.  
  
 다음 표는 잘 정의 된 각 ODBC 문 특성의 규칙 수준을 나타냅니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|코어|  
|SQL_ATTR_APP_ROW_DESC|코어|  
|SQL_ATTR_ASYNC_ENABLE|수준 1/수준 2 [1]|  
|SQL_ATTR_CONCURRENCY|수준 1/수준 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|수준 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|Level 2|  
|SQL_ATTR_CURSOR_TYPE|코어/수준 2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|Level 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Level 2|  
|SQL_ATTR_IMP_PARAM_DESC|코어|  
|SQL_ATTR_IMP_ROW_DESC|코어|  
|SQL_ATTR_KEYSET_SIZE|Level 2|  
|SQL_ATTR_MAX_LENGTH|수준 1|  
|SQL_ATTR_MAX_ROWS|수준 1|  
|SQL_ATTR_METADATA_ID|코어|  
|SQL_ATTR_NOSCAN|코어|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|코어|  
|SQL_ATTR_PARAM_BIND_TYPE|코어|  
|SQL_ATTR_PARAM_OPERATION_PTR|코어|  
|SQL_ATTR_PARAM_STATUS_PTR|코어|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|코어|  
|SQL_ATTR_PARAMSET_SIZE|코어|  
|SQL_ATTR_QUERY_TIMEOUT|Level 2|  
|SQL_ATTR_RETRIEVE_DATA|수준 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|코어|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|코어|  
|SQL_ATTR_ROW_BIND_TYPE|코어|  
|SQL_ATTR_ROW_NUMBER|수준 1|  
|SQL_ATTR_ROW_OPERATION_PTR|수준 1|  
|SQL_ATTR_ROW_STATUS_PTR|코어|  
|SQL_ATTR_ROWS_FETCHED_PTR|코어|  
|SQL_ATTR_SIMULATE_CURSOR|Level 2|  
|SQL_ATTR_USE_BOOKMARKS|Level 2|  
  
 [1] 연결 수준 비동기를 지 원하는 응용 프로그램 (수준 1에 필요) **SQLSetConnectAttr**;를 호출 하 여이 특성을 SQL_TRUE로 설정 하는 것을 지원 해야 합니다. 특성은 **SQLSetStmtAttr**를 통해 기본값이 아닌 다른 값으로 설정할 필요가 없습니다. 문 수준 비동기 (수준 2에 필요)를 지 원하는 응용 프로그램은 두 함수를 사용 하 여이 특성을 SQL_TRUE로 설정 하는 것을 지원 해야 합니다.  
  
 [2] 수준 2 인터페이스 규칙의 경우 드라이버는 SQL_CONCUR_READ_ONLY 및 하나 이상의 다른 값을 지원 해야 합니다.  
  
 [3] 수준 1 인터페이스 규칙의 경우 드라이버는 SQL_CURSOR_FORWARD_ONLY 및 하나 이상의 다른 값을 지원 해야 합니다. 수준 2 인터페이스 규칙의 경우 드라이버는이 문서에 정의 된 모든 값을 지원 해야 합니다.
