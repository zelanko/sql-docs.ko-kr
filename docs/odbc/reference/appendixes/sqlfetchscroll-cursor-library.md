---
title: SQLFetch스크롤 (커서 라이브러리) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302054"
---
# <a name="sqlfetchscroll-cursor-library"></a>SQLFetchScroll(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLFetchScroll** 함수의 사용에 대해 설명합니다. **SQLFetchScroll에**대한 일반 정보는 [SQLFetchScroll 함수를](../../../odbc/reference/syntax/sqlfetchscroll-function.md)참조하십시오.  
  
 커서 라이브러리는 드라이버에서 **SQLFetch를** 반복적으로 호출하여 **SQLFetchScroll를** 구현합니다. 드라이버에서 검색한 데이터를 응용 프로그램에서 제공하는 행 집합 버퍼로 전송합니다. 또한 메모리 및 디스크 파일에 있는 데이터를 캐시합니다. 응용 프로그램이 새 행 집합을 요청하면 커서 라이브러리는 드라이버(이전에 가져온 적이 없는 경우) 또는 캐시(이전에 가져온 경우)에서 필요에 따라 커서 라이브러리를 검색합니다. 마지막으로 커서 라이브러리는 캐시된 데이터의 상태를 유지하고 이 정보를 행 상태 배열의 응용 프로그램에 반환합니다.  
  
 커서 라이브러리를 사용하는 경우 **SQLFetchScroll** 에 대한 호출을 **SQLFetch** 또는 **SQLExtendedFetch**에 대한 호출과 혼합할 수 없습니다.  
  
 커서 라이브러리를 사용하는 경우 ODBC 2에 대해 **SQLFetchScroll** 에 대한 호출이 모두 지원됩니다. *x* 및 ODBC 3. *x* 드라이버.  
  
## <a name="rowset-buffers"></a>행 집합 버퍼  
 커서 라이브러리는 다음과 같은 경우 드라이버에서 응용 프로그램에서 제공하는 행 집합 버퍼로의 데이터 전송을 최적화합니다.  
  
-   응용 프로그램은 행 별 바인딩을 사용합니다.  
  
-   응용 프로그램에서 데이터 행을 보유하도록 선언하는 구조의 필드 사이에 는 사용되지 않는 바이트가 없습니다.  
  
-   **SQLFetch** 또는 **SQLFetchScroll열에** 대 한 길이/표시기를 반환 하는 필드는 해당 열에 대 한 버퍼를 따라 다음 열에 대 한 버퍼 앞에 옵니다. 이러한 필드는 선택 사항입니다.  
  
 응용 프로그램이 새 행 집합을 요청하면 커서 라이브러리는 필요에 따라 해당 캐시와 드라이버에서 데이터를 검색합니다. 새 행 집합과 이전 행 집합이 겹치는 경우 커서 라이브러리는 행 집합 버퍼의 겹치는 섹션의 데이터를 다시 사용하여 성능을 최적화할 수 있습니다. 따라서 새 행 집합과 이전 행 집합이 겹치고 변경 내용이 행 집합 버퍼의 겹치는 섹션에 없는 한 행 집합 버퍼에 대한 저장되지 않은 변경 내용이 손실됩니다. 변경 내용을 저장하기 위해 응용 프로그램은 위치 지정 업데이트 문을 제출합니다.  
  
 커서 라이브러리는 응용 프로그램이 *fetchOrientation* 인수를 SQL_FETCH_RELATIVE 설정한 FETCHOrientation 인수를 사용하여 **SQLFetchScroll를** 호출하고 *FetchOffset* 인수를 0으로 설정할 때 항상 캐시의 데이터로 행 집합 버퍼를 새로 고칩니다.  
  
 커서 라이브러리는 커서가 열려 있는 동안 행 집합 크기를 변경하기 위해 SQL_ATTR_ROW_ARRAY_SIZE *특성을* 사용하여 **SQLSetStmtAttr호출을** 지원합니다. 새 행 집합 크기는 다음에 **SQLFetchScroll가** 호출될 때 적용됩니다.  
  
## <a name="result-set-membership"></a>결과 집합 멤버십  
 커서 라이브러리는 응용 프로그램이 요청하는 경우에만 드라이버에서 데이터를 검색합니다. 데이터 원본 및 SQL_CONCURRENCY 문 특성설정에 따라 다음과 같은 결과가 발생합니다.  
  
-   커서 라이브러리에서 검색한 데이터는 문이 실행될 때 사용 가능한 데이터와 다를 수 있습니다. 예를 들어 커서를 연 후 현재 커서 위치를 벗어난 지점에 삽입된 행은 일부 드라이버에서 검색할 수 있습니다.  
  
-   결과 집합의 데이터는 커서 라이브러리의 데이터 원본에 의해 잠겨 있으므로 다른 사용자가 사용할 수 없습니다.  
  
 커서 라이브러리에서 데이터 행을 캐시한 후에는 기본 데이터 원본에서 해당 행에 대한 변경 내용을 검색할 수 없습니다(동일한 커서의 캐시에서 작동하는 위치 업데이트 및 삭제 제외). **이는 SQLFetchScroll에**대한 호출에 대해 커서 라이브러리가 데이터 원본에서 데이터를 다시 가져오지 않으므로 발생합니다. 대신 캐시에서 데이터를 다시 가져옵니다.  
  
## <a name="scrolling"></a>스크롤  
 커서 라이브러리는 **SQLFetchScroll**에서 다음과 같은 가져오기 형식을 지원합니다.  
  
|커서 유형|가져오기 형식|  
|-----------------|-----------------|  
|정방향 전용|SQL_FETCH_NEXT|  
|정적|SQL_FETCH_NEXT<br /><br /> SQL_FETCH_PRIOR<br /><br /> SQL_FETCH_FIRST<br /><br /> SQL_FETCH_LAST<br /><br /> SQL_FETCH_RELATIVE<br /><br /> SQL_FETCH_ABSOLUTE<br /><br /> SQL_FETCH_BOOKMARK|  
  
## <a name="errors"></a>오류  
 **SQLFetchScroll가** 호출되고 **SQLFetch에** 대한 호출 중 하나가 SQL_ERROR 반환하면 커서 라이브러리는 다음과 같이 진행됩니다. 이러한 단계를 완료하면 커서 라이브러리가 처리를 계속합니다.  
  
1.  **SQLGetDiagRec을** 호출하여 드라이버에서 오류 정보를 가져오고 이를 드라이버 관리자에 진단 레코드로 게시합니다.  
  
2.  진단 레코드의 SQL_DIAG_ROW_NUMBER 필드를 적절한 값으로 설정합니다.  
  
3.  진단 레코드의 SQL_DIAG_COLUMN_NUMBER 필드를 해당되는 경우 적절한 값으로 설정합니다. 그렇지 않으면 0으로 설정합니다.  
  
4.  행 상태 배열의 오류 행에 대한 값을 SQL_ROW_ERROR 설정합니다.  
  
 커서 라이브러리가 **SQLFetchScroll의**구현에서 **SQLFetch를** 여러 번 호출한 후 **SQLFetch** 호출 중 하나에서 반환된 오류 또는 경고는 진단 레코드에 있으며 **SQLGetDiagRec**에 대한 호출로 검색할 수 있습니다. 데이터를 가져올 때 데이터가 잘린 경우 잘린 데이터는 이제 커서 라이브러리의 캐시에 상주합니다. 잘린 데이터가 있는 행으로 스크롤하기 위해 **SQLFetchScroll에** 대한 후속 호출은 잘린 데이터를 반환하며 커서 라이브러리의 캐시에서 데이터를 가져오므로 경고가 발생하지 않습니다. 버퍼에서 반환된 데이터가 잘렸는지 여부를 확인할 수 있도록 반환되는 데이터 길이를 추적하려면 응용 프로그램이 길이/표시기 버퍼를 바인딩해야 합니다.  
  
## <a name="bookmark-operations"></a>북마크 운영  
 커서 라이브러리는 SQL_FETCH_BOOKMARK *FetchOrientation를* 사용하여 **SQLFetchScroll** 호출을 지원합니다. 또한 책갈피 작업에 사용할 수 있는 *FetchOffset* 인수에서 오프셋을 지정하는 것도 지원합니다. 커서 라이브러리가 지원하는 유일한 책갈피 작업입니다. 커서 라이브러리는 **SQLBulkOperations**을 호출하는 것을 지원하지 않습니다.  
  
 응용 프로그램이 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정하고 책갈피 열에 바인딩된 경우 커서 라이브러리는 고정 길이 책갈피를 생성하여 응용 프로그램에 반환합니다. 커서 라이브러리는 사용하는 책갈피를 만들고 유지 관리합니다. 데이터 원본에서 유지 관리되는 책갈피를 사용하지 않습니다. **SQLFetchScroll는** 데이터 원본에서 이미 가져온 데이터 블록을 검색하기 위해 호출되면 커서 라이브러리 캐시에서 데이터를 검색합니다. 따라서 SQL_FETCH_BOOKMARK *FetchOrientation을* 사용하여 **SQLFetchScroll** 호출에 사용된 책갈피를 커서 라이브러리에서 만들고 유지 관리해야 합니다.  
  
## <a name="interaction-with-other-functions"></a>다른 기능과의 상호 작용  
 응용 프로그램은 위치에 있는 업데이트 또는 삭제 문을 준비하거나 실행하기 전에 **SQLFetch** 또는 **SQLFetchScroll를** 호출해야 합니다.
