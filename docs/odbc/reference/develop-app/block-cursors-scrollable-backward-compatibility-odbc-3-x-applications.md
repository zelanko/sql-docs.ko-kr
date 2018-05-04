---
title: 블록 및 스크롤 가능 커서 호환성 odbc 3.x | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670c81a8af1ec229a22ad9a8d52c8bab7164fdd1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>블록 커서, 스크롤 가능 커서 및 ODBC 3.x 응용 프로그램에 대 한 이전 버전과 호환성
둘 다의 존재 여부 **SQLFetchScroll** 및 **SQLExtendedFetch** 사이 API 응용 프로그래밍 인터페이스 (), 일련의 함수는 ODBC의 첫 번째 일반 분할 나타냅니다는 호출 응용 프로그램 및 서비스 공급자 인터페이스 (SPI), 일련의 함수는 드라이버 구현 합니다. 이 분할은 ODBC 3에서 요구 사항이 균형을 조정 해야 합니다. *x*를 사용 하 여 **SQLFetchScroll**는 표준을 준수 하 고 ODBC 2와 호환 되어야 합니다. *x*를 사용 하 여 **SQLExtendedFetch**합니다.  
  
 ODBC 3 *.x* 인 API의 집합, 응용 프로그램 호출 함수는 포함 **SQLFetchScroll** 및 관련 문 특성입니다. ODBC 3 *.x* SPI에 있는 함수의 드라이버 구현에 포함 **SQLFetchScroll**, **SQLExtendedFetch**, 및 관련 문 특성입니다. 없기 때문에 ODBC API와 SPI 간의이 분할이 공식적으로 지정 하지 ODBC 3에 대 한 *.x* 호출 하는 응용 프로그램 **SQLExtendedFetch** 및 관련 문 특성입니다. 그러나 ODBC 3에 대 한 없는 이유는 *.x* 응용 프로그램이이 작업을 수행할 수 있습니다. Api 및 Spi 하는 방법에 대 한 자세한 내용은 소개를 참조 하십시오. [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)합니다.  
  
 방법에 대 한 정보에 대 한 ODBC 3. *x* 드라이버 관리자 ODBC 2에 대 한 호출을 매핑합니다. *x* 및 ODBC 3. *x* 드라이버 및 어떤 함수 및 문 특성 ODBC 3. *x* 드라이버 있어야 블록 및 스크롤 가능 커서에 대 한 구현을 참조 하세요 [the 드라이버 용도](../../../odbc/reference/appendixes/what-the-driver-does.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
 다음 표에서 함수를 요약 하 고 문 특성 ODBC 3. *x* 응용 프로그램 블록 및 스크롤 가능 커서를 사용 해야 합니다. 또한 ODBC 2 사이의 변경 내용을 나열합니다. *x* 및 ODBC 3. *x* 이 영역에서 해당 ODBC 3. *x* ODBC 2와 호환 되도록 응용 프로그램 알고 있어야 합니다. *x* 드라이버입니다.  
  
|함수 또는<br /><br /> 문 특성|설명|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|사용 하면 책갈피를 가리키는 **SQLFetchScroll**합니다.<br /><br /> 때 응용 프로그램 설정이 ODBC 2. *x* 고정 길이의 책갈피를 가리켜야 합니다.이 드라이버를 합니다.|  
|SQL_ATTR_ROW_STATUS_PTR을|행 상태 배열이 가리키는로 채워진 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, 및 **SQLSetPos**합니다.<br /><br /> 응용 프로그램에 ODBC 2이를 설정 합니다. *x* 드라이버 및 호출 **SQLBulkOperation** 와 *작업* 호출 하기 전에 SQL_ADD의 **SQLFetchScroll**,  **SQLFetch**, 또는 **SQLExtendedFetch**, SQLSTATE HY011 (특성 지금 설정할 수 없습니다)이 반환 됩니다.<br /><br /> 응용 프로그램 호출 하는 경우 **SQLFetch** ODBC 2에서. *x* 드라이버 **SQLFetch** 에 매핑된 **SQLExtendedFetch** 따라서이 배열에 있는 값을 반환 합니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|버퍼를 가리키는 **SQLFetch** 및 **SQLFetchScroll** 인출 된 행 수를 반환 합니다.<br /><br /> 응용 프로그램 호출 하는 경우 **SQLFetch** ODBC 2에서. *x* 드라이버 **SQLFetch** 에 매핑된 **SQLExtendedFetch** 따라서이 버퍼의 값을 반환 합니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정합니다.<br /><br /> 응용 프로그램을 호출 하는 경우 **SQLBulkOperations** 와 *작업* 의 SQL_ADD ODBC 2에서. *x* 드라이버를 SQL_ROWSET_SIZE이 사용 됩니다 하지 SQL_ATTR_ROW_ARRAY_SIZE 호출에 대 한 호출에 매핑된 **SQLSetPos** 와 *작업* SQL_ADD 사용 하는 중 SQL_ROWSET_SIZE 합니다.<br /><br /> 호출 **SQLSetPos** 와 *작업* SQL_ADD의 또는 **SQLExtendedFetch** 는 odbc 2. *x* 드라이버 SQL_ROWSET_SIZE을 사용 합니다.<br /><br /> 호출 **SQLFetch** 또는 **SQLFetchScroll** 는 odbc 2. *x* 드라이버 SQL_ATTR_ROW_ARRAY_SIZE를 사용 합니다.|  
|**SQLBulkOperations**|Insert 및 책갈피 작업을 수행합니다. 때 **SQLBulkOperations** 와 *작업* SQL_ADD의 호출 되는 ODBC 2. *x* 에 매핑되어 드라이버를 **SQLSetPos** 와 *작업* SQL_ADD입니다. 다음은 구현 세부 정보:<br /><br /> -는 ODBC 2 작업할 때. *x* 드라이버, 응용 프로그램 관련 된 암시적으로 할당 된를 사용 해야는 *StatementHandle*; 명시적 설명자 작업은 때문에 행을 추가 하기 위한 다른를 할당할 수 없습니다. ODBC 2에서 지원 되지 않습니다. *x* 드라이버입니다. 응용 프로그램을 사용 해야 **SQLBindCol** 하지는 카드가에 바인딩할 **SQLSetDescField** 또는 **SQLSetDescRec**합니다.<br />-ODBC 3을 호출 하는 경우. *x* 응용 프로그램에서 호출할 수 드라이버 **SQLBulkOperations** 와 *작업* 호출 하기 전에 SQL_ADD의 **SQLFetch** 또는 **SQLFetchScroll**합니다. ODBC 2를 호출할 때입니다. *x* 드라이버, 응용 프로그램 호출 해야 **SQLFetchScroll** 호출 하기 전에 **SQLBulkOperations** 작업의 SQL_ADD 사용 합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 호출 경우 **SQLFetch** ODBC 2에서. *x* 에 매핑되어 드라이버를 **SQLExtendedFetch**합니다.<br />-응용 프로그램 호출 경우 **SQLFetch** ODBC 3에서. *x* 드라이버를 SQL_ATTR_ROW_ARRAY_SIZE 문 특성으로 지정 된 행의 수를 반환 합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 다음은 구현 세부 정보:<br /><br /> -응용 프로그램 호출 경우 **SQLFetchScroll** ODBC 2에서. *x* 드라이버, SQLSTATE 01S01 반환 (행에서 오류)는 단일 행에 적용 되는 각 오류에 앞서 있습니다. 이렇게 하기 때문에 ODBC 3 *.x* 드라이버 관리자를이 매핑합니다 **SQLExtendedFetch** 및 **SQLExtendedFetch** 이 SQLSTATE를 반환 합니다. 응용 프로그램 호출 하는 경우 **SQLFetchScroll** ODBC 3에서. *x* 드라이버를 반환 하지 않습니다 SQLSTATE 01S01 (행에서 오류).<br />-응용 프로그램 호출 경우 **SQLFetchScroll** ODBC 2에서. *x* 드라이버와 함께 *FetchOrientation* SQL_FETCH_BOOKMARK로 설정 된 *FetchOffset* 인수는 0으로 설정 해야 합니다. SQLSTATE HYC00 (선택적 기능이 구현 되지 않았습니다)는 ODBC 2 시도 되는 오프셋부터 시작 하는 책갈피를 인출 하는 경우에 반환 됩니다. *x* 드라이버입니다.|  
  
> [!NOTE]  
>  ODBC 3입니다. *x* 응용 프로그램을 사용 하지 않아야 **SQLExtendedFetch** 또는 SQL_ROWSET_SIZE 문 특성입니다. 대신 사용 해야 **SQLFetchScroll** 및 SQL_ATTR_ROW_ARRAY_SIZE 문 특성입니다. ODBC 3입니다. *x* 응용 프로그램을 사용 하지 않아야 **SQLSetPos** 와 *작업* SQL_ADD의 사용 해야 하지만 **SQLBulkOperations** 는 와*작업* SQL_ADD입니다.
