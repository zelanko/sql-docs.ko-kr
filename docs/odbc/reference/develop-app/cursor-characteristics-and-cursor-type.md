---
title: 커서 특성 및 커서 유형 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002048"
---
# <a name="cursor-characteristics-and-cursor-type"></a>커서 특징 및 커서 형식
응용 프로그램은 커서 유형 (앞 으로만 이동 가능, 정적, 키 집합 또는 동적)을 지정 하는 대신 커서의 특성을 지정할 수 있습니다. 이 작업을 수행 하기 위해 응용 프로그램은 문에 커서를 열기 전에 SQL_ATTR_CURSOR_SCROLLABLE statement 특성) 및 민감도 (SQL_ATTR_CURSOR_SENSITIVITY 문 특성 설정)를 선택 하 여 커서의 스크롤 가능 여부을 선택 합니다. 처리. 그러면 드라이버가 응용 프로그램에서 요청한 특징을 가장 효율적으로 제공 하는 커서 유형을 선택 합니다.  
  
 응용 프로그램에서 문 특성 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY 또는 SQL_ATTR_CURSOR_TYPE를 설정할 때마다 드라이버는이 집합의 다른 문 특성에 대해 필요한 변경을 수행 합니다. 값이 일관 되 게 유지 되도록 네 가지 특성 결과적으로 응용 프로그램에서 커서 특징을 지정 하는 경우 드라이버는이 암시적 선택에 따라 커서 유형을 나타내는 특성을 변경할 수 있습니다. 응용 프로그램에서 형식을 지정 하는 경우 드라이버는 선택한 형식의 특성과 일치 하도록 다른 특성을 변경할 수 있습니다. 이러한 문 특성에 대 한 자세한 내용은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명을 참조 하세요.  
  
 문 특성을 설정 하 여 커서 유형과 커서 특성을 모두 지정 하는 응용 프로그램은 응용 프로그램의 요구 사항을 충족 하는 해당 드라이버에서 가장 효율적인 방법이 아닌 커서를 얻을 수 있는 위험을 실행 합니다.  
  
 문 특성의 암시적 설정은 다음 규칙을 따라야 한다는 점을 제외 하 고는 드라이버에서 정의 합니다.  
  
-   앞 으로만 이동 가능한 커서는 스크롤할 수 없습니다. [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)의 SQL_ATTR_CURSOR_SCROLLABLE 정의를 참조 하세요.  
  
-   구분 되지 않는 커서는 업데이트할 수 없으므로 동시성이 읽기 전용입니다. 이는 ISO SQL 표준에서 구분 되지 않은 커서의 정의를 기반으로 합니다.  
  
 따라서 문 특성의 암시적 설정은 다음 표에 설명 된 경우에 발생 합니다.  
  
|응용 프로그램에서 특성을로 설정 합니다.|암시적으로 설정 되는 기타 특성|  
|-----------------------------------|-------------------------------------|  
|SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY|SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY입니다.|  
|SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES에 SQL_ATTR_CONCURRENCY|드라이버에서 정의한 대로 SQL_UNSPECIFIED 또는 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY 합니다. 구분 하지 않는 커서는 항상 읽기 전용 이므로 SQL_INSENSITIVE로 설정할 수 없습니다.|  
|SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|SQL_CURSOR_FORWARD_ONLY SQL_ATTR_CURSOR_TYPE|  
|SQL_SCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE|드라이버에 지정 된 대로 SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC로 SQL_ATTR_CURSOR_TYPE 합니다. SQL_CURSOR_FORWARD_ONLY로 설정 되지 않습니다.|  
|SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY|SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY입니다.<br /><br /> SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE입니다.|  
|SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY|드라이버에 지정 된 대로 SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES로 SQL_ATTR_CONCURRENCY 합니다. SQL_CONCUR_READ_ONLY로 설정 되지 않습니다.<br /><br /> 드라이버에 지정 된 대로 SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC에 SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_UNSPECIFIED SQL_ATTR_CURSOR_SENSITIVITY|드라이버에 지정 된 대로 SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES에 SQL_ATTR_CONCURRENCY 합니다.<br /><br /> 드라이버에 지정 된 대로 SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC에 SQL_ATTR_CURSOR_TYPE 합니다.|  
|SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE|SQL_SCROLLABLE SQL_ATTR_SCROLLABLE입니다.<br /><br /> SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY입니다. SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY와 같지 않은 경우에만입니다. 업데이트 가능한 동적 커서는 항상 자체 트랜잭션에서 수행 된 변경 내용에 대해 중요 합니다.|  
|SQL_CURSOR_FORWARD_ONLY SQL_ATTR_CURSOR_TYPE|SQL_NONSCROLLABLE SQL_ATTR_CURSOR_SCROLLABLE입니다.|  
|SQL_CURSOR_KEYSET_DRIVEN SQL_ATTR_CURSOR_TYPE|SQL_SCROLLABLE SQL_ATTR_SCROLLABLE입니다.<br /><br /> SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 되지 않는 경우 드라이버 정의 기준에 따라 SQL_UNSPECIFIED 또는 SQL_SENSITIVE SQL_ATTR_SENSITIVITY 합니다.|  
|SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE|SQL_SCROLLABLE SQL_ATTR_SCROLLABLE입니다.<br /><br /> SQL_INSENSITIVE SQL_ATTR_SENSITIVITY (SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 경우).<br /><br /> SQL_UNSPECIFIED 또는 SQL_SENSITIVE SQL_ATTR_SENSITIVITY (SQL_ATTR_CONCURRENCY이 SQL_CONCUR_READ_ONLY 되지 않은 경우).|
