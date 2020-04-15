---
title: 블록 커서 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5c487bd8b60a83c709399cb9673dc0b015bd79d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306794"
---
# <a name="using-block-cursors"></a>블록 커서 사용
블록 커서에 대한 지원은 ODBC 3에 내장되어 있습니다. *x*. **SQLFetch는** ODBC 3에서 호출될 때 다중 행 인출에만 사용할 수 있습니다. *x;* ODBC 2인 경우. *x* 응용 프로그램은 **SQLFetch를**호출하며 단일 행의 정방향 전용 커서만 열립니다. 때 ODBC 3. *x* 응용 프로그램은 ODBC 2에서 **SQLFetch를** 호출합니다. *x* 드라이버가 **SQLExtendedFetch**를 지원하지 않는 한 단일 행을 반환합니다. 자세한 내용은 부록 G: 이전 버전과의 호환성을 위한 드라이버 지침에서 [커서 블록, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 참조하십시오.  
  
 블록 커서를 사용하려면 응용 프로그램은 행 집합 크기를 설정하고, 행 집합 버퍼를 바인딩하고(이전 섹션에서 설명한 대로), 선택적으로 SQL_ATTR_ROWS_FETCHED_PTR 및 SQL_ATTR_ROW_STATUS_PTR 문 특성을 **설정하고, SQLFetch** 또는 **SQLFetchScroll을** 호출하여 행 블록을 가져옵니다. 응용 프로그램은 행을 가져온 후에도 행 집합 크기를 변경하고 **SQLBindCol을** 호출하거나 바인드 오프셋을 지정하여 새 행 집합 버퍼를 바인딩할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [행 집합 크기](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [페치된 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 및 블록 커서; 블록 커소](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
