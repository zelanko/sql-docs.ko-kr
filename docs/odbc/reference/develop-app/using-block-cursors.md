---
title: 블록 커서 사용 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306794"
---
# <a name="using-block-cursors"></a>블록 커서 사용
블록 커서에 대 한 지원은 ODBC 3에 기본 제공 됩니다. *x*. **Sqlfetch** 는 ODBC 3에서 호출 될 때 다중 행 페치에 대해서만 사용할 수 있습니다. *x*; ODBC 2 인 경우 *x* 응용 프로그램에서 **sqlfetch**를 호출 하면 단일 행, 앞 으로만 이동 가능한 커서만 열립니다. ODBC 3 인 경우 *x* 응용 프로그램은 ODBC 2에서 **sqlfetch** 를 호출 합니다. *x* 드라이버는 **sqlextendedfetch**를 지원 하지 않는 한 단일 행을 반환 합니다. 자세한 내용은 [블록 커서, 스크롤 가능 커서 및](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 이전 버전과의 호환성에 대 한 드라이버 지침의 이전 버전과의 호환성을 참조 하세요.  
  
 블록 커서를 사용 하기 위해 응용 프로그램은 행 집합 크기를 설정 하 고, 행 집합 버퍼를 바인딩하고 (이전 섹션에서 설명한 대로), 선택적으로 SQL_ATTR_ROWS_FETCHED_PTR 및 SQL_ATTR_ROW_STATUS_PTR 문 특성을 설정 하 고, **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 여 행 블록을 인출 합니다. 행이 인출 된 후에도 응용 프로그램에서 행 집합 크기를 변경 하 고 새 행 집합 버퍼를 바인딩할 수 있습니다 ( **SQLBindCol** 를 호출 하거나 바인드 오프셋을 지정).  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [행 집합 크기](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [페치된 행 수 및 상태](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 및 블록 커서 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
