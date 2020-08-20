---
description: 고정 길이 책갈피
title: 고정 길이 책갈피 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d357ba96141c658889628941c7f9492db5fd6b66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466179"
---
# <a name="fixed-length-bookmarks"></a>고정 길이 책갈피
ODBC *3.x 드라이버가 고정* 길이 책갈피를 사용 하는 odbc 2.x *응용 프로그램* 에서 작동 해야 하는 경우 드라이버는 다음을 지원 해야 합니다.  
  
-   SQL_USE_BOOKMARKS 문 옵션에 대 한 값으로 SQL_UB_ON 합니다. ODBC 3.x에서는 SQL_UB_ON 사용 되지 *않습니다.*  
  
-   SQL_GET_BOOKMARK 문 옵션입니다.
