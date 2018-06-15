---
title: 업데이트, 삭제 또는 책갈피 가져오는 | Microsoft Docs
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
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9b919d30d604410a30ae4c844471c1557b6a2a9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914858"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>업데이트, 삭제 또는 책갈피로 페치
데이터 집합 또는 결과 집합을 행 집합 버퍼에서에서 인출한 결과에서 삭제 된 결과 집합에서 업데이트를 확인할 책갈피를 사용할 수 있습니다. 호출 하 여 이러한 작업은 수행 **SQLBulkOperations** 와 *옵션* SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK, 또는 SQL_FETCH_BY_BOOKMARK의 인수입니다. 이러한 작업에 사용 되는 책갈피 행 집합 버퍼의 0 열에 저장 됩니다. 책갈피를 업데이트할 때 결과 집합 열의 데이터는 행 집합 버퍼에서 검색 하도록 업데이트 됩니다. 자세한 내용은 참조 [SQLBulkOperations 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)합니다.
