---
title: 블록 커서를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bca1bc96ac1c2582bab592a80d65639944e0766
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-block-cursors"></a>블록 커서를 사용 하 여
블록 커서에 대 한 지원 변환은 ODBC 3에 있습니다. *x*합니다. **SQLFetch** 다중 행 인출 ODBC 3에서 호출 된 경우에 사용할 수 있습니다. *x*경우는 ODBC 2. *x* 응용 프로그램 호출 **SQLFetch**는 단일 행, 정방향 전용 커서가 열립니다. 때 ODBC 3. *x* 응용 프로그램 호출 **SQLFetch** ODBC 2에서. *x* 드라이버 반환 단일 행 드라이버를 지원 하지 않으면 **SQLExtendedFetch**합니다. 자세한 내용은 참조 [블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과 호환성에 대 한 부록 g: 드라이버 지침에 있습니다.  
  
 블록 커서를 사용 하려면 응용 프로그램은 행 집합 크기 설정, 행 집합 버퍼 (이전 섹션에서 설명), 필요에 따라 SQL_ATTR_ROWS_FETCHED_PTR 및 SQL_ATTR_ROW_STATUS_PTR 문 특성 집합과 호출 바인딩합니다 **SQLFetch**  또는 **SQLFetchScroll** 를 행 블록을 인출 합니다. 응용 프로그램에서 행 집합 크기를 변경 하 고 새 행 집합 버퍼를 바인딩할 수 (호출 하 여 **SQLBindCol** 바인딩 오프셋을 지정 하거나) 행 인출 된 후에 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [행 집합 크기](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [페치된 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 및 블록 커서; 블록 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
