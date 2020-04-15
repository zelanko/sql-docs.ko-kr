---
title: 책갈피로 업데이트, 삭제 또는 가져오기 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e94a98bb577ef906afbb04539761fd07d15f772
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286153"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>책갈피로 업데이트, 삭제 또는 페치
책갈피를 사용하여 결과 집합에서 업데이트하거나, 결과 집합에서 삭제하거나, 결과 집합에서 행 집합 버퍼로 가져올 데이터를 식별할 수 있습니다. 이러한 작업은 SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK 또는 SQL_FETCH_BY_BOOKMARK *옵션* 인수를 사용 하 여 **SQLBulkOperations를** 호출 하 여 수행 됩니다. 이러한 작업에 사용되는 책갈피는 행 집합 버퍼의 열 0에 저장됩니다. 책갈피로 업데이트할 때 결과 집합 열이 업데이트되는 데이터는 행 집합 버퍼에서 검색됩니다. 자세한 내용은 [SQLBulkOperations를 사용하여 데이터 업데이트를](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)참조하십시오.
