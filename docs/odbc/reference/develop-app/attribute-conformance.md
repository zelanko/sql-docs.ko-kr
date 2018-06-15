---
title: 규칙에 따라 특성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c765982a35fd41fc36fdc82ddbd3434b2d90c07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913738"
---
# <a name="attribute-conformance"></a>특성 규칙
다음 표에서이 잘 정의 된 각 ODBC 환경 특성의 규칙 수준과 보여 줍니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|핵심|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1]이 선택적 기능 및 받는 규칙 수준에 속하지 않는 따라서 합니다.  
  
 다음 표에서이 잘 정의 된 각 ODBC 연결 특성의 규칙 수준과 보여 줍니다.  
  
|함수|규칙 수준|  
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
|SQL_ATTR_TXN_ISOLATION|수준 1/수준 2 [2]|  
  
 [호출 하 여이 특성을 SQL_TRUE로 설정 (수준 1에 필요) 하는 연결 수준 비동기 지원 되는 1] 응용 프로그램 지원 해야 **SQLSetConnectAttr**; 특성은 기본값 이외의 값으로 설정할 수 없습니다 통해 값 **SQLSetStmtAttr**합니다. 이 특성을 함수 중 하나를 사용 하 여 SQL_TRUE로 설정 (수준 2에 필요) 하는 문 수준 비동기 지원 되는 응용 프로그램 지원 해야 합니다.  
  
 [2] 수준 1 인터페이스 규칙에 대 한 드라이버 드라이버에서 정의한 기본값 외에도 하나의 값을 지원 해야 합니다 (호출 하 여 사용 가능한 **SQLGetInfo** SQL_DEFAULT_TXN_ISOLATION 옵션). 수준 2 인터페이스 규칙에 따라 드라이버 SQL_TXN_SERIALIZABLE 사항도 지원 해야 합니다.  
  
 다음 표에서이 잘 정의 된 각 ODBC 문 특성의 규칙 수준과 보여 줍니다.  
  
|함수|규칙 수준|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|핵심|  
|SQL_ATTR_APP_ROW_DESC|핵심|  
|SQL_ATTR_ASYNC_ENABLE|수준 1/수준 2 [1]|  
|SQL_ATTR_CONCURRENCY|수준 1/수준 2 [2]|  
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
|SQL_ATTR_ROW_STATUS_PTR을|핵심|  
|SQL_ATTR_ROWS_FETCHED_PTR|핵심|  
|SQL_ATTR_SIMULATE_CURSOR|수준 2|  
|SQL_ATTR_USE_BOOKMARKS|수준 2|  
  
 [호출 하 여이 특성을 SQL_TRUE로 설정 (수준 1에 필요) 하는 연결 수준 비동기 지원 되는 1] 응용 프로그램 지원 해야 **SQLSetConnectAttr**; 특성은 기본값 이외의 값으로 설정할 수 없습니다 통해 값 **SQLSetStmtAttr**합니다. 이 특성을 함수 중 하나를 사용 하 여 SQL_TRUE로 설정 (수준 2에 필요) 하는 문 수준 비동기 지원 되는 응용 프로그램 지원 해야 합니다.  
  
 [2] 수준 2 인터페이스 규칙에 대 한 드라이버 SQL_CONCUR_READ_ONLY 및 다른 값이 하나 이상 지원 해야 합니다.  
  
 [3] 수준 1 인터페이스 규칙에 대 한 드라이버 SQL_CURSOR_FORWARD_ONLY 및 다른 값이 하나 이상 지원 해야 합니다. 수준 2 인터페이스 규칙에 대 한 드라이버는이 문서에 정의 된 모든 값을 지원 해야 합니다.
