---
title: 규칙 특성 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 44f1311d98f37412454ad2352366492a8d5a1768
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818843"
---
# <a name="attribute-conformance"></a>특성 적합성
다음 표에서이 방법이 잘 정의 된 각 ODBC 환경 특성의 규칙 수준은 보여 줍니다.  
  
|기능|적합성 수준|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|핵심|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1]이 선택적 기능 이며 따라서 속하지 적합성 수준입니다.  
  
 다음 표에서 각 ODBC 연결 특성에이 잘 정의 된 규칙 수준을 나타냅니다.  
  
|기능|적합성 수준|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|핵심|  
|SQL_ATTR_ASYNC_ENABLE|수준 1/수준 2 [1]|  
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
|SQL_ATTR_TXN_ISOLATION|수준 1/수준 2: [2]|  
  
 [이 특성을 호출 하 여 SQL_TRUE로 설정 (수준 1에 필요) 하는 연결 수준 비동기를 지 원하는 1] 응용 프로그램 지원 해야 합니다 **SQLSetConnectAttr**; 특성을 기본값 이외의 값으로 설정할 수 있어야 합니다. 통해 값 **SQLSetStmtAttr**합니다. 문 수준 비동기 (수준 2에 필요)를 지 원하는 응용 프로그램은이 특성을 함수 중 하나를 사용 하 여 SQL_TRUE로 설정 지원 해야 합니다.  
  
 [2] 수준 1 인터페이스 적합성을 위해 드라이버를 드라이버에서 정의 된 기본 값 외에도 하나의 값을 지원 해야 합니다 (호출 하 여 사용 가능한 **SQLGetInfo** SQL_DEFAULT_TXN_ISOLATION 옵션을 사용 하 여). 수준 2 인터페이스 적합성에 대 한 드라이버 sql_txn_serializable로 지원 해야 합니다.  
  
 다음 표에서이 방법이 잘 정의 된 각 ODBC 문 특성의 규칙 수준은 보여 줍니다.  
  
|기능|적합성 수준|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|핵심|  
|SQL_ATTR_APP_ROW_DESC|핵심|  
|SQL_ATTR_ASYNC_ENABLE|수준 1/수준 2 [1]|  
|SQL_ATTR_CONCURRENCY|수준 1/수준 2: [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|수준 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|수준 2|  
|SQL_ATTR_CURSOR_TYPE|코어/수준 2 [3]|  
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
|SQL_ATTR_ROWS_FETCHED_PTR을 설정|핵심|  
|SQL_ATTR_SIMULATE_CURSOR|수준 2|  
|SQL_ATTR_USE_BOOKMARKS|수준 2|  
  
 [이 특성을 호출 하 여 SQL_TRUE로 설정 (수준 1에 필요) 하는 연결 수준 비동기를 지 원하는 1] 응용 프로그램 지원 해야 합니다 **SQLSetConnectAttr**; 특성을 기본값 이외의 값으로 설정할 수 있어야 합니다. 통해 값 **SQLSetStmtAttr**합니다. 문 수준 비동기 (수준 2에 필요)를 지 원하는 응용 프로그램은이 특성을 함수 중 하나를 사용 하 여 SQL_TRUE로 설정 지원 해야 합니다.  
  
 [2] 수준 2 인터페이스 적합성을 위해 하 고 하나 이상의 다른 값 SQL_CONCUR_READ_ONLY 드라이버 지원 해야 합니다.  
  
 [3] 수준 1 인터페이스 적합성을 위해 SQL_CURSOR_FORWARD_ONLY 및 다른 값이 하나 이상 드라이버를 지원 해야 합니다. 수준 2 인터페이스 적합성에 대 한 드라이버는이 문서에 정의 된 모든 값을 지원 해야 합니다.
