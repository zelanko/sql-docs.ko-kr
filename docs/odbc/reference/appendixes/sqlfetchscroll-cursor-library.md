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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5573b8afc49afec8b7afa4fc52590e7a6a9e2fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302054"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **Sqlfetchscroll** 함수를 사용 하는 방법을 설명 합니다. **Sqlfetchscroll**에 대 한 일반 정보는 [Sqlfetchscroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)를 참조 하세요.  
  
 커서 라이브러리는 드라이버에서 **Sqlfetch** 를 반복 해 서 호출 하 여 **sqlfetchscroll** 을 구현 합니다. 드라이버에서 검색 하는 데이터를 응용 프로그램에서 제공 하는 행 집합 버퍼로 전송 합니다. 또한 메모리 및 디스크 파일에 데이터를 캐시 합니다. 응용 프로그램이 새 행 집합을 요청 하면 커서 라이브러리는 드라이버 (이전에 인출 되지 않은 경우) 또는 캐시 (이전에 인출 된 경우)에서 필요에 따라이를 검색 합니다. 마지막으로 커서 라이브러리는 캐시 된 데이터의 상태를 유지 관리 하 고이 정보를 행 상태 배열의 응용 프로그램에 반환 합니다.  
  
 커서 라이브러리를 사용 하는 경우 **Sqlfetchscroll** 에 대 한 호출을 **Sqlfetch** 또는 **sqlfetchscroll**호출로 혼합할 수 없습니다.  
  
 커서 라이브러리를 사용 하는 경우에는 **Sqlfetchscroll** 에 대 한 호출이 ODBC 2 모두에서 지원 됩니다. *x* 및 for ODBC 3. *x* 드라이버.  
  
## <a name="rowset-buffers"></a>행 집합 버퍼  
 커서 라이브러리는 다음과 같은 경우 드라이버에서 응용 프로그램에서 제공 하는 행 집합 버퍼로 데이터 전송을 최적화 합니다.  
  
-   응용 프로그램에서 행 단위 바인딩을 사용 합니다.  
  
-   응용 프로그램에서 데이터 행을 저장 하기 위해 선언 하는 구조의 필드 사이에 사용 되지 않는 바이트가 없습니다.  
  
-   **Sqlfetch** 또는 **sqlfetchscroll** 이 반환 하는 필드는 해당 열에 대 한 버퍼 뒤에 오는 열의 길이/표시기를 반환 하 고 다음 열의 버퍼 앞에 옵니다. 이러한 필드는 선택 사항입니다.  
  
 응용 프로그램이 새 행 집합을 요청 하면 커서 라이브러리는 필요에 따라 해당 캐시 및 드라이버에서 데이터를 검색 합니다. 새 행 집합이 중복 되는 경우 커서 라이브러리는 행 집합 버퍼의 겹치는 섹션에서 데이터를 재사용 하 여 성능을 최적화할 수 있습니다. 따라서 새 행 집합 및 오래 된 행 집합이 중복 되 고 변경 내용이 행 집합 버퍼의 겹치는 부분에 없으면 행 집합 버퍼에 대 한 저장 되지 않은 변경 내용이 손실 됩니다. 응용 프로그램은 변경 내용을 저장 하기 위해 위치 지정 update 문을 전송 합니다.  
  
 커서 라이브러리는 항상 응용 프로그램이 **Sqlfetchscroll** 을 호출할 때 *fetchorientation* 인수가 SQL_FETCH_RELATIVE로 설정 되 고 *fetchoffset* 인수가 0으로 설정 된 경우 캐시의 데이터를 사용 하 여 행 집합 버퍼를 새로 고칩니다.  
  
 커서 라이브러리는 커서가 열려 있는 동안 행 집합 크기를 변경 하는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 을 가진 **SQLSetStmtAttr** 호출을 지원 합니다. 새 행 집합 크기는 다음에 **Sqlfetchscroll** 을 호출할 때 적용 됩니다.  
  
## <a name="result-set-membership"></a>결과 집합 멤버 자격  
 커서 라이브러리는 응용 프로그램에서 데이터를 요청 하는 경우에만 드라이버에서 데이터를 검색 합니다. 데이터 원본 및 SQL_CONCURRENCY statement 특성의 설정에 따라 다음과 같은 결과가 발생 합니다.  
  
-   커서 라이브러리에 의해 검색 된 데이터는 문이 실행 될 때 사용 가능한 데이터와 다를 수 있습니다. 예를 들어 커서를 연 후에는 일부 드라이버에서 현재 커서 위치를 벗어난 지점에 삽입 된 행을 검색할 수 있습니다.  
  
-   결과 집합의 데이터는 커서 라이브러리의 데이터 원본에 의해 잠겨 있으므로 다른 사용자가 사용할 수 없습니다.  
  
 커서 라이브러리가 데이터 행을 캐시 한 후에는 기본 데이터 원본에서 해당 행에 대 한 변경 내용을 검색할 수 없습니다. 단, 동일한 커서의 캐시에서 작동 하는 위치 지정 업데이트 및 삭제는 제외 됩니다. 이는 **Sqlfetchscroll**에 대 한 호출의 경우 커서 라이브러리가 데이터 원본에서 데이터를 refetches 하지 않기 때문에 발생 합니다. 대신 캐시에서 데이터를 refetches 합니다.  
  
## <a name="scrolling"></a>스크롤  
 커서 라이브러리는 **Sqlfetchscroll**에서 다음과 같은 인출 유형을 지원 합니다.  
  
|커서 유형|Fetch 형식|  
|-----------------|-----------------|  
|정방향 전용|SQL_FETCH_NEXT|  
|정적|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>오류  
 **Sqlfetchscroll** 이 호출 되 고 **sqlfetch** 에 대 한 호출 중 하나가 SQL_ERROR을 반환 하는 경우 커서 라이브러리는 다음과 같이 진행 됩니다. 이러한 단계를 완료 하면 커서 라이브러리의 처리가 계속 됩니다.  
  
1.  **SQLGetDiagRec** 를 호출 하 여 드라이버에서 오류 정보를 가져오고이를 드라이버 관리자의 진단 레코드로 게시 합니다.  
  
2.  진단 레코드의 SQL_DIAG_ROW_NUMBER 필드를 적절 한 값으로 설정 합니다.  
  
3.  진단 레코드의 SQL_DIAG_COLUMN_NUMBER 필드를 해당 하는 경우 적절 한 값으로 설정 합니다 (해당 하는 경우). 그렇지 않으면 0으로 설정 합니다.  
  
4.  행 상태 배열에서 오류가 발생 한 행의 값을 SQL_ROW_ERROR 설정 합니다.  
  
 **Sqlfetchscroll**을 구현할 때 커서 **라이브러리가 여러 번** 호출 된 후 **sqlfetch** 호출 중 하나에서 반환 된 오류 또는 경고는 진단 레코드에 포함 되며 **SQLGetDiagRec**를 호출 하 여 검색할 수 있습니다. 데이터를 반입할 때 잘린 경우 잘린 데이터가 이제 커서 라이브러리의 캐시에 저장 됩니다. 데이터가 잘린 행으로 스크롤할 수 있도록 **Sqlfetchscroll** 에 대 한 후속 호출에서는 잘린 데이터가 반환 되 고 데이터는 커서 라이브러리의 캐시에서 인출 되기 때문에 경고가 발생 하지 않습니다. 버퍼에 반환 된 데이터가 잘린 지 여부를 확인할 수 있도록 반환 되는 데이터의 길이를 추적 하려면 응용 프로그램이 길이/표시기 버퍼를 바인딩해야 합니다.  
  
## <a name="bookmark-operations"></a>책갈피 작업  
 커서 라이브러리는 SQL_FETCH_BOOKMARK의 *Fetchorientation* 로 **sqlfetchscroll** 호출을 지원 합니다. 또한 책갈피 작업에 사용할 수 있는 *fetchoffset* 인수에 오프셋을 지정 하는 것을 지원 합니다. 커서 라이브러리에서 지 원하는 유일한 책갈피 작업입니다. 커서 라이브러리는 **SQLBulkOperations**호출을 지원 하지 않습니다.  
  
 응용 프로그램에서 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정 하 고 책갈피 열에 바인딩한 경우 커서 라이브러리는 고정 길이 책갈피를 생성 하 여 응용 프로그램에 반환 합니다. 커서 라이브러리는 사용 하는 책갈피를 만들고 유지 관리 합니다. 데이터 원본에서 유지 관리 되는 책갈피를 사용 하지 않습니다. 데이터 원본에서 이미 인출 된 데이터 블록을 검색 하기 위해 **Sqlfetchscroll** 을 호출 하면 커서 라이브러리 캐시에서 데이터를 검색 합니다. 결과적으로, SQL_FETCH_BOOKMARK의 *Fetchorientation* 로 **sqlfetchscroll** 에 대 한 호출에 사용 되는 책갈피는 커서 라이브러리에서 만들고 유지 관리 해야 합니다.  
  
## <a name="interaction-with-other-functions"></a>다른 함수와의 상호 작용  
 응용 프로그램은 위치 지정 update 또는 delete 문을 준비 하거나 실행 하기 전에 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 해야 합니다.
