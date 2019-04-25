---
title: 스크롤 및 페치 (ODBC) 행 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 884c798e14964fbcaaf3ca9ba6656f4d62738fe8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445994"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>행 스크롤 및 페치(ODBC)
스크롤 가능 커서를 사용 하는 경우 응용 프로그램 호출 **SQLFetchScroll** cursor와 fetch 행의 위치입니다. **SQLFetchScroll** 상대 스크롤을 지 원하는 (다음, 이전, 및 상대 *n* 행)을 절대 스크롤 (이름, 성 및 행 *n*), 및 책갈피에서 위치 지정 합니다. *FetchOrientation* 하 고 *FetchOffset* 에서 인수 **SQLFetchScroll** 다음 다이어그램에 나와 있는 것 처럼를 인출 하는 행 집합을 지정 합니다.  
  
 ![이전, 첫 번째 및 마지막 행 다음에 가져오는](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **다음으로, 이전, 첫 번째 및 마지막 행 집합을 인출**  
  
 ![절대, 상대 및 책갈피에 추가 된 행 집합을 인출](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **절대, 상대 및 책갈피에 추가 된 행 집합을 인출**  
  
 **SQLFetchScroll** 지정된 된 행에 커서를 배치 하 고 해당 행부터 행 집합의 행을 반환 합니다. 지정 된 행 집합 결과 집합의 끝 겹치면 부분 행 집합 반환 됩니다. 지정 된 행 집합 결과의 시작 겹치는 경우, 행 집합의 첫 번째 결과에서 집합 반환 됩니다. 자세한 내용은 참조는 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명 합니다.  
  
 경우에 따라 응용 프로그램 데이터를 검색 하지 않고 커서를 배치 하려고 수 있습니다. 예를 들어, 행이 있는지 여부를 테스트 하거나 네트워크를 통해 다른 데이터 표시 하지 않고 행에 대 한 책갈피 효과만 좋습니다. 이렇게 하려면 SQL_RD_OFF를 SQL_ATTR_RETRIEVE_DATA 문 특성을 설정 합니다. 이 문 특성의 설정에 관계 없이 책갈피 열 (해당 되는 경우)에 바인딩된 변수 항상, 업데이트 됩니다.  
  
 행 집합을 가져온 후 응용 프로그램이 호출할 수 있습니다 **SQLSetPos** 행 집합의 행 집합 또는 새로 고침 행에 있는 특정 행에 위치 합니다. 사용 하 여 대 한 자세한 내용은 **SQLSetPos**를 참조 하십시오 [SQLSetPos 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)합니다.  
  
> [!NOTE]  
>  스크롤 하는 ODBC 2에서 지원 됩니다. *x* 하 여 드라이버 **SQLExtendedFetch**합니다. 자세한 내용은 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)부록 g:에서 이전 버전과 호환성에 대 한 드라이버 지침입니다.
