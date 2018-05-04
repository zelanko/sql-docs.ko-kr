---
title: 고정 길이의 책갈피 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c94d79500047fe1f918689426846a3faa98bb2d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="fixed-length-bookmarks"></a>고정 길이의 책갈피
ODBC 3 경우 *.x* 드라이버는 ODBC 2 함께 사용할 수 있어야 합니다. *x* 응용 프로그램 사용 하 여 고정 길이의 책갈피, 드라이버에서 다음을 지원 해야 합니다.  
  
-   SQL_UB_ON SQL_USE_BOOKMARKS 문 옵션에 대 한 값으로. (SQL_UB_ON ODBC 3에서 사용 되지 않는 *.x*.)  
  
-   SQL_GET_BOOKMARK 문 옵션입니다.
