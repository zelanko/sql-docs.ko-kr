---
title: Statement 특성 | Microsoft Docs
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
ms.openlocfilehash: c74f1a79ef79b682bc2900d671e07bbe34c4dbf5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107269"
---
# <a name="statement-attributes"></a>문 특성
문 특성은 문의 특징입니다. 예를 들어 책갈피를 사용할지 여부와 문의 결과 집합에 사용할 커서의 종류는 문 특성입니다.  
  
 Statement 특성은 **SQLSetStmtAttr** 를 사용 하 여 설정 되며 현재 설정은 **SQLGetStmtAttr**로 검색 됩니다. 응용 프로그램에서 문 특성을 설정 해야 하는 요구 사항은 없습니다. 모든 문 특성에는 기본값이 있으며, 그 중 일부는 드라이버 전용입니다.  
  
 문 특성을 설정할 수 있는 경우 특성 자체에 따라 달라 집니다. 문이 실행 되기 전에 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR 및 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정 해야 합니다. SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_NOSCAN 문 특성은 언제 든 지 설정할 수 있지만 문이 다시 사용 될 때까지 적용 되지 않습니다. SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS 및 SQL_ATTR_QUERY_TIMEOUT 문 특성은 언제 든 지 설정할 수 있지만, 문이 다시 사용 되기 전에 적용 되는지 여부는 드라이버 마다 다릅니다. 나머지 문 특성은 언제 든 지 설정할 수 있습니다.  
  
> [!NOTE]  
>  **SQLSetConnectAttr** 를 호출 하 여 연결 수준에서 문 특성을 설정 하는 기능은 ODBC 3에서 더 이상 사용 되지 않습니다. *x*. ODBC 3. *x* 응용 프로그램은 연결 수준에서 문 특성을 설정 하면 안 됩니다. ODBC 3. *x* 드라이버는 ODBC 2를 사용 해야 하는 경우에만이 기능을 지원 해야 합니다. *x* 응용 프로그램. 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 을 참조 하세요.  
>   
>  이에 대 한 예외는 연결 특성 및 문 특성 모두 이며 연결 수준 또는 문 수준에서 설정할 수 있는 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성입니다.  
>   
>  ODBC 3에 도입 된 문 특성은 없습니다. 연결 수준에서 *x* (SQL_ATTR_METADATA_ID 제외)를 설정할 수 있습니다.  
  
 자세한 내용은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명을 참조 하세요.
