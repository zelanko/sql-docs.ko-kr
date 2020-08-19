---
description: 책갈피로 업데이트, 삭제 또는 페치
title: 책갈피에서 업데이트, 삭제 또는 페치 | Microsoft Docs
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
ms.openlocfilehash: 2202e3483e13848ccac7f7e6f21145ba9704a8b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448950"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>책갈피로 업데이트, 삭제 또는 페치
책갈피를 사용 하 여 결과 집합에서 업데이트 하거나 결과 집합에서 삭제 하거나 결과 집합에서 행 집합 버퍼로 가져올 데이터를 식별할 수 있습니다. 이러한 작업은 SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK 또는 SQL_FETCH_BY_BOOKMARK의 *옵션* 인수를 사용 하 여 **SQLBulkOperations** 를 호출 하 여 수행 됩니다. 이러한 작업에 사용 되는 책갈피는 행 집합 버퍼의 0 열에 저장 됩니다. 책갈피를 기준으로 업데이트 하는 경우 결과 집합 열이 업데이트 되는 데이터는 행 집합 버퍼에서 검색 됩니다. 자세한 내용은 [SQLBulkOperations를 사용 하 여 데이터 업데이트](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)를 참조 하세요.
