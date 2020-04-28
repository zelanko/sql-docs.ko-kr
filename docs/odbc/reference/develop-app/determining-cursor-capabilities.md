---
title: 커서 기능 결정 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 984ad8302f2e1695c8df84a64a18042f4cc9e364
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305884"
---
# <a name="determining-cursor-capabilities"></a>커서 기능 확인
**SQLGetInfo** 의 다음 네 가지 옵션은 지원 되는 커서 유형과 해당 기능에 대해 설명 합니다.  
  
-   SQL_CURSOR_SENSITIVITY. 커서가 다른 커서에서 변경한 내용을 인식 하는지 여부를 나타냅니다.  
  
-   SQL_SCROLL_OPTIONS. 지원 되는 커서 유형 (전진 전용, 정적, 키 집합, 동적 또는 혼합)을 나열 합니다. 모든 데이터 원본은 앞 으로만 이동 가능한 커서를 지원 해야 합니다.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 (커서의 유형에 따라 다름). 스크롤할 때 지원 되는 커서에서 지원 되는 fetch 유형을 나열 합니다. 반환 값의 비트는 **Sqlfetchscroll**의 인출 형식에 해당 합니다.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 또는 SQL_STATIC_CURSOR_ATTRIBUTES2 (커서의 유형에 따라 다름). 정적 및 키 집합 커서의 업데이트, 삭제 및 삽입을 검색할 수 있는지 여부를 나열 합니다.  
  
 응용 프로그램은 런타임에 이러한 옵션으로 **SQLGetInfo** 를 호출 하 여 커서 기능을 확인할 수 있습니다. 일반적으로 일반 응용 프로그램에 의해 수행 됩니다. 응용 프로그램을 개발 하는 동안 커서 기능을 결정 하 고 응용 프로그램에 하드 코딩 된 기능을 사용할 수도 있습니다. 이는 일반적으로 수직 및 사용자 지정 응용 프로그램에서 수행 되지만 ODBC 커서 라이브러리와 같은 클라이언트 쪽 커서 구현을 사용 하는 일반 응용 프로그램 에서도 수행할 수 있습니다.
