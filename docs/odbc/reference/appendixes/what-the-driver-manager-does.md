---
title: 드라이버 관리자가 하는 일 | 마이크로 소프트 문서
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
ms.openlocfilehash: 07ab0784e6f6ad4487a02a179a5fa3be2617c930
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306564"
---
# <a name="what-the-driver-manager-does"></a>드라이버 관리자가 수행하는 작업
다음 표는 ODBC *3.x* 드라이버 관리자가 ODBC *2.x* 및 ODBC *3.x* 드라이버에 대한 호출을 매핑하는 방법을 요약합니다.  
  
|기능 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|**SQLFetchScroll와**함께 사용할 책갈피를 가리킵니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 이를 설정하면 ODBC *3.x* 드라이버 관리자가 이를 캐시합니다. SQLFetchScroll 나중에 응용 프로그램에서 호출 될 때 **SQLExtendedFetch의** *FetchOffset* 인수에서 ODBC *2.x* 드라이버에 값을 전달 **합니다.**<br />- 응용 프로그램이 ODBC *3.x* 드라이버에서 이 것을 설정하면 ODBC *3.x* 드라이버 관리자가 드라이버에 대한 호출을 전달합니다.|  
|SQL_ATTR_ROW_STATUS_PTR|**SQLFetch,** **SQLFetch스크롤,** **SQLBulkOperations**및 **SQLSetPos로**채워진 행 상태 배열을 가리킵니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 이 값을 설정하면 ODBC *3.x* 드라이버 관리자가 값을 캐시합니다. **SQLFetch스크롤** 또는 **SQLFetch가** 호출될 때 **SQLExtendedFetch의** *RowStatusArray* 인수에서 ODBC *2.x* 드라이버에 이 값을 전달합니다.<br />- 응용 프로그램이 ODBC *3.x* 드라이버에서 이 것을 설정하면 ODBC *3.x* 드라이버 관리자가 드라이버에 대한 호출을 전달합니다.<br />- 상태 S6에서 응용 프로그램이 SQL_ATTR_ROW_STATUS_PTR 설정한 다음 SQLBulkOperations (SQL_ADD *작업* 사용) 또는 **SQLSetPos를** 호출하지 않고 **SQLFetch** 또는 **SQLFetchScroll을**호출하지 않고 **SQLBulkOperations를** 호출하면 SQLSTATE HY011 (특성은 지금 설정할 수 없음)이 반환됩니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|**SQLFetch** 및 **SQLFetchScroll** 가져온 행 수를 반환 하는 버퍼를 가리킵니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 이 값을 설정하면 ODBC *3.x* 드라이버 관리자가 값을 캐시합니다. SQLFetch 또는 **SQLFetchScroll** 응용 프로그램에서 호출 될 때 **SQLExtendedFetch의** **SQLFetch** *RowCountPtr* 인수에서 ODBC *2.x* 드라이버에 이 값을 전달 합니다.<br />- 응용 프로그램이 ODBC *3.x* 드라이버에서 이 것을 설정하면 ODBC *3.x* 드라이버 관리자가 드라이버에 대한 호출을 전달합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 이를 설정하면 ODBC *3.x* 드라이버 관리자가 SQL_ROWSET_SIZE 명령문 특성에 매핑합니다.<br />- 응용 프로그램이 ODBC *3.x* 드라이버에서 이 것을 설정하면 ODBC *3.x* 드라이버 관리자가 드라이버에 대한 호출을 전달합니다.<br />- ODBC *3.x* 드라이버로 작업하는 응용 프로그램이 **SQLSetScrollOptions를**호출하는 경우 SQL_ROWSET_SIZE 기본 드라이버가 **SQLSetScrollOptions를**지원하지 않는 경우 *RowsetSize* 인수의 값으로 설정됩니다.|  
|SQL_ROWSET_SIZE|**SQLExtendedFetch는** ODBC *2.x* 응용 프로그램에서 호출될 때 **SQLExtendedFetch에서** 사용하는 행 집합 크기를 설정합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 이 것을 설정하면 ODBC *3.x* 드라이버 관리자는 드라이버 버전에 관계없이 드라이버에 대한 호출을 전달합니다.<br />- ODBC *2.x* 드라이버로 작업하는 응용 프로그램이 **SQLSetScrollOptions를**호출하면 SQL_ROWSET_SIZE **RowsetSize** 인수의 값으로 설정됩니다.|  
|**SQLBulk운영**|책갈피 작업을 수행하거나 책갈피 작업을 업데이트, 삭제 또는 가져옵니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 SQL_ADD *작업으로* **SQLBulkOperations를** 호출하면 ODBC *3.x* 드라이버 관리자는 SQL_ADD *작업을* 사용하여 **SQLSetPos에** 매핑합니다.<br />- SQL_ADD *작업으로* **SQLSetPos를** 지원하지 않는 ODBC *2.x* 드라이버로 작업하는 경우 ODBC *3.x* 드라이버 관리자는 SQL_ADD *작업으로* SQL_ADD *작업과* **SQLBulkOperations를** 매핑하지 않습니다. **SQLSetPos** 이는 **SQLBulkOperations가** ODBC *2.x에서* **SQLSetPos를** 호출할 수 있는 유일한 상태인 S7 상태에서 호출할 수 없기 때문입니다.<br />- 응용 프로그램이 **SQLFetchScroll를**호출하기 전에 ODBC *2.x* 드라이버에서 SQL_ADD *작업으로* **SQLBulkOperations를** 호출하는 경우 ODBC *3.x* 드라이버 관리자는 오류를 반환합니다.|  
|**SQLExtendedFetch**|지정된 행 집합을 반환합니다. 방금 언급한 제한을 제외하고 ODBC *3.x* 드라이버 관리자는 드라이버 버전에 관계없이 **SQLExtendedFetch호출을** 드라이버에 전달합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetch를** 호출하면 ODBC *3.x* 드라이버 관리자가 **SQLExtendedFetch**에 매핑합니다. **SQLExtendedFetch의** *FetchOrientation* 인수는 SQL_FETCH_NEXT 설정됩니다. 드라이버 관리자는 *RowStatusArray* 인수에 대한 SQL_ATTR_ROW_STATUS_PTR 문 특성의 캐시된 값과 *RowCountPtr* 인수에 대한 SQL_ATTR_ROWS_FETCHED_PTR 명령문 특성의 캐시된 값을 사용합니다.<br />- ODBC 3.x 응용 프로그램은 ODBC *3.x* 드라이버 관리자가 **SQLExtendedFetch에** **SQLFetch를** 매핑하기 때문에 **SQLExtendedFetch** ODBC *2.x* *2.x* 드라이버에서 SQLFetch 및 **SQLFetchScroll에** 대한 호출을 혼합할 수 있습니다. *3.x*<br />- ODBC *2.x* 드라이버가 **SQLExtendedFetch를**지원하지 않는 경우, ODBC *3.x* 드라이버 관리자는 응용 프로그램이 해당 드라이버에서 호출할 때 **SQLFetch** 또는 **SQLFetchScroll을** **SQLExtendedFetch에** 매핑하지 않습니다. 응용 프로그램이 SQL_ATTR_ROW_ARRAY_SIZE 1보다 큰 값으로 설정하려고 하면 SQLSTATE HYC00(구현되지 않은 선택적 기능)이 반환됩니다.<br />- 방금 언급한 제한 사항을 제외하고 ODBC *3.x* 드라이버 관리자는 드라이버 버전에 관계없이 **SQLFetch에** 대한 호출을 드라이버에 전달합니다.|  
|**SQLFetchScroll**|지정된 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetchScroll를** 호출하면 ODBC *3.x* 드라이버 관리자가 **SQLExtendedFetch에**매핑합니다. *RowStatusArray* 인수에 대 한 SQL_ATTR_ROW_STATUS_PTR 문 특성의 캐시 된 값 및 *RowCountPtr* 인수에 대 한 SQL_ATTR_ROWS_FETCHED_PTR 문 특성의 캐시 된 값을 사용 합니다. **SQLFetchScroll의** *FetchOrientation* 인수가 SQL_FETCH_BOOKMARK 경우 *FetchOffset* 인수에 대해 SQL_ATTR_FETCH_BOOKMARK_PTR 문 특성의 캐시된 값을 사용하고 **SQLFetchScroll의** *FetchOffset* 인수가 0이 아닌 경우 오류를 반환합니다.<br />- 응용 프로그램이 ODBC *3.x* 드라이버에서 이 것을 호출하면 ODBC *3.x* 드라이버 관리자가 드라이버에 호출을 전달합니다.|  
|**SQLSetPos**|다양한 위치 가있는 작업을 수행합니다. ODBC *3.x* 드라이버 관리자는 드라이버 버전에 관계없이 **SQLSetPos호출을** 드라이버에 전달합니다.|  
|**SQLSet스크롤 옵션**|드라이버 **관리자가 SQLSetScrollOptions를** 지원하지 않는 ODBC *3.x* 드라이버로 작업하는 응용 프로그램에 대해 **SQLSetScrollOptions를**매핑할 때 드라이버 관리자는 SQL_ATTR_ROW_ARRAY_SIZE 문 특성이 아닌 SQL_ROWSET_SIZE 명령문 옵션을 **SQLSetScrollOption의** *RowsetSize* 인수로 설정합니다. 따라서 SQLFetch스크롤 에 대한 호출로 여러 행을 가져올 때 응용 프로그램에서 **SQLFetchScroll** **SQLSetScroll 옵션을** 사용할 수 없습니다. **SQLFetch** **SQLExtendedFetch**에 대한 호출로 여러 행을 가져올 때만 사용할 수 있습니다.|
