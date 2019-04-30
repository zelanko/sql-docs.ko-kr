---
title: 업데이트, 삭제 또는 페치 책갈피 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5af3cad39739c3b85a0c6298d682d8e75a5918d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151219"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>책갈피로 업데이트, 삭제 또는 페치
데이터 집합 또는 결과 행 집합 버퍼에 집합에서 인출한 결과에서 삭제 결과 집합에서 업데이트를 식별 하려면 책갈피를 사용할 수 있습니다. 호출 하 여 이러한 작업은 수행 **SQLBulkOperations** 사용 하 여는 *옵션* SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK, 또는 SQL_FETCH_BY_BOOKMARK의 인수입니다. 이러한 작업에 사용 되는 책갈피 행 집합 버퍼의 0 열에 저장 됩니다. 책갈피로 업데이트, 행 집합 버퍼에서 검색 되는 결과 집합 열의 데이터 업데이트 됩니다. 자세한 내용은 [SQLBulkOperations 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)합니다.
