---
title: "업데이트, 삭제 또는 책갈피 가져오는 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 520d33c12b88fd6cd1c03cd7fd64ec254662ae3d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>업데이트, 삭제 또는 책갈피로 페치
데이터 집합 또는 결과 집합을 행 집합 버퍼에서에서 인출한 결과에서 삭제 된 결과 집합에서 업데이트를 확인할 책갈피를 사용할 수 있습니다. 호출 하 여 이러한 작업은 수행 **SQLBulkOperations** 와 *옵션* SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK, 또는 SQL_FETCH_BY_BOOKMARK의 인수입니다. 이러한 작업에 사용 되는 책갈피 행 집합 버퍼의 0 열에 저장 됩니다. 책갈피를 업데이트할 때 결과 집합 열의 데이터는 행 집합 버퍼에서 검색 하도록 업데이트 됩니다. 자세한 내용은 참조 [SQLBulkOperations 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)합니다.
