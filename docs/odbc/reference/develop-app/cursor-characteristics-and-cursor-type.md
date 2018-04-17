---
title: 커서 특성 및 커서 유형을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f54cc2f954a67d7a9cb3a4dfa6f6a006b652611d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-characteristics-and-cursor-type"></a>커서 특성 및 커서 유형
응용 프로그램 (정방향 전용, 정적, 키 집합 커서 또는 동적) 커서 유형을 지정 하는 대신 커서의 특징을 지정할 수 있습니다. 이 위해 응용 프로그램 선택 (으로 SQL_ATTR_CURSOR_SCROLLABLE 문 특성 설정) 커서의 스크롤 가능 여부 및 민감도 (으로 SQL_ATTR_CURSOR_SENSITIVITY 문 특성 설정) 문에서 커서를 열기 전에 핸들입니다. 드라이버는 다음 있는 특성을 가장 효율적으로 제공 하는 커서 유형을 요청한 응용 프로그램을 선택 합니다.  
  
 응용 프로그램이 문 특성 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE 및 SQL_ATTR_CURSOR_SENSITIVITY, SQL_ATTR_CURSOR_TYPE 중에 설정 될 때마다 드라이버에 게 필요한 모든 변경이 집합이 다른 문 특성 4 개의 특성을 해당 값을 일관 된 상태로 유지 되도록 합니다. 결과적으로, 응용 프로그램에는 커서 특성 지정, 드라이버 특성을 변경할 수 암시적이 선택을; 기반으로 하는 커서 유형을 나타내는 응용 프로그램에는 형식을 지정 하는 경우 드라이버 선택한 유형의 특성와 일치 하도록 다른 특성의 변경할 수 있습니다. 이러한 문 특성에 대 한 자세한 내용은 참조는 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명 합니다.  
  
 커서 유형 및 커서 특징을 모두 지정 하는 문 특성을 설정 하는 응용 프로그램의 응용 프로그램의 요구 사항을 충족 해당 드라이버에서 사용할 수 있는 가장 효율적인 방법이 되지 않는 커서를 실행 합니다.  
  
 문 특성의 암시적 설정은 드라이버에서 정의 된 제외 하 고 이러한 규칙을 따라야 합니다.  
  
-   정방향 전용 커서는 스크롤 가능한; SQL_ATTR_CURSOR_SCROLLABLE 정의 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다.  
  
-   Insensitive 커서는 업데이트할 수 없습니다 (및 따라서 자신의 동시성은 읽기 전용); 이 해당 정의 ISO sql 표준 insensitive 커서의 기반으로 합니다.  
  
 따라서 문 특성의 암시적 설정에는 다음 표에 설명 하는 경우 발생 합니다.  
  
|특성을 설정 하는 응용 프로그램|암시적으로 설정 하는 다른 특성|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE로 합니다.|  
|SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES에 SQL_ATTR_CONCURRENCY|SQL_ATTR_CURSOR_SENSITIVITY를 SQL_UNSPECIFIED 또는 드라이버에 의해 정의 된 대로 SQL_SENSITIVE, 합니다. 되지 설정할 수 있습니다, SQL_INSENSITIVE로 insensitive 커서는 항상 읽기 전용입니다.|  
|SQL_ATTR_CURSOR_SCROLLABLE을 SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE을 SQL_SCROLLABLE|SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN, 또는 드라이버에 의해 지정 된 대로 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE 합니다. SQL_CURSOR_FORWARD_ONLY로는 설정 되지 됩니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE로|SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY 합니다.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC 하 합니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY를 SQL_SENSITIVE로|SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES 드라이버에 의해 지정 된 대로 SQL_ATTR_CONCURRENCY 합니다. SQL_CONCUR_READ_ONLY로는 설정 되지 됩니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN, 또는 드라이버에 의해 지정 된 대로 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY를 SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, 또는 드라이버에 의해 지정 된 대로 SQL_CONCUR_VALUES 합니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN, 또는 드라이버에 의해 지정 된 대로 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_DYNAMIC|Sql_scrollable SQL_ATTR_SCROLLABLE 합니다.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY를 SQL_SENSITIVE 합니다. (하지만 SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY과 같지 않은 경우에 합니다. 업데이트할 수 있는 동적 커서는 항상 자체의 트랜잭션을에서 이루어진 변경 내용에 민감합니다.)|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE을 SQL_NONSCROLLABLE 합니다.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN|Sql_scrollable SQL_ATTR_SCROLLABLE 합니다.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 또는 SQL_SENSITIVE (기준에 따라 드라이버에서 정의한 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 아닌 경우).|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC|Sql_scrollable SQL_ATTR_SCROLLABLE 합니다.<br /><br /> (SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 경우) SQL_INSENSITIVE로 SQL_ATTR_SENSITIVITY 합니다.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 또는 SQL_SENSITIVE (SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 아닌 경우).|
