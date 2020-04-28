---
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
ms.openlocfilehash: f90c5888a68506c056b2a56fce516080148528e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306984"
---
# <a name="fixed-length-bookmarks"></a>고정 길이 책갈피
ODBC *3.x 드라이버가 고정* 길이 책갈피를 사용 하는 odbc 2.x *응용 프로그램* 에서 작동 해야 하는 경우 드라이버는 다음을 지원 해야 합니다.  
  
-   SQL_USE_BOOKMARKS 문 옵션에 대 한 값으로 SQL_UB_ON 합니다. ODBC 3.x에서는 SQL_UB_ON 사용 되지 *않습니다.*  
  
-   SQL_GET_BOOKMARK 문 옵션입니다.
