---
title: 드라이버 관리자 됩니까 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f29a40db8b35b5915de1889996e7953b1a8ad3f8
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794079"
---
# <a name="what-the-driver-manager-does"></a>드라이버 관리자가 수행하는 작업
다음 표에서 어떻게 ODBC *3.x* 드라이버 관리자는 odbc 호출을 매핑합니다 *2.x* 및 ODBC *3.x* 드라이버입니다.  
  
|함수 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|사용 하는 책갈피를 가리키는 **SQLFetchScroll**합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 설정이 ODBC *2.x* ODBC 드라이버 *3.x* 드라이버 관리자에서 캐시 합니다. 포인터를 역참조 하 고 ODBC 값 전달 *2.x* 드라이버에는 *FetchOffset* 인수의 **SQLExtendedFetch** 때 **SQLFetchScroll**  나중에 응용 프로그램에서 호출 됩니다.<br />-응용 프로그램 설정이 ODBC *3.x* ODBC 드라이버 *3.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.|  
|SQL_ATTR_ROW_STATUS_PTR|행 상태 배열 가리키는 채울 **SQLFetch**, **SQLFetchScroll**를 **SQLBulkOperations**, 및 **SQLSetPos**합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 설정이 ODBC *2.x* ODBC 드라이버 *3.x* 드라이버 관리자는 해당 값을 캐시 합니다. ODBC에이 값 전달 *2.x* 드라이버에는 *RowStatusArray* 인수의 **SQLExtendedFetch** 때 **SQLFetchScroll** 또는 **SQLFetch** 라고 합니다.<br />-응용 프로그램 설정이 ODBC *3.x* ODBC 드라이버 *3.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.<br />상태 S6, 응용 프로그램 SQL_ATTR_ROW_STATUS_PTR을 설정 하 고 호출 하는 경우 옵트인 **SQLBulkOperations** (사용 하 여는 *작업이* SQL_ADD의) 또는 **SQLSetPos** 첫 번째 호출 하지 않고 **SQLFetch** 하거나 **SQLFetchScroll**, SQLSTATE HY011 (특성 지금 설정할 수 없습니다)이 반환 됩니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|버퍼를 가리키는 **SQLFetch** 하 고 **SQLFetchScroll** 인출 된 행 수를 반환 합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 설정이 ODBC *2.x* ODBC 드라이버 *3.x* 드라이버 관리자는 해당 값을 캐시 합니다. ODBC에이 값 전달 *2.x* 드라이버에는 *RowCountPtr* 인수의 **SQLExtendedFetch** 때 **SQLFetch** 또는 **SQLFetchScroll** 응용 프로그램에서 호출 됩니다.<br />-응용 프로그램 설정이 ODBC *3.x* ODBC 드라이버 *3.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 설정이 ODBC *2.x* ODBC 드라이버 *3.x* 드라이버 관리자 SQL_ROWSET_SIZE 문 특성에 매핑합니다.<br />-응용 프로그램 설정이 ODBC *3.x* ODBC 드라이버 *3.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.<br />-때 ODBC를 사용 하 여 작업 하는 응용 프로그램 *3.x* 드라이버 호출 **SQLSetScrollOptions**, SQL_ROWSET_SIZE 값으로 설정 됩니다는 *RowsetSize* 인수 하는 경우 기본 드라이버 지원 하지 않습니다 **SQLSetScrollOptions**합니다.|  
|SQL_ROWSET_SIZE|사용 되는 행 집합 크기 설정 **SQLExtendedFetch** 때 **SQLExtendedFetch** ODBC 호출한 *2.x* 응용 프로그램입니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 설정이 ODBC *3.x* 드라이버 관리자, 드라이버 버전에 관계 없이 드라이버에 대 한 호출을 전달 합니다.<br />-때 ODBC를 사용 하 여 작업 하는 응용 프로그램 *2.x* 드라이버 호출 **SQLSetScrollOptions**, SQL_ROWSET_SIZE 값으로 설정 됩니다는 **RowsetSize** 인수입니다.|  
|**SQLBulkOperations**|삽입 작업이 나 업데이트, 삭제 또는 책갈피 작업 하는 페치를 수행합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 호출 **SQLBulkOperations** 사용 하 여는 *작업이* ODBC에 SQL_ADD의 *2.x* ODBC 드라이버 *3.x* 드라이버 관리자 매핑합니다 **SQLSetPos** 사용 하 여는 *작업* SQL_ADD입니다.<br />-ODBC를 사용 하 여 작업할 때 *2.x* 드라이버를 지원 하지 않는 **SQLSetPos** 사용 하 여는 *작업이* SQL_ADD, ODBC의 *3.x* 드라이버 Manager 매핑되지 **SQLSetPos** 사용 하 여는 *작업이* 에 SQL_ADD의 **SQLBulkOperations** 사용 하 여는 *작업* sql 추가 (_A). 왜냐하면 **SQLBulkOperations** S7에서는 상태에는 ODBC에서 호출할 수 없습니다 *2.x* 가 있는 유일한 상태 이기 때문 **SQLSetPos** 호출할 수 있습니다.<br />-응용 프로그램을 호출 하는 경우 **SQLBulkOperations** 사용 하 여는 *작업이* 의 ODBC에 SQL_ADD *2.x* 호출 하기 전에 드라이버 **SQLFetchScroll**, ODBC *3.x* 드라이버 관리자 오류를 반환 합니다.|  
|**SQLExtendedFetch**|지정 된 행 집합을 반환 합니다. 앞서 언급 한 제한 ODBC 제외 하 고 *3.x* 드라이버 관리자에 대 한 호출을 전달 **SQLExtendedFetch** 드라이버, 드라이버 버전에 관계 없이 합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 호출 **SQLFetch** 는 ODBC의 *2.x* ODBC 드라이버 *3.x* 드라이버 관리자 매핑합니다 **SQLExtendedFetch**합니다. 합니다 *FetchOrientation* 인수의 **SQLExtendedFetch** SQL_FETCH_NEXT로 설정 됩니다. 드라이버 관리자 SQL_ATTR_ROW_STATUS_PTR 문 특성에 대 한 캐시 된 값을 사용 합니다 *RowStatusArray* 인수와 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 대 한 캐시 된 값을  *RowCountPtr* 인수입니다.<br />-ODBC *3.x* 응용 프로그램에 대 한 호출을 혼합할 수 있습니다 **SQLFetch** 하 고 **SQLFetchScroll** ODBC에서 *2.x* 드라이버 때문에 ODBC *3.x* 드라이버 관리자 매핑합니다 **SQLFetch** 하 **SQLExtendedFetch** 때 응용 프로그램에서에서 호출 ODBC *2.x* 드라이버입니다.<br />-경우 ODBC *2.x* 드라이버를 지원 하지 않습니다 **SQLExtendedFetch**, ODBC *3.x* 드라이버 관리자 매핑되지 **SQLFetch** 또는 **SQLFetchScroll** 하 **SQLExtendedFetch** 응용 프로그램이 해당 드라이버의 것으로 호출 되는 경우. 응용 프로그램에서 SQLSTATE HYC00 1 보다 큰 값으로 SQL_ATTR_ROW_ARRAY_SIZE를 설정 하려고 하는 경우 (선택적 기능이 구현 되지 않음)이 반환 됩니다.<br />-제외 하 고 제한에 대 한는 앞서 언급 한 ODBC *3.x* 드라이버 관리자에 대 한 호출을 전달 **SQLFetch** 드라이버, 드라이버 버전에 관계 없이 합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 호출 **SQLFetchScroll** 는 ODBC의 *2.x* ODBC 드라이버 *3.x* 드라이버 관리자 매핑합니다 **SQLExtendedFetch**합니다. SQL_ATTR_ROW_STATUS_PTR 문 특성에 대 한 캐시 된 값을 사용 합니다 *RowStatusArray* 인수와 SQL_ATTR_ROWS_FETCHED_PTR 문 특성에 대 한 캐시 된 값을 *RowCountPtr* 인수입니다. 경우는 *FetchOrientation* 에서 인수 **SQLFetchScroll** SQL_FETCH_BOOKMARK는 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성에 대 한 캐시 된 값을 사용 합니다 *FetchOffset*  인수 오류를 반환 하 고는 *FetchOffset* 인수의 **SQLFetchScroll** 는 0이 아닌 합니다.<br />응용 프로그램에서 ODBC이으로 호출 되는- *3.x* ODBC 드라이버 *3.x* 드라이버 관리자 드라이버에 대 한 호출을 전달 합니다.|  
|**SQLSetPos**|다양 한 배치 작업을 수행합니다. ODBC *3.x* 드라이버 관리자에 대 한 호출을 전달 **SQLSetPos** 드라이버, 드라이버 버전에 관계 없이 합니다.|  
|**SQLSetScrollOptions**|때 드라이버 관리자 매핑합니다 **SQLSetScrollOptions** ODBC를 사용 하 여 작업 하는 응용 프로그램에 대 한 *3.x* 지원 하지 않는 드라이버 **SQLSetScrollOptions**, 드라이버 관리자에 not SQL_ATTR_ROW_ARRAY_SIZE 문 특성 SQL_ROWSET_SIZE 문 옵션을 설정 합니다는 *RowsetSize* 에서 인수 **SQLSetScrollOption**합니다. 따라서 **SQLSetScrollOptions** 를 호출 하 여 여러 행을 인출할 때 응용 프로그램에서 사용할 수 없습니다 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 호출 하 여 행을 가져오는 여러 경우에 사용할 수 있습니다 **SQLExtendedFetch**합니다.|
