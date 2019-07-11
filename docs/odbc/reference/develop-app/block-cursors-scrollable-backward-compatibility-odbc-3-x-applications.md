---
title: 블록 및 스크롤 가능 커서 호환성 odbc 3.x | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49a7a1af0f4b487baddfffa3e4f14d2a148b7a1d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794037"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>ODBC 3.x 애플리케이션의 블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
둘 다의 존재 여부 **SQLFetchScroll** 하 고 **SQLExtendedFetch** ODBC 간에 응용 프로그램 프로그래밍 인터페이스 (API) 되는 함수의 집합의에서 첫 번째 일반 분할 나타냅니다는 호출 응용 프로그램 및 서비스 공급자 인터페이스 (SPI), 함수의 집합인 드라이버 구현 합니다. 이 분할은 ODBC에서 요구 사항을 균형을 유지 해야 *3.x*를 사용 하는 **SQLFetchScroll**하는 표준을 준수 하 고 ODBC와 호환 되도록 *2.x*를 사용 하는 **SQLExtendedFetch**합니다.  
  
 ODBC *3.x* API 집합이 응용 프로그램이 호출 함수를 포함 **SQLFetchScroll** 및 관련 문 특성입니다. ODBC *3.x* 집합인 SPI 함수 드라이버 구현, 포함 **SQLFetchScroll**를 **SQLExtendedFetch**, 및 관련 문 특성입니다. 있기 때문에 ODBC API 및 SPI 간의이 분할이 공식적으로 강제 적용 하지 않습니다, odbc *3.x* 응용 프로그램이 호출할 **SQLExtendedFetch** 및 관련 문 특성입니다. 그러나 odbc 되지 않아도 됩니다 *3.x* 응용 프로그램을이 작업을 수행 합니다. Spi 및 Api에 대 한 자세한 내용은 참조에 대 한 소개 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)합니다.  
  
 하는 방법에 대 한 정보에 대 한 ODBC *3.x* 드라이버 관리자는 odbc 호출을 매핑합니다 *2.x* 및 ODBC *3.x* 드라이버 및 어떤 함수 및 문 특성 ODBC *3.x* 드라이버는 블록 및 스크롤 가능 커서에 대 한 구현 내용은 [the 드라이버 용도](../../../odbc/reference/appendixes/what-the-driver-does.md) 부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.  
  
 다음 표에서 기능 및 문 특성 ODBC *3.x* 응용 프로그램 블록 및 스크롤 가능 커서를 사용 해야 합니다. 또한 ODBC 간의 변경 내용을 나열 *2.x* 및 ODBC *3.x* 이 여기에는 ODBC *3.x* ODBC와 호환 되도록 응용 프로그램 인식 해야 *2.x* 드라이버입니다.  
  
|함수 또는<br /><br /> 문 특성|주석|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|사용 하는 책갈피를 가리키는 **SQLFetchScroll**합니다.<br /><br /> 응용 프로그램에서 ODBC이으로 설정 되는 경우 *2.x* 드라이버를이 가리켜야 고정 길이 책갈피입니다.|  
|SQL_ATTR_ROW_STATUS_PTR|행 상태 배열 가리키는 채울 **SQLFetch**, **SQLFetchScroll**를 **SQLBulkOperations**, 및 **SQLSetPos**합니다.<br /><br /> 응용 프로그램을 ODBC에이 설정 하는 경우 *2.x* 드라이버와 호출 **SQLBulkOperation** 사용 하 여는 *작업이* 호출 하기 전에 SQL_ADD의 **SQLFetchScroll**, **SQLFetch**, 또는 **SQLExtendedFetch**, SQLSTATE HY011 (특성 지금 설정할 수 없습니다)이 반환 됩니다.<br /><br /> 응용 프로그램을 호출할 때 **SQLFetch** 는 ODBC의 *2.x* 드라이버 **SQLFetch** 매핑되 **SQLExtendedFetch** 반환 하므로 이 배열에 있는 값입니다.|  
|SQL_ATTR_ROWS_FETCHED_PTR|버퍼를 가리키는 **SQLFetch** 하 고 **SQLFetchScroll** 인출 된 행 수를 반환 합니다.<br /><br /> 응용 프로그램을 호출할 때 **SQLFetch** ODBC에서 *2.x* 드라이버 **SQLFetch** 매핑되 **SQLExtendedFetch** 따라서 반환 하 고는 이 버퍼의 값입니다.|  
|SQL_ATTR_ROW_ARRAY_SIZE|행 집합 크기를 설정합니다.<br /><br /> 응용 프로그램을 호출 하는 경우 **SQLBulkOperations** 사용 하 여는 *작업* 의 ODBC에 SQL_ADD *2.x* 없습니다 SQL_ATTR_ROW_ARRAY_ 호출에 사용할 드라이버를 SQL_ROWSET_SIZE 크기, 호출에 매핑되므로 **SQLSetPos** 사용 하 여는 *작업* SQL_ADD SQL_ROWSET_SIZE를 사용 하는 중입니다.<br /><br /> 호출 **SQLSetPos** 사용 하 여는 *작업* SQL_ADD의 또는 **SQLExtendedFetch** ODBC에서 *2.x* 드라이버는 SQL_ROWSET_SIZE를 사용 합니다.<br /><br /> 호출 **SQLFetch** 하거나 **SQLFetchScroll** ODBC에서 *2.x* 드라이버는 SQL_ATTR_ROW_ARRAY_SIZE를 사용 합니다.|  
|**SQLBulkOperations**|Insert 및 책갈피 작업을 수행합니다. 때 **SQLBulkOperations** 사용 하 여는 *작업이* SQL_ADD의 ODBC에서 호출 되 *2.x* 에 매핑되어 드라이버 **SQLSetPos** 는를사용하여 *작업* SQL_ADD입니다. 다음은 구현 세부 정보입니다.<br /><br /> -ODBC를 사용 하 여 작업할 때 *2.x* 드라이버를 응용 프로그램에 관련 된 암시적으로 할당 된 카드가 사용 해야 합니다는 *StatementHandle*; 때문에 행을 추가 하기 위한 다른를 할당할 수 없습니다. 명시적 작업 설명자를 ODBC에서 지원 되지 않습니다 *2.x* 드라이버입니다. 응용 프로그램을 사용 해야 합니다 **SQLBindCol** 하지는 카드가에 바인딩할 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.<br />-ODBC를 호출할 때 *3.x* 드라이버, 응용 프로그램이 호출할 수 있습니다 **SQLBulkOperations** 사용 하 여는 *작업이* 호출 하기 전에 SQL_ADD의 **SQLFetch**나 **SQLFetchScroll**합니다. ODBC를 호출할 때 *2.x* 드라이버, 응용 프로그램 호출 해야 **SQLFetchScroll** 호출 하기 전에 **SQLBulkOperations** 작업의 SQL_ADD를 사용 하 여 합니다.|  
|**SQLFetch**|다음 행 집합을 반환합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 호출 **SQLFetch** 는 ODBC의 *2.x* 에 매핑되어 드라이버 **SQLExtendedFetch**합니다.<br />응용 프로그램 호출- **SQLFetch** 는 odbc *3.x* 드라이버 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 사용 하 여 지정 된 행의 수를 반환 합니다.|  
|**SQLFetchScroll**|지정 된 행 집합을 반환 합니다. 다음은 구현 세부 정보입니다.<br /><br /> -응용 프로그램 호출 **SQLFetchScroll** ODBC에서 *2.x* 드라이버 SQLSTATE 01S01 반환 (행의 오류) 단일 행에 적용 되는 각 오류에 앞서 합니다. 이렇게 하기 때문에 ODBC *3.x* 드라이버 관리자를이 매핑됩니다 **SQLExtendedFetch** 하 고 **SQLExtendedFetch** 이 SQLSTATE를 반환 합니다. 응용 프로그램을 호출할 때 **SQLFetchScroll** 는 odbc *3.x* 드라이버를 반환 하지 않습니다 SQLSTATE 01S01 (행의 오류).<br />-응용 프로그램 호출 **SQLFetchScroll** ODBC에서 *2.x* 드라이버와 함께 *FetchOrientation* SQL_FETCH_BOOKMARK로 설정 된 *FetchOffset* 인수는 0으로 설정 되어 있어야 합니다. SQLSTATE HYC00 ODBC를 사용 하 여 시도 오프셋 기반 책갈피 가져오는 경우 (선택적 기능이 구현 되지 않음)이 반환 됩니다 *2.x* 드라이버입니다.|  
  
> [!NOTE]  
>  ODBC *3.x* 응용 프로그램을 사용 하지 않아야 **SQLExtendedFetch** 또는 SQL_ROWSET_SIZE 문 특성입니다. 대신 사용 해야 **SQLFetchScroll** 및 SQL_ATTR_ROW_ARRAY_SIZE 문 특성입니다. ODBC *3.x* 응용 프로그램을 사용 하지 않아야 **SQLSetPos** 사용 하 여는 *작업이* SQL_ADD의를 사용 해야 **SQLBulkOperations** 는를사용하여 *작업* SQL_ADD입니다.
