---
title: SQLFetchScroll (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16e7e4d133fdfafd7a005c19b0a2943b2ea9ef6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086449"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLFetchScroll** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLFetchScroll**를 참조 하십시오 [SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)합니다.  
  
 커서 라이브러리 구현 **SQLFetchScroll** 반복적으로 호출 하 여 **SQLFetch** 드라이버에서입니다. 드라이버에서 응용 프로그램에서 제공 하는 행 집합 버퍼를 검색 하는 데이터를 전송 합니다. 또한 메모리 및 디스크 파일에서 데이터를 캐시 합니다. 응용 프로그램에서 새 행 집합을 요청 하면 (이전에 반입 된) 경우 커서 라이브러리 (이 인출 되지 않은 이전) 하는 경우 드라이버 또는 캐시에서 필요에 따라 것을 검색 합니다. 마지막으로 커서 라이브러리 캐시 된 데이터의 상태를 유지 관리 하 고 응용 프로그램 행 상태 배열에이 정보를 반환 합니다.  
  
 커서 라이브러리를 사용 하는 경우 호출 **SQLFetchScroll** 중 하나를 호출 하 여 혼합할 수 없습니다 **SQLFetch** 하거나 **SQLExtendedFetch**합니다.  
  
 커서 라이브러리를 사용 하는 경우 호출 **SQLFetchScroll** 는 ODBC 2 모두 지원 합니다. *x* 고 ODBC 3. *x* 드라이버입니다.  
  
## <a name="rowset-buffers"></a>버퍼 행 집합  
 커서 라이브러리에 드라이버는 경우 응용 프로그램에서 제공 하는 행 집합 버퍼 데이터의 전송을 최적화 합니다.  
  
-   응용 프로그램에는 행 단위 바인딩을 사용합니다.  
  
-   응용 프로그램 데이터의 행을 보관할 수 선언 구조에서 필드 간 사용 되지 않는 바이트가 있습니다.  
  
-   필드 **SQLFetch** 하거나 **SQLFetchScroll** 열을 해당 열에 대 한 버퍼를 따르고 다음 열에 대 한 버퍼를 앞에 길이/표시기를 반환 합니다. 이러한 필드는 선택 사항입니다.  
  
 응용 프로그램에서 새 행 집합을 요청 하면 커서 라이브러리 캐시에서 필요에 따라 드라이버에서 데이터를 검색 합니다. 새 일정과 이전 행 집합은 겹치는 경우 커서 라이브러리 겹치는 행 집합 버퍼의 섹션에서 데이터를 다시 사용 하 여 성능을 최적화할 수 있습니다. 따라서 새 일정과 이전 행 집합에서 겹치는 경우가 아니면 행 집합 버퍼 겹치는 섹션의 변경 내용이 행 집합 버퍼에 저장 되지 않은 변경 내용이 손실 됩니다. 변경 내용의 저장 하려면 응용 프로그램 위치 지정된 update 문을 전송 합니다.  
  
 참고는 커서 라이브러리 항상 새로 고침 행 집합 버퍼 캐시에서 데이터를 사용 하 여 응용 프로그램을 호출할 때 **SQLFetchScroll** 사용 하 여는 *FetchOrientation* 인수 SQL_FETCH_RELATIVE로 설정 하 고 합니다 *FetchOffset* 인수는 0으로 설정 합니다.  
  
 커서 라이브러리 호출을 지 원하는 **SQLSetStmtAttr** 사용 하 여는 *특성* 커서가 열려 있는 동안에 행 집합 크기를 변경 하려면 sql_attr_row_array_size 라는 합니다. 새 행 집합 크기가 적용 됩니다 나중 **SQLFetchScroll** 라고 합니다.  
  
## <a name="result-set-membership"></a>결과 집합 멤버 자격  
 커서 라이브러리는 응용 프로그램이 요청할 때에 드라이버에서 데이터를 검색 합니다. 데이터 원본 및 SQL_CONCURRENCY 문 특성의 설정에 따라이 다음과 같은 결과가 발생 합니다.  
  
-   커서 라이브러리에 의해 검색 되는 데이터는 문이 실행 된 시간에 사용할 수 있는 데이터에서 달라질 수 있습니다. 예를 들어 커서가 열린 후 일부 드라이버에서 현재 커서 위치나 그 뒤에 삽입 된 행을 검색할 수 있습니다.  
  
-   결과 집합의 데이터는 커서 라이브러리에 대 한 데이터 원본에 의해 잠긴 상태일 수 있습니다 하 고 다른 사용자에 게 사용할 수 없게 될.  
  
 커서 라이브러리에 데이터 행을 캐시 한 후 해당 행을 변경 (제외 하 고 위치 지정된 업데이트 및 삭제 같은 커서를 캐시에서)의 데이터 원본에서 검색할 수 없습니다 것. 때문에 발생 하는이에 대 한 호출 **SQLFetchScroll**, 커서 라이브러리를 데이터 원본에서 데이터를 다시 되지 않습니다. 대신, 해당 캐시에서 데이터를 다시 합니다.  
  
## <a name="scrolling"></a>스크롤  
 커서 라이브러리 지원의 다음 인출 형식을 **SQLFetchScroll**합니다.  
  
|커서 유형|인출 유형|  
|-----------------|-----------------|  
|정방향 전용|SQL_FETCH_NEXT|  
|정적|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>오류  
 때 **SQLFetchScroll** 라고 하 고에 대 한 호출 중 하나 **SQLFetch** SQL_ERROR를 커서 라이브러리 진행 다음과 같이 반환 합니다. 다음이 단계를 완료 한 후 커서 라이브러리는 처리를 계속 합니다.  
  
1.  호출 **SQLGetDiagRec** 드라이버에서 오류 정보를 가져올 드라이버 관리자의 진단 레코드와이 게시 합니다.  
  
2.  적절 한 값을 진단 레코드에 SQL_DIAG_ROW_NUMBER 필드를 설정합니다.  
  
3.  해당 되는 경우 적절 한 값을 진단 레코드에 SQL_DIAG_COLUMN_NUMBER 필드 설정 그렇지 않으면 0으로 설정 하기.  
  
4.  SQL_ROW_ERROR 행 상태 배열에서 오류에서 행의 값을 설정합니다.  
  
 커서 라이브러리가 호출 **SQLFetch** 구현에서 여러 번 **SQLFetchScroll**를 오류 또는 경고에 대 한 호출 중 하나를 반환한 **SQLFetch** 진단 레코드의 수 고를 호출 하 여 검색할 수 있습니다 **SQLGetDiagRec**합니다. 페치 될 때 데이터가 잘렸습니다, 경우 잘린된 데이터는 이제 커서 라이브러리 캐시에 합니다. 에 대 한 후속 호출 **SQLFetchScroll** 행으로 스크롤해야 잘린된 데이터 잘린된 데이터를 반환 하 고 커서 라이브러리 캐시에서 데이터를 인출 되 때문에 경고가 발생 합니다. 추적 하는 버퍼에 반환 되는 데이터에 잘렸습니다 여부를 결정할 수 있도록 반환 된 데이터의 길이, 응용 프로그램에 길이/표시기 버퍼를 바인딩해야 합니다.  
  
## <a name="bookmark-operations"></a>책갈피 작업  
 커서 라이브러리 호출을 지 원하는 **SQLFetchScroll** 사용 하 여를 *FetchOrientation* 에서는 SQL_FETCH_BOOKMARK의 합니다. 오프셋을 지정도 지원 합니다 *FetchOffset* 책갈피 작업에 사용할 수 있는 인수입니다. 이 커서 라이브러리를 지 원하는 유일한 책갈피 작업입니다. 커서 라이브러리 호출을 지원 하지 않습니다 **SQLBulkOperations**합니다.  
  
 응용 프로그램 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정 하는 책갈피 열에 바인딩된 경우 커서 라이브러리는 고정 길이 책갈피를 생성 하 고 응용 프로그램에 반환 합니다. 커서 라이브러리를 만들고 사용 하 여; 책갈피를 유지 관리 데이터 원본에서 유지 관리 하는 책갈피를 사용 하지 않습니다. 때 **SQLFetchScroll** 라고를 이미 데이터 원본에서 가져온 데이터의 블록을 검색 하려면 커서 라이브러리 캐시에서 데이터를 검색 합니다. 책갈피에 대 한 호출에 사용 되는 결과적으로 **SQLFetchScroll** 사용 하 여를 *FetchOrientation* 의 SQL_FETCH_BOOKMARK 만들어지고 커서 라이브러리에 의해 유지 관리 되어야 합니다.  
  
## <a name="interaction-with-other-functions"></a>다른 기능과 상호 작용  
 응용 프로그램에서 호출 해야 합니다 **SQLFetch** 하거나 **SQLFetchScroll** update 또는 delete 문에 배치 하나를 준비 하거나 실행 하기 전에 합니다.
