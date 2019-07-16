---
title: 커서 특징 및 커서 유형 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8803e7827102f564be63454b0387df938064d84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002048"
---
# <a name="cursor-characteristics-and-cursor-type"></a>커서 특징 및 커서 형식
응용 프로그램 (정방향 전용, 정적, 키 집합 커서 또는 동적) 커서 유형을 지정 하는 대신 커서의 특징을 지정할 수 있습니다. 이렇게 하려면 응용 프로그램 선택 (SQL_ATTR_CURSOR_SCROLLABLE 문 특성 설정) 하 여 커서의 스크롤 가능 여부 및 민감도 (으로 SQL_ATTR_CURSOR_SENSITIVITY 문 특성 설정) 문에서 커서를 열기 전에 핸들입니다. 드라이버는 다음는 특징을 가장 효율적으로 제공 하는 커서 유형을 요청한 응용 프로그램을 선택 합니다.  
  
 응용 프로그램이 SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY를 SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY 문 특성 중 하나에 설정 될 때마다 드라이버에 게 필요한 모든 변경 내용을이 집합이 다른 문 특성 4 개의 특성을 해당 값을 일관 된 상태로 유지 되도록 합니다. 결과적으로, 응용 프로그램이 커서 특성을 지정 하는 경우 드라이버 특성을 변경할 수; 암시적 선택 내용에 따라 커서 유형을 나타내는 형식을 지정 하는 응용 프로그램을 드라이버 선택한 유형의 특성을 사용 하 여 일관 되도록 다른 특성을 변경할 수 있습니다. 이러한 문 특성에 대 한 자세한 내용은 참조는 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명 합니다.  
  
 커서 유형 및 커서 특징을 모두 지정 하는 문 특성을 설정 하는 응용 프로그램의 가장 효율적인 방법은 응용 프로그램의 요구 사항을 충족 하는 드라이버에서 사용할 수 없는 커서를 실행 합니다.  
  
 문 특성의 암시적 설정은 드라이버에서 정의 된 이러한 규칙을 따라야 한다는 점을 제외 하면:  
  
-   정방향 전용 커서는 스크롤 가능한; 없습니다. SQL_ATTR_CURSOR_SCROLLABLE에서의 정의 참조 하세요 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다.  
  
-   Insensitive 커서는 업데이트할 수 없습니다 (및 따라서 해당 동시성은 읽기 전용). 이 필드는 insensitive 커서 ISO sql 표준의 해당 정의 기반으로 계산 됩니다.  
  
 따라서 문 특성의 암시적 설정을 다음 표에서 설명 하는 경우에 발생 합니다.  
  
|특성을 설정 하는 응용 프로그램|암시적으로 설정 된 다른 특성|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY|Sql_insensitive SQL_ATTR_CURSOR_SENSITIVITY 합니다.|  
|SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES에 SQL_ATTR_CONCURRENCY|SQL_ATTR_CURSOR_SENSITIVITY를 SQL_UNSPECIFIED 또는 SQL_SENSITIVE, 드라이버에 의해 정의 된 대로 합니다. 되지 설정할 수 있습니다 sql_insensitive, insensitive 커서는 항상 읽기 전용입니다.|  
|SQL_ATTR_CURSOR_SCROLLABLE을 SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE을 SQL_SCROLLABLE|SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN, 또는 드라이버에 의해 지정 된 대로 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE 합니다. SQL_CURSOR_FORWARD_ONLY에 설정 되지 됩니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY sql_insensitive|SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY입니다.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC 하 합니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY를 sql_sensitive|SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES 드라이버에 의해 지정 된 대로 SQL_ATTR_CONCURRENCY를 제공 합니다. SQL_CONCUR_READ_ONLY에 설정 되지 됩니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN, 또는 드라이버에 의해 지정 된 대로 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY를 SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES 드라이버에 의해 지정 된 대로 합니다.<br /><br /> SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN, 또는 드라이버에 의해 지정 된 대로 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_DYNAMIC|Sql_scrollable SQL_ATTR_SCROLLABLE 합니다.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY를 SQL_SENSITIVE입니다. (하지만 SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY와 같지 않은 경우에 합니다. 업데이트할 수 있는 동적 커서는 항상 자체 트랜잭션에서 수행한 변경 내용에 민감합니다.)|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE을 SQL_NONSCROLLABLE입니다.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN|Sql_scrollable SQL_ATTR_SCROLLABLE 합니다.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 또는 SQL_SENSITIVE (조건에 따라 드라이버에서 정의 된, SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 없는 경우).|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC|Sql_scrollable SQL_ATTR_SCROLLABLE 합니다.<br /><br /> SQL_ATTR_SENSITIVITY sql_insensitive (SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 경우).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 또는 SQL_SENSITIVE (SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 아닌 경우).|
