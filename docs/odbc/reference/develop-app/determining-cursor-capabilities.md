---
title: "커서 기능을 결정 하 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 490369663aaaee6f9dbb70504b61087ad96191d8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="determining-cursor-capabilities"></a>커서 기능을 결정 하
다음 네 가지 옵션 **SQLGetInfo** 커서의 종류는 지원 하 고, 이와 관련 된 기능에 설명 합니다.  
  
-   SQL_CURSOR_SENSITIVITY 합니다. 커서는 다른 커서가 변경한 내용의 영향 있는지 여부를 나타냅니다.  
  
-   SQL_SCROLL_OPTIONS 합니다. 지원 되는 커서 유형 (정방향 전용, 정적, 키 집합 커서, 동적 또는 혼합)을 나열합니다. 모든 데이터 원본 정방향 전용 커서를 지원 해야 합니다.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1, 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 (커서 유형)에 따라 다름 스크롤 가능 커서에서 지 원하는 인출 유형을 나열 합니다. 인출 형식에 해당 하는 반환 값에 비트 **SQLFetchScroll**합니다.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 (커서 유형)에 따라 다름. 정적 및 키 집합 커서는 자체 업데이트, 삭제 및 삽입 검색할 수 있는지 여부를 나열 합니다.  
  
 응용 프로그램 호출 하 여 런타임에 커서 기능을 확인 수 **SQLGetInfo** 이 옵션으로 합니다. 이 일반 응용 프로그램에서 일반적으로 수행 됩니다. 커서 기능 수를 결정할 수도 응용 프로그램 개발 및 하드 코드 된 사용 하는 동안 응용 프로그램으로. 이 세로 및 사용자 지정 응용 프로그램에서 일반적으로 수행 되지만 같은 ODBC 커서 라이브러리는 클라이언트 쪽 커서 구현을 사용 하는 일반 응용 프로그램에서 수행할 수도 있습니다.
