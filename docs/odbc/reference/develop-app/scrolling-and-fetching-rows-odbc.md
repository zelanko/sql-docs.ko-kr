---
title: (ODBC) 행 스크롤 및 인출 | Microsoft Docs
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
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 273046a04849b0b1501e2dd4be476c9abb540c5f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="scrolling-and-fetching-rows-odbc"></a>스크롤 및 인출 행 (ODBC)
응용 프로그램 호출 하는 스크롤 가능한 커서를 사용할 때 **SQLFetchScroll** cursor와 fetch 행 위치입니다. **SQLFetchScroll** 상대 스크롤 지원 (다음, 이전, 및 상대 *n* 행), 절대 스크롤 (이름, 성 및 행 *n*), 및 책갈피에서 위치 지정 합니다. *FetchOrientation* 및 *FetchOffset* 인수에 **SQLFetchScroll** 다음 다이어그램에 나와 있는 것 처럼를 인출 하는 행 집합을 지정 합니다.  
  
 ![다음으로, 이전, 첫 번째 및 마지막 행 집합을 인출](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **다음으로, 이전, 첫 번째 및 마지막 행 집합을 인출**  
  
 ![절대, 상대 및 책갈피 지정 된 행 집합을 인출](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **절대, 상대 및 책갈피 지정 된 행 집합을 인출**  
  
 **SQLFetchScroll** 지정된 된 행에 커서를 배치 하 고 해당 행부터 행 집합의 행을 반환 합니다. 지정 된 행 집합 결과 집합의 끝을 중첩 하는 경우 부분 행 집합 반환 됩니다. 지정 된 행 집합 결과의 시작 겹치는 경우, 행 집합의 첫 번째 결과에서 집합 반환 됩니다. 자세한 내용은 참조는 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명 합니다.  
  
 경우에 따라 응용 프로그램 데이터를 검색 하지 않고 커서의 위치를 할 수 있습니다. 예를 들어에 행이 있는지 여부를 테스트 하거나 네트워크를 통해 다른 데이터를 표시 하지 않고 행에 대 한 책갈피 가져오기만 수도 있습니다. 이렇게 하려면 SQL_RD_OFF을 SQL_ATTR_RETRIEVE_DATA 문 특성을 설정 합니다. 이 문 특성 설정에 관계 없이 책갈피 열 (있는 경우)에 바인딩된 variable 항상, 업데이트 됩니다.  
  
 응용 프로그램을 호출할 수는 행 집합을 가져온 후 **SQLSetPos** 행 집합의 행 집합 또는 새로 고침 행에 있는 특정 행에 위치 합니다. 사용 하 여 대 한 자세한 내용은 **SQLSetPos**, 참조 [SQLSetPos 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)합니다.  
  
> [!NOTE]  
>  스크롤는 ODBC 2에서 지원 됩니다. *x* 드라이버 **SQLExtendedFetch**합니다. 자세한 내용은 참조 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.
