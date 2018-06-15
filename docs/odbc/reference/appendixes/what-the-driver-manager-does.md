---
title: 드라이버 관리자 않음 | Microsoft Docs
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
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 194bf496314c89bca72cbb650226db5222651c4b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914238"
---
# <a name="what-the-driver-manager-does"></a>드라이버 관리자에서 수행 하는 작업
다음 표에서 요약 방식을 ODBC 3 *.x* 드라이버 관리자 ODBC 2에 대 한 호출을 매핑합니다. *x* 고 ODBC 3 *.x* 드라이버입니다.  
  
|함수 또는<br /><br /> 문 특성|설명|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|사용 하면 책갈피를 가리키는 **SQLFetchScroll**합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 설정이 ODBC 2. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자에서 캐시 합니다. 포인터를 역참조 하 고 ODBC 2에는 값을 전달 합니다. *x* 에서 드라이버는 *FetchOffset* 의 인수 **SQLExtendedFetch** 때 **SQLFetchScroll** 나중에 응용 프로그램에 의해 호출 됩니다.<br />-응용 프로그램에서 설정이 ODBC 3에서 *.x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.|  
|SQL_ATTR_ROW_STATUS_PTR을|행 상태 배열이 가리키는로 채워진 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, 및 **SQLSetPos**합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 설정이 ODBC 2. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자는 해당 값을 캐시 합니다. ODBC 2이 값이 전달 됩니다. *x* 에서 드라이버는 *RowStatusArray* 의 인수 **SQLExtendedFetch** 때 **SQLFetchScroll** 또는 **SQLFetch** 라고 합니다.<br />-응용 프로그램에서 설정이 ODBC 3에서 *.x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.<br />상태 S6, 응용 프로그램이 SQL_ATTR_ROW_STATUS_PTR을 설정 하는 다음 호출 하는 경우 옵트인 **SQLBulkOperations** (으로 *작업* SQL_ADD의) 또는 **SQLSetPos** 먼저 호출 하지 않고 **SQLFetch** 또는 **SQLFetchScroll**, SQLSTATE HY011 (특성 지금 설정할 수 없습니다)이 반환 됩니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|버퍼를 가리키는 **SQLFetch** 및 **SQLFetchScroll** 인출 된 행 수를 반환 합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 설정이 ODBC 2. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자는 해당 값을 캐시 합니다. ODBC 2이 값이 전달 됩니다. *x* 에서 드라이버는 *RowCountPtr* 의 인수 **SQLExtendedFetch** 때 **SQLFetch** 또는 **SQLFetchScroll** 응용 프로그램에 의해 호출 됩니다.<br />-응용 프로그램에서 설정이 ODBC 3에서 *.x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 설정이 ODBC 2. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 SQL_ROWSET_SIZE 문 특성에 매핑합니다.<br />-응용 프로그램에서 설정이 ODBC 3에서 *.x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.<br />-때 ODBC 3을 사용 하는 응용 프로그램 *.x* 드라이버 호출 **SQLSetScrollOptions**, SQL_ROWSET_SIZE에 값으로 설정 되는 *RowsetSize* 인수 하는 경우 내부 드라이버가 지원 하지 않으면 **SQLSetScrollOptions**합니다.|  
|SQL_ROWSET_SIZE|사용 하는 행 집합 크기 설정 **SQLExtendedFetch** 때 **SQLExtendedFetch** 는 ODBC 2에 의해 호출 됩니다 *.x* 응용 프로그램입니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 설정, ODBC 3 *.x* 드라이버 관리자 드라이버 버전에 관계 없이 드라이버에 대 한 호출을 전달 합니다.<br />-때 ODBC 2를 사용 하는 응용 프로그램입니다. *x* 드라이버 호출 **SQLSetScrollOptions**, SQL_ROWSET_SIZE에 값으로 설정 되는 **RowsetSize** 인수입니다.|  
|**SQLBulkOperations**|Insert 작업 또는 update, delete 또는 책갈피 작업에 의해 인출 수행합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 호출 경우 **SQLBulkOperations** 와 *작업* ODBC 2에 SQL_ADD의. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 매핑합니다 **SQLSetPos** 와 *작업* SQL_ADD의 합니다.<br />-는 ODBC 2 작업할 때. *x* 지원 하지 않는 드라이버 **SQLSetPos** 와 *작업* SQL_ADD, ODBC 3의 *.x* 드라이버 관리자 매핑되지않는**SQLSetPos** 와 *작업* 에 SQL_ADD의 **SQLBulkOperations** 와 *작업* SQL_ADD의 합니다. 때문에 이것이 **SQLBulkOperations** 상태 S7에 ODBC 2에서에서 호출할 수 없습니다. *x* 는 않은 유일한 상태가 **SQLSetPos** 호출할 수 있습니다.<br />-응용 프로그램을 호출 하는 경우 **SQLBulkOperations** 와 *작업* 의 SQL_ADD ODBC 2에서. *x* 호출 하기 전에 드라이버 **SQLFetchScroll**, ODBC 3 *.x* 드라이버 관리자에서 오류를 반환 합니다.|  
|**SQLExtendedFetch**|지정 된 행 집합을 반환 합니다. 앞서 언급 한 제한 ODBC 3 제외한 *.x* 드라이버 관리자에 대 한 호출을 전달 **SQLExtendedFetch** 드라이버 버전에 관계 없이 드라이버에 있습니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 호출 경우 **SQLFetch** ODBC 2에서. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 매핑합니다 **SQLExtendedFetch**합니다. *FetchOrientation* 의 인수 **SQLExtendedFetch** SQL_FETCH_NEXT로 설정 됩니다. SQL_ATTR_ROW_STATUS_PTR 문 특성에 대 한 캐시 된 값을 사용 하 여 드라이버 관리자는 *RowStatusArray* 인수와 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 대 한 캐시 된 값은  *RowCountPtr* 인수입니다.<br />-ODBC 3 an *.x* 응용 프로그램에 대 한 호출을 혼합할 수 **SQLFetch** 및 **SQLFetchScroll** ODBC 2에서. *x* 드라이버 때문에 ODBC 3 *.x* 드라이버 관리자 매핑합니다 **SQLFetch** 를 **SQLExtendedFetch** 때 응용 프로그램에서 호출는 ODBC 2. *x* 드라이버입니다.<br />-경우에는 ODBC 2입니다. *x* 드라이버가 지원 하지 않으면 **SQLExtendedFetch**, ODBC 3 *.x* 드라이버 관리자를 매핑하지 않습니다 **SQLFetch** 또는  **SQLFetchScroll** 를 **SQLExtendedFetch** 응용 프로그램이 드라이버의 것으로 호출 되는 경우. 응용 프로그램 SQL_ATTR_ROW_ARRAY_SIZE SQLSTATE HYC00 1 보다 큰 값으로 설정 하려고 할 경우 (선택적 기능이 구현 되지 않았습니다)이 반환 됩니다.<br />-을 제외 하 고 앞서 언급 한 제한 ODBC 3 *.x* 드라이버 관리자에 대 한 호출을 전달 **SQLFetch** 드라이버 버전에 관계 없이 드라이버에 있습니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 호출 경우 **SQLFetchScroll** ODBC 2에서. *x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 매핑합니다 **SQLExtendedFetch**합니다. SQL_ATTR_ROW_STATUS_PTR 문 특성에 대 한 캐시 된 값을 사용 하 여는 *RowStatusArray* 인수와 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 대 한 캐시 된 값은 *RowCountPtr* 인수입니다. 경우는 *FetchOrientation* 인수 **SQLFetchScroll** SQL_FETCH_BOOKMARK은 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 대 한 캐시 된 값을 사용 하 여는 *FetchOffset*  인수 오류를 반환 하 고는 *FetchOffset* 의 인수 **SQLFetchScroll** 는 0이 아닌 합니다.<br />-응용 프로그램 호출 하는 경우이 ODBC 3에서 *.x* 드라이버에서 ODBC 3 *.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.|  
|**SQLSetPos**|다양 한 위치 지정된 작업을 수행합니다. ODBC 3 *.x* 드라이버 관리자에 대 한 호출을 전달 **SQLSetPos** 드라이버 버전에 관계 없이 드라이버에 있습니다.|  
|**SQLSetScrollOptions**|드라이버 관리자에 매핑합니다 **SQLSetScrollOptions** ODBC 3을 사용 하는 응용 프로그램에 대 한 *.x* 지원 하지 않는 드라이버 **SQLSetScrollOptions**, 드라이버 관리자 설정 SQL_ROWSET_SIZE 문 옵션 not SQL_ATTR_ROW_ARRAY_SIZE 문 특성에는 *RowsetSize* 인수 **SQLSetScrollOption**합니다. 결과적으로, **SQLSetScrollOptions** 를 호출 하 여 여러 행을 인출할 때 응용 프로그램에서 사용할 수 없습니다 **SQLFetch** 또는 **SQLFetchScroll**합니다. 호출 하 여 행을 가져오는 여러 경우에 사용할 수 있습니다 **SQLExtendedFetch**합니다.|
