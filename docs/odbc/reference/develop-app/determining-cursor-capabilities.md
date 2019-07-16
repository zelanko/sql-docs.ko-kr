---
title: 커서 기능 확인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14715e40cd99f3f1a03c2ae19e825705a8376e30
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040000"
---
# <a name="determining-cursor-capabilities"></a>커서 기능 확인
다음 네 가지 옵션 **SQLGetInfo** 지 원하는 커서의 형식 및 해당 기능에 설명 합니다.  
  
-   SQL_CURSOR_SENSITIVITY. 커서를 다른 커서가 변경한 내용의 중요 한지 여부를 나타냅니다.  
  
-   SQL_SCROLL_OPTIONS. 지원 되는 커서 유형에 (정방향 전용, 정적, 키 집합 커서, 동적 또는 혼합)을 나열합니다. 모든 데이터 원본 정방향 전용 커서를 지원 해야 합니다.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1, 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 (커서 유형)에 따라 다름 스크롤 가능 커서를 지 원하는 인출 유형을 나열 합니다. 인출 형식에 해당 하는 반환 값의 비트 **SQLFetchScroll**합니다.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 (커서 유형)에 따라 다름. 정적 및 키 집합 커서는 자체 업데이트, 삭제 및 삽입 감지할 수 있는지 여부를 나열 합니다.  
  
 응용 프로그램 호출 하 여 런타임에 커서 기능을 확인 수 있습니다 **SQLGetInfo** 이러한 옵션을 사용 하 여 합니다. 이 일반 응용 프로그램에서 일반적으로 수행 됩니다. 커서 기능도 확인할 수 있습니다 응용 프로그램 개발 및 하드 코드 된 사용 하는 동안 응용 프로그램에 있습니다. 이 세로 및 사용자 지정 응용 프로그램에서 일반적으로 수행 되지만 ODBC 커서 라이브러리 등 클라이언트 쪽 커서 구현을 사용 하는 일반 응용 프로그램에서 수행할 수도 있습니다.
