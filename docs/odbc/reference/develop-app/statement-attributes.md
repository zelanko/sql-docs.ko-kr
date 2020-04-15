---
title: 명령문 속성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299646"
---
# <a name="statement-attributes"></a>문 특성
명령문 특성은 명령문의 특성입니다. 예를 들어 책갈피와 명령문의 결과 집합에 사용할 커서의 종류를 사용할지 여부는 문 특성입니다.  
  
 문 특성은 **SQLSetStmtAttr** 및 **SQLGetStmtAttr로**검색된 현재 설정으로 설정됩니다. 응용 프로그램이 문 특성을 설정할 필요는 없습니다. 모든 문 특성에는 기본값이 있으며, 그 중 일부는 드라이버에 따라 다릅니다.  
  
 문 특성을 설정할 수 있는 경우 특성 자체에 따라 다릅니다. SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR 및 SQL_ATTR_USE_BOOKMARKS 명령문 특성은 문이 실행되기 전에 설정되어야 합니다. SQL_ATTR_ASYNC_ENABLE 및 SQL_ATTR_NOSCAN 문 특성은 언제든지 설정할 수 있지만 문이 다시 사용될 때까지 적용되지 않습니다. SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS 및 SQL_ATTR_QUERY_TIMEOUT 명령문 특성은 언제든지 설정할 수 있지만 명령문이 다시 사용되기 전에 적용되는지 여부는 드라이버에 따라 다릅니다. 나머지 문 특성은 언제든지 설정할 수 있습니다.  
  
> [!NOTE]  
>  **SQLSetConnectAttr을** 호출 하여 연결 수준에서 문 특성을 설정 하는 기능은 ODBC 3에서 더 이상 사용 되지 않았습니다. *x*. ODBC 3. *x* 응용 프로그램은 연결 수준에서 문 특성을 설정해서는 안 됩니다. ODBC 3. *x* 드라이버는 ODBC 2에서 작동해야 하는 경우에만 이 기능을 지원하면 됩니다. *x* 응용 프로그램. 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침의 [SQLSetConnectOption 매핑을](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) 참조하십시오.  
>   
>  이에 대한 예외는 연결 특성 및 문 특성모두인 SQL_ATTR_METADATA_ID 및 SQL_ATTR_ASYNC_ENABLE 특성이며 연결 수준 또는 명령문 수준에서 설정할 수 있습니다.  
>   
>  ODBC 3에 도입된 문 특성은 없습니다. *x(SQL_ATTR_METADATA_ID* 제외)는 연결 수준에서 설정할 수 있습니다.  
  
 자세한 내용은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명을 참조하십시오.
