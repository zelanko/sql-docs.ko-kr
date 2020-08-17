---
description: 드라이버 관리자가 수행하는 작업
title: 드라이버 관리자의 기능 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 399dec39e18c9e31ce4a93172d0597c333fb40cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386169"
---
# <a name="what-the-driver-manager-does"></a>드라이버 관리자가 수행하는 작업
다음 표에는 ODBC *2.X 드라이버 관리자에서 odbc 2.x* 및 odbc *3.x 드라이버에* 대 *한 호출* 을 매핑하는 방법이 요약 되어 있습니다.  
  
|함수 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|**Sqlfetchscroll**에 사용할 책갈피를 가리킵니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x *드라이버에서* 이를 설정 하면 odbc *3.x 드라이버 관리자* 가이를 캐시 합니다. 응용 프로그램에서 **Sqlextendedfetch** 이 호출 될 때 포인터를 역참조 하 고 **Sqlextendedfetch** 의 *FETCHOFFSET* 인수에 *있는 ODBC 2.x* 드라이버에 값을 전달 합니다.<br />-응용 프로그램이 ODBC 3.x 드라이버에서이를 설정 하는 경우 ODBC *3.X 드라이버 관리자* 는 드라이버에 대 한 호출을 전달 *합니다.*|  
|SQL_ATTR_ROW_STATUS_PTR|**Sqlfetch**, **sqlfetchscroll**, **SQLBulkOperations**및 **SQLSetPos**로 채워진 행 상태 배열을 가리킵니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x 드라이버에서이를 설정 하면 ODBC *3.X 드라이버 관리자* 가 해당 값을 캐시 *합니다.* **Sqlextendedfetch** 또는 **sqlfetch** 가 호출 될 때 **Sqlextendedfetch** 의 *ROWSTATUSARRAY* 인수에서이 값 *을 ODBC 2.x* 드라이버에 전달 합니다.<br />-응용 프로그램이 ODBC 3.x 드라이버에서이를 설정 하는 경우 ODBC *3.X 드라이버 관리자* 는 드라이버에 대 한 호출을 전달 *합니다.*<br />-상태 S6 응용 프로그램이 SQL_ATTR_ROW_STATUS_PTR를 설정한 다음 먼저 **Sqlfetch** 또는 **sqlfetchscroll**을 호출 하지 않고 **SQLBulkOperations** (SQL_ADD *작업* 을 사용 하 여) 또는 **SQLSetPos** 를 호출한 후에는 SQLSTATE HY011 (특성을 지금 설정할 수 없음)이 반환 됩니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|**Sqlfetch** 및 **sqlfetchscroll** 이 인출 된 행 수를 반환 하는 버퍼를 가리킵니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x 드라이버에서이를 설정 하면 ODBC *3.X 드라이버 관리자* 가 해당 값을 캐시 *합니다.* 응용 프로그램에서 **sqlfetch** 또는 **sqlextendedfetch** 을 호출할 때 **Sqlextendedfetch** 의 *rowcountptr* 인수에이 값을 전달 *합니다.*<br />-응용 프로그램이 ODBC 3.x 드라이버에서이를 설정 하는 경우 ODBC *3.X 드라이버 관리자* 는 드라이버에 대 한 호출을 전달 *합니다.*|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x 드라이버에서이를 설정 하는 경우 ODBC *3.X 드라이버 관리자* 는이를 SQL_ROWSET_SIZE statement 특성에 *매핑합니다.*<br />-응용 프로그램이 ODBC 3.x 드라이버에서이를 설정 하는 경우 ODBC *3.X 드라이버 관리자* 는 드라이버에 대 한 호출을 전달 *합니다.*<br />- *ODBC 3.x* 드라이버를 사용 하 여 작업 하는 응용 프로그램에서 **SQLSetScrollOptions**를 호출 하면 기본 드라이버가 **SQLSetScrollOptions**를 지원 하지 않는 경우 SQL_ROWSET_SIZE가 *RowsetSize* 인수의 값으로 설정 됩니다.|  
|SQL_ROWSET_SIZE|**Sqlextendedfetch** *가 ODBC 2.x* 응용 프로그램에 의해 호출 될 때 **sqlextendedfetch** 에서 사용 되는 행 집합 크기를 설정 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램에서이를 설정 *하면 ODBC 3.X* 드라이버 관리자는 드라이버 버전에 관계 없이 드라이버에 대 한 호출을 전달 합니다.<br />-ODBC *2.x 드라이버를* 사용 하 여 작업 하는 응용 프로그램에서 **SQLSetScrollOptions**를 호출 하는 경우 SQL_ROWSET_SIZE는 **RowsetSize** 인수의 값으로 설정 됩니다.|  
|**SQLBulkOperations**|책갈피 작업을 통해 삽입 작업, 업데이트, 삭제 또는 페치를 수행 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x 드라이버에서 SQL_ADD *작업* 을 사용 하 여 **SQLBulkOperations** 를 호출 하는 경우 odbc *3.X 드라이버 관리자* 는 SQL_ADD *작업* 을 사용 하 여이를 **SQLSetPos** 에 *매핑합니다.*<br />-SQL_ADD *작업* 을 사용 하 여 **sqlsetpos** 를 지원 하지 않는 odbc 2.x 드라이버를 사용 하는 경우 odbc *3.X 드라이버 관리자* 는 SQL_ADD *작업* 을 사용 하 여 **sqlsetpos** 를 SQL_ADD *작업* 으로 **SQLBulkOperations** 에 매핑하지 *않습니다.* 이는 **SQLBulkOperations** 를 상태 S7에서 호출할 수 없기 때문입니다 *.* 이는 ODBC 2.x가 **SQLSetPos** 를 호출할 수 있는 유일한 상태 였습니다.<br />- **Sqlfetchscroll**을 호출 하기 전에 응용 프로그램이 odbc 2.x 드라이버에서 SQL_ADD *작업* 을 사용 하 여 **SQLBulkOperations** 를 호출 하는 경우 *odbc* *3.x 드라이버 관리자* 에서 오류를 반환 합니다.|  
|**SQLExtendedFetch**|지정 된 행 집합을 반환 합니다. 앞서 언급 한 제한 사항을 제외 하 *고 ODBC 3.X* 드라이버 관리자는 드라이버 버전에 관계 없이 **sqlextendedfetch** 에 대 한 호출을 드라이버로 전달 합니다.|  
|**SQLFetch**|다음 행 집합을 반환 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x *드라이버에서* **sqlfetch** 를 호출 하면 odbc *3.x 드라이버 관리자* 는이를 **sqlextendedfetch**에 매핑합니다. **Sqlextendedfetch** 의 *fetchorientation* 인수가 SQL_FETCH_NEXT로 설정 되어 있습니다. 드라이버 관리자는 *Rowstatusarray* 인수에 SQL_ATTR_ROW_STATUS_PTR statement 특성의 캐시 된 값을 사용 하 고 *rowstatusarray* 인수에 대 한 SQL_ATTR_ROWS_FETCHED_PTR statement 특성의 캐시 된 값을 사용 합니다.<br />- *Odbc 2.x 응용 프로그램* 은 odbc *2.x 드라이버* **에서 Sqlfetch 및** **sqlfetchscroll** 에 대 한 호출을 혼합할 수 있습니다. odbc 2.x *드라이버 관리자* 는 응용 *프로그램이 odbc 2.x* 드라이버에서 호출 하는 경우 **sqlextendedfetch** 에 **sqlfetch** 를 매핑합니다.<br />-ODBC 2.x 드라이버가 **Sqlextendedfetch**를 지원 하지 않는 경우 odbc *3.x 드라이버 관리자* 는 **Sqlfetch** 또는 **sqlextendedfetch** 을 응용 프로그램이 해당 드라이버에서 호출할 때 **sqlextendedfetch** 에 매핑하지 *않습니다.* 응용 프로그램에서 SQL_ATTR_ROW_ARRAY_SIZE 값을 1 보다 큰 값으로 설정 하려고 하면 SQLSTATE HYC00 (선택적 기능이 구현 되지 않음)가 반환 됩니다.<br />-위에서 설명한 제한 사항을 제외 하 고 *, ODBC 3.X* 드라이버 관리자는 드라이버 버전에 관계 없이 **sqlfetch** 호출을 드라이버로 전달 합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 프로그램이 ODBC 2.x 드라이버에서 **Sqlfetchscroll** 을 호출 하는 *경우 Odbc* *3.x 드라이버 관리자* 는이를 **sqlfetchscroll**에 매핑합니다. *Rowstatusarray* 인수에 SQL_ATTR_ROW_STATUS_PTR statement 특성의 캐시 된 값을 사용 하 고 *rowstatusarray* 인수에 대 한 SQL_ATTR_ROWS_FETCHED_PTR statement 특성의 캐시 된 값을 사용 합니다. **Sqlfetchscroll** 의 *fetchorientation* 인수가 SQL_FETCH_BOOKMARK 이면 *fetchorientation* 인수에 대해 SQL_ATTR_FETCH_BOOKMARK_PTR statement 특성의 캐시 된 값을 사용 하 고 **sqlfetchscroll** 의 *fetchorientation* 인수가 0이 아닌 경우 오류를 반환 합니다.<br />-응용 프로그램이 ODBC 3.x 드라이버에서이를 호출 하는 경우 ODBC *3.X 드라이버 관리자* 는 드라이버에 대 한 호출을 전달 *합니다.*|  
|**SQLSetPos**|다양 한 위치 지정 작업을 수행 합니다. ODBC 3.x 드라이버 관리자는 드라이버 버전에 관계 없이 **SQLSetPos** 호출을 드라이버로 전달 *합니다.*|  
|**SQLSetScrollOptions**|드라이버 관리자가 **SQLSetScrollOptions**을 지원 하지 *않는 ODBC 2.x* 드라이버를 사용 하 여 작동 하는 응용 프로그램에 대해 **SQLSetScrollOptions** 를 매핑하는 경우 드라이버 관리자는 SQL_ATTR_ROW_ARRAY_SIZE statement 특성이 아닌 SQL_ROWSET_SIZE 문 옵션을 **SQLSetScrollOption**의 *RowsetSize* 인수로 설정 합니다. 결과적으로 **Sqlfetch** 또는 **sqlfetchscroll**을 호출 하 여 여러 행을 인출 하는 경우 응용 프로그램에서 **SQLSetScrollOptions** 를 사용할 수 없습니다. **Sqlextendedfetch**를 호출 하 여 여러 행을 인출 하는 경우에만 사용할 수 있습니다.|
