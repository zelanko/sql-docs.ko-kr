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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bab3571ba880658d9f1a2629b899484008428083
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118793"
---
# <a name="bookmarks-odbc"></a>책갈피(ODBC)
책갈피는 데이터의 행을 식별하는 데 사용되는 값입니다. 책갈피 값의 의미는 드라이버나 데이터 원본에만 알려집니다. 예를 들어 책갈피 값은 행 번호처럼 간단하거나 디스크 주소처럼 복잡할 수 있습니다. ODBC에서 책갈피 실제 책의 책갈피와에서 약간 다릅니다. 실제 책에서 판독기가 특정 페이지에 책갈피를 배치 하 고 페이지로 반환 하는 책갈피를 찾습니다. ODBC 응용 프로그램에서는 특정 행에 대해 책갈피를 요청하고 이를 저장한 다음 다시 커서에 전달하여 원래 행으로 돌아갑니다. 따라서 ODBC에서 책갈피를 기억 하 고 다음 페이지를 다시 조회 된 페이지 번호를 적어 판독기 비슷합니다.  
  
 드라이버의 지원 책갈피를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_BOOKMARK_PERSISTENCE 옵션을 사용 합니다. 이 값의 비트 어떤 작업 책갈피에서 생존 커서를 닫은 후 책갈피 여전히 유효한 지 여부 등을 설명 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [책갈피 유형](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [책갈피 검색](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [책갈피로 스크롤](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [책갈피로 업데이트, 삭제 또는 페치](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [책갈피 비교](../../../odbc/reference/develop-app/comparing-bookmarks.md)
