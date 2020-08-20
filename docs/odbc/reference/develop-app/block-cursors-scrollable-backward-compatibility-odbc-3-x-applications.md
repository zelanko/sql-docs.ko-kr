---
description: ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
title: ODBC 3.x의 블록 및 스크롤 가능 커서 호환성 | Microsoft Docs
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
ms.openlocfilehash: 96645f91d52f4141aacf4f2e171ef809a639f73c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476835"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
**Sqlfetchscroll** 및 **sqlfetchscroll** 는 모두 응용 프로그램에서 호출 하는 함수 집합인 API (응용 프로그래밍 인터페이스)와 드라이버에서 구현 하는 함수 집합인 SPI (서비스 공급자 인터페이스) 사이에서 ODBC의 첫 번째 명확한 분할을 나타냅니다. 이러한 분할은 **Sqlfetchscroll**을 사용 하 여 표준에 맞게 정렬 하 고 **sqlfetchscroll** *를 사용 하는 odbc 2.x*와 호환 되도록 하는 odbc *3(sp3)* 의 요구 사항을 분산 하는 데 필요 합니다.  
  
 응용 프로그램에서 호출 하는 함수 *집합인 ODBC 2.X* API는 **sqlfetchscroll** 및 관련 문 특성을 포함 합니다. 드라이버가 구현 하는 함수 *집합인 ODBC 3.X* SPI는 **sqlfetchscroll**, **sqlfetchscroll**및 관련 된 문 특성을 포함 합니다. ODBC는 API와 SPI 사이에 이러한 분할을 공식적으로 적용 하지 않으므로 ODBC *2.x 응용 프로그램* 에서 **sqlextendedfetch** 및 관련 문 특성을 호출할 수 있습니다. 그러나 ODBC 2.x 응용 프로그램에서이 작업을 수행 하는 이유는 *없습니다.* Api 및 SPIs에 대 한 자세한 내용은 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)소개를 참조 하세요.  
  
 Odbc *3.x 드라이버 관리자* 가에 대 한 호출을 수행 하는 방법에 대 한 자세한 *내용은 ODBC 2.x 및 odbc* *3. x* 드라이버를 매핑하는 방법 및 odbc *3.x 드라이버에서* 블록 및 스크롤 가능 커서에 대해 구현 해야 하 [는 기능](../../../odbc/reference/appendixes/what-the-driver-does.md) 에 대 한 자세한 내용은 부록 G: 드라이버 지침에서 이전 버전과의 호환성을 위한 드라이버 지침  
  
 다음 표에서 *는 ODBC 3.x* 응용 프로그램에서 블록 및 스크롤 가능 커서에 사용 해야 하는 함수 및 문 특성을 요약 하 여 보여 줍니다. *Odbc 2.x 응용* 프로그램에서 odbc *2.x 드라이버와* 호환 되는 것을 인식 해야 하는이 영역 *에서 odbc 2.x와 odbc* *3.x의 변경* 내용도 나열 됩니다.  
  
|함수 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|**Sqlfetchscroll**에 사용할 책갈피를 가리킵니다.<br /><br /> 응용 프로그램이 ODBC *2.x 드라이버에서* 이를 설정 하는 경우 고정 길이 책갈피를 가리켜야 합니다.|  
|SQL_ATTR_ROW_STATUS_PTR|**Sqlfetch**, **sqlfetchscroll**, **SQLBulkOperations**및 **SQLSetPos**로 채워진 행 상태 배열을 가리킵니다.<br /><br /> 응용 프로그램에서이를 ODBC *2.x 드라이버에* 설정 하 고 **sqlfetchscroll**, **Sqlfetch**또는 **sqlfetchscroll**를 호출 하기 전에 SQL_ADD *작업* 으로 **SQLBulkOperation** 를 호출 하는 경우 SQLSTATE HY011 (지금은 특성을 설정할 수 없음)이 반환 됩니다.<br /><br /> 응용 *프로그램이 ODBC 2.x* 드라이버에서 **sqlfetch** 를 호출 하면 **Sqlfetch** 는 **sqlextendedfetch** 에 매핑되며이 배열에서 값을 반환 합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|**Sqlfetch** 및 **sqlfetchscroll** 이 인출 된 행 수를 반환 하는 버퍼를 가리킵니다.<br /><br /> 응용 *프로그램이 ODBC 2.x* 드라이버에서 **sqlfetch** 를 호출 하는 경우 **Sqlfetch** 는 **sqlextendedfetch** 에 매핑되고 따라서이 버퍼에서 값을 반환 합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정 합니다.<br /><br /> 응용 *프로그램이 ODBC 2.x* 드라이버에서 SQL_ADD *작업* 을 사용 하 여 **SQLBulkOperations** 를 호출 하는 경우 호출은 SQL_ROWSET_SIZE을 사용 하는 SQL_ADD *작업* 을 통해 **SQLSetPos** 에 매핑되므로 SQL_ATTR_ROW_ARRAY_SIZE이 아닌 호출에 사용 됩니다 SQL_ROWSET_SIZE.<br /><br /> ODBC 2.x 드라이버에서 SQL_ADD 또는 **Sqlextendedfetch** 의 *작업* 을 사용 하 여 **SQLSetPos** 를 호출 하면 SQL_ROWSET_SIZE 사용 *됩니다.*<br /><br /> ODBC 2.x 드라이버에서 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하면 SQL_ATTR_ROW_ARRAY_SIZE 사용 *됩니다.*|  
|**SQLBulkOperations**|삽입 및 책갈피 작업을 수행 합니다. SQL_ADD *작업* 을 사용 하는 **SQLBulkOperations** 가 ODBC 2.x 드라이버에서 호출 되는 경우 SQL_ADD *작업* 을 사용 하 여 **SQLSetPos** 에 *매핑됩니다.* 구현 세부 정보는 다음과 같습니다.<br /><br /> -ODBC 2.x 드라이버를 사용 하는 경우 응용 프로그램은 *StatementHandle*와 연결 된 암시적으로 할당 된 인만 사용 해야 *합니다.* ODBC 2.x 드라이버에서는 명시적 설명자 작업이 지원 되지 않으므로 행을 추가 하기 위해 다른 기능을 할당할 수 *없습니다.* 응용 프로그램은 **SQLBindCol** 를 사용 하 여 **SQLSetDescField** 또는 **SQLSetDescRec**가 아닌 사용에 바인딩해야 합니다.<br />-ODBC 3.x 드라이버를 호출할 때 응용 프로그램은 **Sqlfetch** 또는 **sqlfetchscroll**을 호출 하기 전에 SQL_ADD *작업* 을 사용 하 여 **SQLBulkOperations** 를 호출할 수 *있습니다.* ODBC 2.x 드라이버를 호출할 때 응용 프로그램은 SQL_ADD 작업을 사용 하 여 **SQLBulkOperations** 를 호출 하기 전에 **sqlfetchscroll** 을 호출 해야 *합니다.*|  
|**SQLFetch**|다음 행 집합을 반환 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 *프로그램이 ODBC 2.x* 드라이버에서 **sqlfetch** 를 호출 하면 **sqlextendedfetch**에 매핑됩니다.<br />-응용 *프로그램이 ODBC 3.x* 드라이버에서 **sqlfetch** 를 호출할 때 SQL_ATTR_ROW_ARRAY_SIZE statement 특성으로 지정 된 행 수를 반환 합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 구현 세부 정보는 다음과 같습니다.<br /><br /> -응용 *프로그램이 ODBC 2.x* 드라이버에서 **sqlfetchscroll** 을 호출 하면 단일 행에 적용 되는 각 오류 앞에 SQLSTATE 01S01 (행 오류)가 반환 됩니다. 이 *는 ODBC 3.X* 드라이버 관리자가이를 **sqlextendedfetch** 에 매핑하고 **sqlextendedfetch** 에서이 SQLSTATE를 반환 하기 때문에 발생 합니다. 응용 *프로그램이 ODBC 3.x* 드라이버에서 **sqlfetchscroll** 을 호출 하면 SQLSTATE 01S01 (행에 오류)가 반환 되지 않습니다.<br />-응용 프로그램이 *Fetchorientation* 가 SQL_FETCH_BOOKMARK로 설정 *된 ODBC 2.X* 드라이버에서 **sqlfetchscroll** 을 호출 하는 경우 *fetchoffset* 인수를 0으로 설정 해야 합니다. SQLSTATE HYC00 (선택적 기능이 구현 되지 않음) *는 ODBC 2.x* 드라이버를 사용 하 여 오프셋 기반 책갈피 페치를 시도 하는 경우에 반환 됩니다.|  
  
> [!NOTE]  
>  ODBC *3.x 응용 프로그램은* **sqlextendedfetch** 또는 SQL_ROWSET_SIZE statement 특성을 사용 하면 안 됩니다. 대신 **Sqlfetchscroll** 및 SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 사용 해야 합니다. ODBC *3.x* 응용 프로그램은 SQL_ADD *작업과* 함께 **SQLSetPos** 를 사용 하면 안 되지만 SQL_ADD *작업* 에 **SQLBulkOperations** 를 사용 해야 합니다.
