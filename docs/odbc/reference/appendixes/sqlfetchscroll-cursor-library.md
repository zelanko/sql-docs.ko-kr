---
title: SQLFetchScroll (커서 라이브러리) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQLFetchScroll function [ODBC], Cursor Library
ms.assetid: 4417e57c-31dd-475e-8fe9-eab00a459c80
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 014ed6202023a87d074faa7a746aa7f06fff04a7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLFetchScroll** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLFetchScroll**, 참조 [SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)합니다.  
  
 커서 라이브러리 구현 **SQLFetchScroll** 반복적으로 호출 하 여 **SQLFetch** 드라이버에서입니다. 응용 프로그램에서 제공 하는 행 집합 버퍼에는 드라이버에서 검색 된 데이터를 전송 합니다. 메모리 및 디스크 파일의 데이터를 캐시 하기도 합니다. 새 행 집합을 요청 하는 응용 프로그램 (이전에 반입 된) 경우 커서 라이브러리 (것 인출 되지 않은 이전에) 하는 경우 드라이버 또는 캐시에서 필요에 따라 것을 검색 합니다. 마지막으로, 커서 라이브러리는 캐시 된 데이터의 상태를 유지 관리 하 고 행 상태 배열이에서 응용 프로그램에이 정보를 반환 합니다.  
  
 커서 라이브러리를 사용 하는 경우에 대 한 호출이 **SQLFetchScroll** 에 대 한 호출 함께 **SQLFetch** 또는 **SQLExtendedFetch**합니다.  
  
 커서 라이브러리를 사용 하는 경우에 대 한 호출이 **SQLFetchScroll** 는 ODBC 2에 대 한 지원. *x* 고 odbc 3. *x* 드라이버입니다.  
  
## <a name="rowset-buffers"></a>버퍼 행 집합  
 커서 라이브러리에 드라이버 경우 응용 프로그램에서 제공 하는 행 집합 버퍼의 데이터 전송을 최적화 합니다.  
  
-   행 단위 바인딩을 사용 하는 응용 프로그램.  
  
-   응용 프로그램 데이터의 행을 보관 하기 선언 구조에서 필드 간 사용 하지 않는 바이트가 없습니다.  
  
-   필드는 **SQLFetch** 또는 **SQLFetchScroll** 열 해당 열에 대 한 버퍼를 따르며 다음 열에 대 한 버퍼를 앞에 길이/표시기를 반환 합니다. 이러한 필드는 선택 사항입니다.  
  
 새 행 집합을 요청 하는 응용 프로그램 커서 라이브러리는 필요에 따라 드라이버 들어오고 캐시에서 데이터를 검색 합니다. 신규 버전과 기존 행 집합 겹치는 경우 커서 라이브러리는 겹치는 섹션 행 집합 버퍼의 데이터를 다시 사용 하 여 해당 성능을 최적화할 수 있습니다. 따라서 신규 버전과 기존 행 집합 겹치고 변경 내용을 행 집합 버퍼 겹치는 섹션에서 설명 하지 않는 한 행 집합 버퍼에 저장 되지 않은 변경 내용이 손실 됩니다. ְ ת, 응용 프로그램을 위치 지정된 update 문을 제출 합니다.  
  
 으로 커서 라이브러리 항상 새로 고치도록 캐시에서 데이터를 사용 하 여 행 집합 버퍼 응용 프로그램 호출 때 참고 **SQLFetchScroll** 와 *FetchOrientation* 인수 SQL_FETCH_RELATIVE로 설정 하 고 *FetchOffset* 인수는 0으로 설정 합니다.  
  
 커서 라이브러리 호출을 지 원하는 **SQLSetStmtAttr** 와 *특성* sql_attr_row_array_size 라는 커서가 열려 있는 동안 행 집합 크기를 변경할 수 있습니다. 새 행 집합 크기가 적용 됩니다 다음에 **SQLFetchScroll** 호출 됩니다.  
  
## <a name="result-set-membership"></a>결과 집합 멤버 자격  
 커서 라이브러리는 응용 프로그램이 요청할 때에 드라이버에서 데이터를 검색 합니다. 이 데이터 원본 및 SQL_CONCURRENCY 문 특성의 설정에 따라 다음과 같은 결과가 같습니다.  
  
-   커서 라이브러리에서 검색 되는 데이터는 데이터를 문이 실행 된 시간에 사용 가능 했던 다를 수 있습니다. 예를 들어, 커서를 연 후 일부 드라이버에 의해 시점 이후로 현재 커서 위치에 삽입 된 행을 검색할 수 있습니다.  
  
-   결과 집합의 데이터 커서 라이브러리에 대 한 데이터 원본에 의해 잠긴 상태일 수 없고 따라서 수 다른 사용자에 게 사용할 수 없습니다.  
  
 커서 라이브러리에서 데이터 행을 캐시 한 후 해당 행에 대 한 변경 (제외 하 고 위치 지정된 업데이트 및 삭제 같은 커서 캐시에 대 한 작동) 데이터 원본에서 검색할 수 없어 합니다. 이 발생 하기 때문에 대 한 호출 **SQLFetchScroll**, 커서 라이브러리는 데이터 원본에서 데이터를 다시 되지 않습니다. 대신, 캐시에서 데이터를 다시 합니다.  
  
## <a name="scrolling"></a>스크롤  
 커서 라이브러리에서 fetch 형식을 지원 **SQLFetchScroll**합니다.  
  
|커서 유형|인출 유형|  
|-----------------|-----------------|  
|정방향 전용|SQL_FETCH_NEXT|  
|정적|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>오류  
 때 **SQLFetchScroll** 호출에 대 한 호출 중 하나를 **SQLFetch** 다음과 같은 커서 라이브러리 진행 SQL_ERROR를 반환 합니다. 다음이 단계를 완료 한 후 커서 라이브러리는 처리를 계속 합니다.  
  
1.  호출 **SQLGetDiagRec** 드라이버에서 오류 정보를 가져오는 진단 레코드로 드라이버 관리자에서이 게시 합니다.  
  
2.  SQL_DIAG_ROW_NUMBER 필드는 진단 레코드 적절 한 값으로 설정합니다.  
  
3.  해당 되는 경우 적절 한 값으로는 진단 레코드 SQL_DIAG_COLUMN_NUMBER 필드 설정 그렇지 않으면 것 것을 0으로 설정 합니다.  
  
4.  SQL_ROW_ERROR 행 상태 배열이에서 오류가 있는 행에 대 한 값을 설정합니다.  
  
 커서 라이브러리가 호출 **SQLFetch** 여러 번 구현에서에서 **SQLFetchScroll**, 모든 오류 또는 경고 하나에 대 한 호출에서 반환 된 **SQLFetch** 진단 레코드에 되 고 호출 하 여 검색할 수 **SQLGetDiagRec**합니다. 인출 된 될 때 데이터가 잘렸습니다, 경우 잘린된 데이터 커서 라이브러리의 캐시에 있는 이제 됩니다. 에 대 한 후속 호출 **SQLFetchScroll** 포함 된 행으로 스크롤해야 잘린된 데이터 잘린된 데이터를 반환 하 고 경고 없이 데이터가 커서 라이브러리 캐시에서 인출 되 때문에 발생 합니다. 추적 하는 버퍼에 반환 되는 데이터 잘린 있는지 여부를 결정할 수 있도록 반환 된 데이터의 길이, 응용 프로그램에 길이/표시기 버퍼를 바인딩해야 합니다.  
  
## <a name="bookmark-operations"></a>책갈피 작업  
 커서 라이브러리 호출을 지 원하는 **SQLFetchScroll** 와 *FetchOrientation* 에서는 SQL_FETCH_BOOKMARK의 합니다. 도 지원 합니다.에서 오프셋을 지정 하는 *FetchOffset* 책갈피 동작에서 사용할 수 있는 인수입니다. 커서 라이브러리에서 지 원하는 유일한 책갈피 작업입니다. 커서 라이브러리가 호출을 지원 하지 않을 **SQLBulkOperations**합니다.  
  
 응용 프로그램이 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정 하는 책갈피 열에 바인딩된 하는 경우 커서 라이브러리는 고정 길이 책갈피를 생성 하 고 응용 프로그램에 반환 합니다. 커서 라이브러리를 만들고 사용 하 여; 된 책갈피를 유지 관리 데이터 원본에서 유지 관리 하는 책갈피를 사용 하지 않습니다. 때 **SQLFetchScroll** 라고를 이미 데이터 원본에서 가져온 데이터 블록을 검색 하려면 커서 라이브러리 캐시에서의 데이터를 검색 합니다. 책갈피에 대 한 호출에서 사용 하는 결과적으로, **SQLFetchScroll** 와 *FetchOrientation* 의 SQL_FETCH_BOOKMARK를 생성 하 고 커서 라이브러리에서 유지 관리 해야 합니다.  
  
## <a name="interaction-with-other-functions"></a>다른 기능과 상호 작용  
 호출 하는 응용 프로그램 **SQLFetch** 또는 **SQLFetchScroll** 준비 하거나 실행 하기 전에 배치 되는 update 또는 delete 문에 합니다.
