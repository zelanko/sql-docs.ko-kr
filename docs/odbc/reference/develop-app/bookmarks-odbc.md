---
title: 책갈피 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8273c82b918024417e613ea44a2d26bafaf7d76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306324"
---
# <a name="bookmarks-odbc"></a>책갈피(ODBC)
책갈피는 데이터의 행을 식별하는 데 사용되는 값입니다. 책갈피 값의 의미는 드라이버나 데이터 원본에만 알려집니다. 예를 들어 책갈피 값은 행 번호처럼 간단하거나 디스크 주소처럼 복잡할 수 있습니다. ODBC의 책갈피는 실제 서적에서 책갈피와 약간 다릅니다. 실제 책에서 판독기는 특정 페이지에 책갈피를 배치한 다음 해당 책갈피를 찾아 페이지로 돌아갑니다. ODBC 애플리케이션에서는 특정 행에 대해 책갈피를 요청하고 이를 저장한 다음 다시 커서에 전달하여 원래 행으로 돌아갑니다. 따라서 ODBC의 책갈피는 페이지 번호를 기록한 후 페이지를 기억 하 고 페이지를 다시 조회 하는 판독기와 유사 합니다.  
  
 드라이버의 책갈피 지원을 확인 하기 위해 응용 프로그램은 SQL_BOOKMARK_PERSISTENCE 옵션으로 **SQLGetInfo** 를 호출 합니다. 이 값의 비트는 커서를 닫은 후 책갈피를 계속 사용할 수 있는지 여부와 같이 책갈피의 남은 작업을 설명 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [책갈피 형식](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [책갈피 검색](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [책갈피로 스크롤](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [책갈피로 업데이트, 삭제 또는 페치](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [책갈피 비교](../../../odbc/reference/develop-app/comparing-bookmarks.md)
