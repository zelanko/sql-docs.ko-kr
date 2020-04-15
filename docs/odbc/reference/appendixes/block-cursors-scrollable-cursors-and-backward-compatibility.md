---
title: 블록 커서, 스크롤 가능한 커서 및 이전 버전과의 호환성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe24362f1a49577a7fb494f768947080d0ab6e9e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292313"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
**SQLFetchScroll** 및 **SQLExtendedFetch의** 존재는 응용 프로그램이 호출하는 함수 집합인 API(응용 프로그램 프로그래밍 인터페이스)와 드라이버가 구현하는 함수 집합인 SPI(서비스 공급자 인터페이스) 간의 ODBC에서 첫 번째 명확한 분할을 나타냅니다. 이 분할은 **SQLFetchScroll를**사용하는 ODBC *3.x가*표준과 정렬되고 **SQLExtendedFetch를**사용하는 ODBC *2.x와*호환되도록 필요합니다.  
  
 응용 프로그램에서 호출하는 함수 집합인 ODBC *3.x* API에는 **SQLFetchScroll** 및 관련 문 특성이 포함됩니다. 드라이버가 구현하는 함수 집합인 ODBC *3.x* SPI에는 **SQLFetch스크롤,** **SQLExtendedFetch**및 관련 문 특성이 포함됩니다. ODBC는 API와 SPI 간에 이 분할을 공식적으로 적용하지 않으므로 ODBC *3.x* 응용 프로그램에서 **SQLExtendedFetch** 및 관련 문 특성을 호출할 수 있습니다. 그러나 ODBC *3.x* 응용 프로그램에서 이 작업을 수행할 이유가 없습니다. API 및 SAPI에 대한 자세한 내용은 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)에 대한 소개를 참조하십시오.  
  
 ODBC *3.x* 응용 프로그램이 블록 및 스크롤 가능한 커서와 함께 사용해야 하는 함수 및 명령문 특성에 대한 자세한 내용은 [ODBC 3.x 응용 프로그램에 대한 블록 커서, 스크롤 가능한 커서 및 이전 버전과의 호환성을](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 관리자가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [드라이버가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-does.md)
