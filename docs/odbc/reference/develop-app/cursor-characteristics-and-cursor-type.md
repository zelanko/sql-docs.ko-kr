---
title: 커서 특성 및 커서 유형 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8354fdabf6830780ec2d128492c86cc1edd582ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301630"
---
# <a name="cursor-characteristics-and-cursor-type"></a>커서 특징 및 커서 형식
응용 프로그램은 커서 유형(정방향 전용, 정적, 키 집합 기반 또는 동적)을 지정하는 대신 커서의 특성을 지정할 수 있습니다. 이렇게 하려면 응용 프로그램은 명령문 핸들에서 커서를 열기 전에 커서의 스크롤 가능성(SQL_ATTR_CURSOR_SCROLLABLE 문 특성설정) 및 민감도(SQL_ATTR_CURSOR_SENSITIVITY 문 특성설정)를 선택합니다. 그런 다음 드라이버는 응용 프로그램에서 요청한 특성을 가장 효율적으로 제공하는 커서 유형을 선택합니다.  
  
 응용 프로그램에서 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY 또는 SQL_ATTR_CURSOR_TYPE 문 특성을 설정할 때마다 드라이버는 값이 일관되게 유지되도록 이 네 가지 특성 집합의 다른 문 특성을 변경합니다. 결과적으로 응용 프로그램이 커서 특성을 지정하면 드라이버는 이 암시적 선택을 기반으로 커서 유형을 나타내는 특성을 변경할 수 있습니다. 응용 프로그램이 형식을 지정하면 드라이버는 선택한 형식의 특성과 일치하도록 다른 특성을 변경할 수 있습니다. 이러한 문 특성에 대한 자세한 내용은 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 함수 설명을 참조하십시오.  
  
 명령문 특성을 설정하여 커서 유형과 커서 특성을 모두 지정하는 응용 프로그램은 응용 프로그램의 요구 사항을 충족하는 해당 드라이버에서 사용할 수 있는 가장 효율적인 방법이 아닌 커서를 얻을 위험이 있습니다.  
  
 문 특성의 암시적 설정은 다음 규칙을 따라야 한다는 점을 제외하면 드라이버 정의됩니다.  
  
-   정방향 전용 커서는 스크롤할 수 없습니다. [SQLSetStmtAttr에서](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)SQL_ATTR_CURSOR_SCROLLABLE 정의 참조 .  
  
-   민감하지 않은 커서는 절대 로데이터화되지 않으므로 동시성은 읽기 전용입니다. 이는 ISO SQL 표준에서 민감하지 않은 커서의 정의를 기반으로 합니다.  
  
 따라서 다음 표에 설명된 경우 문 특성의 암시적 설정이 발생합니다.  
  
|응용 프로그램 집합 특성은|암시적으로 설정된 다른 특성|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY to SQL_CONCUR_READ_ONLY|SQL_INSENSITIVE SQL_ATTR_CURSOR_SENSITIVITY.|  
|SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY|드라이버가 정의한 대로 SQL_UNSPECIFIED 또는 SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY. 민감하지 않은 커서는 항상 읽기 전용이므로 SQL_INSENSITIVE 설정할 수 없습니다.|  
|SQL_ATTR_CURSOR_SCROLLABLE to SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE to SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE to SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE 드라이버가 지정한 대로 SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC. SQL_CURSOR_FORWARD_ONLY 설정되지 않습니다.|  
|SQL_ATTR_CURSOR_SENSITIVITY to SQL_INSENSITIVE|SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY.<br /><br /> SQL_CURSOR_STATIC SQL_ATTR_CURSOR_TYPE.|  
|SQL_ATTR_CURSOR_SENSITIVITY to SQL_SENSITIVE|드라이버가 지정한 대로 SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY. 그것은 SQL_CONCUR_READ_ONLY 설정되지 않습니다.<br /><br /> 드라이버가 지정한 대로 SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE.|  
|SQL_ATTR_CURSOR_SENSITIVITY to SQL_UNSPECIFIED|드라이버가 지정한 대로 SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY.<br /><br /> 드라이버가 지정한 대로 SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN 또는 SQL_CURSOR_DYNAMIC SQL_ATTR_CURSOR_TYPE.|  
|SQL_ATTR_CURSOR_TYPE to SQL_CURSOR_DYNAMIC|SQL_SCROLLABLE SQL_ATTR_SCROLLABLE.<br /><br /> SQL_SENSITIVE SQL_ATTR_CURSOR_SENSITIVITY. (그러나 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 동일하지 않은 경우에만. 업데이터 동적 커서는 항상 자체 트랜잭션에서 변경된 변경 사항에 민감합니다.|  
|SQL_ATTR_CURSOR_TYPE to SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE to SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE to SQL_CURSOR_KEYSET_DRIVEN|SQL_SCROLLABLE SQL_ATTR_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 또는 SQL_SENSITIVE(드라이버 정의 기준에 따라 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 않은 경우).|  
|SQL_ATTR_CURSOR_TYPE to SQL_CURSOR_STATIC|SQL_SCROLLABLE SQL_ATTR_SCROLLABLE.<br /><br /> SQL_INSENSITIVE SQL_ATTR_SENSITIVITY(SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 경우).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED 또는 SQL_SENSITIVE (SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 않은 경우).|
