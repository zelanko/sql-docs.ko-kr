---
title: ODBC 3.x에 대한 블록 및 스크롤 커서 호환성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c526eff6e19014c923f05ad91551a7d7c66f5294
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306344"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
**SQLFetchScroll** 및 **SQLExtendedFetch의** 존재는 응용 프로그램이 호출하는 함수 집합인 API(응용 프로그램 프로그래밍 인터페이스)와 드라이버가 구현하는 함수 집합인 SPI(서비스 공급자 인터페이스) 간의 ODBC에서 첫 번째 명확한 분할을 나타냅니다. 이 분할은 **SQLFetchScroll를**사용하는 ODBC *3.x의*요구 사항의 균형을 조정하여 표준에 맞추고 **SQLExtendedFetch를**사용하는 ODBC *2.x와*호환됩니다.  
  
 응용 프로그램에서 호출하는 함수 집합인 ODBC *3.x* API에는 **SQLFetchScroll** 및 관련 문 특성이 포함됩니다. 드라이버가 구현하는 함수 집합인 ODBC *3.x* SPI에는 **SQLFetch스크롤,** **SQLExtendedFetch**및 관련 문 특성이 포함됩니다. ODBC는 API와 SPI 간에 이 분할을 공식적으로 적용하지 않으므로 ODBC *3.x* 응용 프로그램에서 **SQLExtendedFetch** 및 관련 문 특성을 호출할 수 있습니다. 그러나 ODBC *3.x* 응용 프로그램에서 이 작업을 수행할 이유가 없습니다. API 및 SAPI에 대한 자세한 내용은 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)에 대한 소개를 참조하십시오.  
  
 ODBC *3.x* 드라이버 관리자가 ODBC *2.x* 및 ODBC *3.x* 드라이버에 대한 호출을 매핑하는 방법과 ODBC *3.x* 드라이버가 블록 및 스크롤 가능한 커서에 대해 구현해야 하는 기능 및 명령어에 대한 자세한 내용은 [부록](../../../odbc/reference/appendixes/what-the-driver-does.md) G: 이전 버전과의 호환성에 대한 드라이버 지침을 참조하십시오.  
  
 다음 표에는 ODBC *3.x* 응용 프로그램이 블록 및 스크롤 가능한 커서와 함께 사용해야 하는 함수 및 명령문 특성이 요약되어 있습니다. 또한 ODBC 3.x 응용 프로그램이 ODBC 2.x 드라이버와 호환되도록 알고 있어야 하는 이 영역에서 ODBC *2.x와* ODBC *3.x* 간의 변경 내용도 나열합니다. *3.x* *2.x*  
  
|기능 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|**SQLFetchScroll와**함께 사용할 책갈피를 가리킵니다.<br /><br /> 응용 프로그램이 ODBC *2.x* 드라이버에서 이 것을 설정하는 경우 고정 길이 책갈피를 가리킬 수 있어야 합니다.|  
|SQL_ATTR_ROW_STATUS_PTR|**SQLFetch,** **SQLFetch스크롤,** **SQLBulkOperations**및 **SQLSetPos로**채워진 행 상태 배열을 가리킵니다.<br /><br /> 응용 프로그램이 ODBC *2.x* 드라이버에서 이 것을 설정하고 **SQLFetch**, **SQLFetch**또는 **SQLExtendedFetch를**호출하기 전에 SQL_ADD *작업으로* **SQLBulkOperation을** 호출하면 SQLSTATE HY011 (특성은 지금 설정할 수 없음)이 반환됩니다.<br /><br /> 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetch를** 호출하면 **SQLFetch는** **SQLExtendedFetch에** 매핑되므로 이 배열의 값을 반환합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|**SQLFetch** 및 **SQLFetchScroll** 가져온 행 수를 반환 하는 버퍼를 가리킵니다.<br /><br /> 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetch를** 호출하면 **SQLFetch는** **SQLExtendedFetch에** 매핑되므로 이 버퍼의 값을 반환합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정합니다.<br /><br /> 응용 프로그램이 ODBC *2.x* 드라이버에서 SQL_ADD *작업으로* **SQLBulkOperations를** 호출하는 경우 호출이 SQL_ROWSET_SIZE 사용하는 SQL_ADD *작업을* 사용하여 **SQLSetPos에** 매핑되므로 SQL_ROWSET_SIZE SQL_ATTR_ROW_ARRAY_SIZE 아니라 호출에 사용됩니다.<br /><br /> ODBC *2.x* 드라이버에서 SQL_ADD 또는 **SQLExtendedFetch의** *작업으로* **SQLSetPos를** 호출하는 것은 SQL_ROWSET_SIZE 사용합니다.<br /><br /> ODBC *2.x* 드라이버에서 **SQLFetch** 또는 **SQLFetchScroll를** 호출하는 것은 SQL_ATTR_ROW_ARRAY_SIZE 사용합니다.|  
|**SQLBulk운영**|삽입 및 책갈피 작업을 수행합니다. SQL_ADD *작업을* 사용하여 **SQLBulkOperations가** ODBC *2.x* 드라이버에서 호출되면 SQL_ADD *작업으로* **SQLSetPos에** 매핑됩니다. 다음은 구현 세부 정보입니다.<br /><br /> - ODBC *2.x* 드라이버로 작업할 때 응용 프로그램은 *StatementHandle과*연결된 암시적으로 할당된 ARD만 사용해야 합니다. ODBC *2.x* 드라이버에서 명시적 설명자 작업이 지원되지 않으므로 행을 추가하기 위해 다른 ARD를 할당할 수 없습니다. 응용 프로그램은 **SQLBindCol을** 사용하여 **SQLSetDescField** 또는 **SQLSetDescRec**이 아닌 ARD에 바인딩해야 합니다.<br />- ODBC *3.x* 드라이버를 호출할 때 응용 프로그램은 **SQLFetch** 또는 **SQLFetchScroll**를 호출하기 전에 SQL_ADD *작업으로* **SQLBulkOperations를** 호출할 수 있습니다. ODBC *2.x* 드라이버를 호출할 때 응용 프로그램은 **SQLBulkOperations를** SQL_ADD 작업으로 호출하기 전에 **SQLFetchScroll를** 호출해야 합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetch를** 호출하면 **SQLExtendedFetch**에 매핑됩니다.<br />- 응용 프로그램이 ODBC *3.x* 드라이버에서 **SQLFetch를** 호출하면 SQL_ATTR_ROW_ARRAY_SIZE 문 특성으로 지정된 행 수를 반환합니다.|  
|**SQLFetchScroll**|지정된 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> - 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetchScroll를** 호출하면 단일 행에 적용되는 각 오류 전에 SQLSTATE 01S01(행의 오류)을 반환합니다. ODBC *3.x* 드라이버 관리자가 **SQLExtendedFetch에** 이 것을 매핑하고 **SQLExtendedFetch가** 이 SQLSTATE를 반환하기 때문에 이 작업을 수행합니다. 응용 프로그램이 ODBC *3.x* 드라이버에서 **SQLFetchScroll를** 호출하면 SQLSTATE 01S01(행의 오류)이 반환되지 않습니다.<br />- 응용 프로그램이 ODBC *2.x* 드라이버에서 **SQLFetchScroll을** 호출할 때 *FetchOrientation이* SQL_FETCH_BOOKMARK 설정된 *경우 FetchOffset* 인수를 0으로 설정해야 합니다. ODBC *2.x* 드라이버에서 오프셋 기반 책갈피 가져오기를 시도하는 경우 SQLSTATE HYC00(선택적 기능이 구현되지 않음)이 반환됩니다.|  
  
> [!NOTE]  
>  ODBC *3.x* 응용 프로그램은 **SQLExtendedFetch** 또는 SQL_ROWSET_SIZE 문 특성을 사용해서는 안 됩니다. 대신 **SQLFetchScroll** 및 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 사용해야 합니다. ODBC *3.x* 응용 프로그램은 SQL_ADD *작업과* 함께 **SQLSetPos를** 사용하지 말고 SQL_ADD *작업과* 함께 **SQLBulkOperations를** 사용해야 합니다.
