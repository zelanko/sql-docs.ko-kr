---
title: 문 특성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e669f02eeb76ba529c75851ce8bf6ff9a7831a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149095"
---
# <a name="statement-attributes"></a>문 특성
문 특성은 문 특성입니다. 예를 들어 문의 결과 사용 하는 커서 및 사용 하 여 책갈피 어떤 종류의 설정 여부를 나타내는 경우 문 특성  
  
 사용 하 여 문 특성 설정 **SQLSetStmtAttr** 사용 하 여 현재 설정을 검색 하 고 **SQLGetStmtAttr**합니다. 응용 프로그램을 모든 문 특성을 설정할는 요구 사항은 없습니다. 모든 문 특성 기본값이, 일부는 드라이버별 있습니다.  
  
 문 특성을 설정할 수 있습니다 특성 자체에 따라 달라 집니다. SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, 및 SQL_ATTR_USE_BOOKMARKS 문 특성은 문이 실행 되기 전에 설정 되어야 합니다. SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_NOSCAN 문 특성을 언제 든 지 설정할 수 있지만 문을 다시 사용 될 때까지 적용 되지 않습니다. 언제 든 지 SQL_ATTR_MAX_LENGTH을 SQL_ATTR_MAX_ROWS을 SQL_ATTR_QUERY_TIMEOUT 문 특성을 설정할 수 있습니다 이지만 드라이버별 여부 문을 다시 사용 하기 전에 적용 됩니다. 언제 든 지 나머지 문 특성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  연결 수준에서 호출 하 여 문 특성을 설정 하는 기능 **SQLSetConnectAttr** 사용 되지 ODBC 3. *x*합니다. ODBC 3입니다. *x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC 3입니다. *x* 드라이버는 ODBC 2를 사용 하 여 작동 하는 경우이 기능을 지원만 필요 합니다. *x* 응용 프로그램입니다. 자세한 내용은 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
>   
>  이 예외는 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성을 연결 특성 및 문 특성을 모두 되 고 연결 수준 또는 문 수준에서 설정할 수 있습니다.  
>   
>  ODBC 3에 도입 된 문 특성의 none입니다. *x* SQL_ATTR_METADATA_ID) (제외 연결 수준에서 설정할 수 있습니다.  
  
 자세한 내용은 참조는 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명 합니다.
