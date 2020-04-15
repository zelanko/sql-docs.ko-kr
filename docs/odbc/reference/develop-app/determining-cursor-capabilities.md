---
title: 커서 기능 결정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305884"
---
# <a name="determining-cursor-capabilities"></a>커서 기능 확인
**SQLGetInfo의** 다음 네 가지 옵션은 지원되는 커서 유형과 해당 기능에 대해 설명합니다.  
  
-   SQL_CURSOR_SENSITIVITY. 커서가 다른 커서의 변경 사항에 민감하는지 여부를 나타냅니다.  
  
-   SQL_SCROLL_OPTIONS. 지원되는 커서 유형(정방향 전용, 정적, 키 집합 기반, 동적 또는 혼합)을 나열합니다. 모든 데이터 원본은 정방향 전용 커서를 지원해야 합니다.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1(커서의 유형에 따라 다름). 스크롤 가능한 커서에서 지원하는 가져오기 유형을 나열합니다. 반환 값의 비트는 **SQLFetchScroll**의 가져오기 형식에 해당합니다.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 또는 SQL_STATIC_CURSOR_ATTRIBUTES2(커서의 유형에 따라 다름). 정적 및 키 집합 기반 커서가 자체 업데이트, 삭제 및 삽입을 검색할 수 있는지 여부를 나열합니다.  
  
 응용 프로그램은 이러한 옵션을 사용하여 **SQLGetInfo를** 호출하여 런타임에 커서 기능을 확인할 수 있습니다. 이 작업은 일반적으로 일반 응용 프로그램에서 수행됩니다. 커서 기능은 응용 프로그램 개발 및 응용 프로그램에 하드 코딩된 사용 중에 확인할 수도 있습니다. 이 작업은 일반적으로 수직 및 사용자 지정 응용 프로그램에서 수행되지만 ODBC 커서 라이브러리와 같은 클라이언트 측 커서 구현을 사용하는 일반 응용 프로그램에서도 수행할 수 있습니다.
