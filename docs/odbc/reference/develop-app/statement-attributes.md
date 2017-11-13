---
title: "문 특성 | Microsoft Docs"
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
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d50c660ed3b405a7ae9fec6b9c66a9b395605025
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="statement-attributes"></a>문 특성
문 특성은 문이의 특성입니다. 예를 들어 설명의 결과 함께 사용할 커서를 설정 및 사용 하 여 책갈피 어떤 종류의 여부는 문 특성입니다.  
  
 문 특성 설정 됩니다 **SQLSetStmtAttr** 의 현재 설정은 사용 하 여 검색 및 **SQLGetStmtAttr**합니다. 응용 프로그램 설정 모든 문 특성; 있는지 요구 사항은 없습니다. 모든 문 특성에는 기본값, 일부는 드라이버별 합니다.  
  
 문 특성을 설정할 수 있습니다 특성 자체에 따라 달라 집니다. 문 특성 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, 및 SQL_ATTR_USE_BOOKMARKS 문이 실행 되기 전에 설정 되어야 합니다. SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_NOSCAN 문 특성은 언제 든 지 설정할 수 있지만 문을 다시 사용 될 때까지 적용 되지 않습니다. 언제 든 지 SQL_ATTR_MAX_LENGTH 및 SQL_ATTR_MAX_ROWS, SQL_ATTR_QUERY_TIMEOUT 문 특성을 설정할 수 이지만 드라이버 관련 여부는 문을 다시 사용 하기 전에 적용 됩니다. 언제 든 지 나머지 문 특성을 설정할 수 있습니다.  
  
> [!NOTE]  
>  연결 수준에서 호출 하 여 문 특성을 설정 하는 기능 **SQLSetConnectAttr** 사용 되지 ODBC 3. *x*합니다. ODBC 3입니다. *x* 응용 프로그램 연결 수준에서 문 특성을 설정 해서는 안됩니다. ODBC 3입니다. *x* 드라이버 ODBC 2와 작동 해야 하는 경우이 기능을 지원만 필요 합니다. *x* 응용 프로그램입니다. 자세한 내용은 참조 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
>   
>  이 예외는 연결 특성 및 문 특성 모두에 있으며 연결 수준 또는 문 수준에서 설정할 수 있는 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성입니다.  
>   
>  ODBC 3에 도입 된 문 특성의 없음. *x* SQL_ATTR_METADATA_ID) (제외 연결 수준에서 설정할 수 있습니다.  
  
 자세한 내용은 참조는 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명 합니다.

