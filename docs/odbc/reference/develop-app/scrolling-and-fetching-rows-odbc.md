---
title: 행 스크롤 및 가져오기(ODBC) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72d262bf73e69388f65ff281e62235d2d831669e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304204"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>행 스크롤 및 페치(ODBC)
스크롤 가능한 커서를 사용하는 경우 응용 프로그램은 **SQLFetchScroll를** 호출하여 커서를 배치하고 행을 가져옵니다. **SQLFetchScroll는** 상대 스크롤(다음, 이전 및 상대 *n* 행), 절대 스크롤(첫 번째, 마지막 및 행 *n)* 및 책갈피별로 위치를 지정하는 것을 지원합니다. **SQLFetchScroll의** *FetchOrientation* 및 *FetchOffset* 인수는 다음 다이어그램과 같이 가져올 행 집합을 지정합니다.  
  
 ![다음, 이전, 첫 번째 및 마지막 행 집합 페치](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **다음, 이전, 첫 번째 및 마지막 행 집합 페치**  
  
 ![절대, 상대 및 책갈피 지정된 행 집합 페치](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **절대, 상대 및 북마크행 집합 가져오기**  
  
 **SQLFetchScroll는** 커서를 지정된 행에 배치하고 해당 행으로 시작하는 행집합의 행을 반환합니다. 지정된 행 집합이 결과 집합의 끝과 겹치면 부분 행 집합이 반환됩니다. 지정된 행 집합이 결과 집합의 시작과 겹치면 결과 집합의 첫 번째 행 집합이 반환됩니다. 자세한 내용은 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 함수 설명을 참조하십시오.  
  
 경우에 따라 응용 프로그램은 데이터를 검색하지 않고 커서를 배치하려고 할 수 있습니다. 예를 들어 네트워크를 통해 다른 데이터를 가져오지 않고 행이 있는지 테스트하거나 행의 책갈피를 가져오는 것이 좋습니다. 이렇게 하려면 SQL_RD_OFF SQL_ATTR_RETRIEVE_DATA 문 특성을 설정합니다. 책갈피 열에 바인딩된 변수(있는 경우)는 이 문 특성의 설정에 관계없이 항상 업데이트됩니다.  
  
 행 집합을 검색한 후 응용 프로그램은 **SQLSetPos를** 호출하여 행 집합의 특정 행에 배치하거나 행 집합의 행을 새로 고칠 수 있습니다. **SQLSetPos**사용에 대한 자세한 내용은 [SQLSetPos를 사용하여 데이터 업데이트를](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)참조하십시오.  
  
> [!NOTE]  
>  스크롤은 ODBC 2에서 지원됩니다. *x* 드라이버 로 **SQLExtendedFetch**. 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [커서 블록, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)참조하십시오.
