---
title: 블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3896473a1fa08f769f13d94bd1d81f373cf67c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854512"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>블록 커서, 스크롤 가능 커서 및 이전 버전과의 호환성
둘 다의 존재 여부 **SQLFetchScroll** 하 고 **SQLExtendedFetch** ODBC 간에 응용 프로그램 프로그래밍 인터페이스 (API) 되는 함수의 집합의에서 첫 번째 일반 분할 나타냅니다는 호출 응용 프로그램 및 서비스 공급자 인터페이스 (SPI), 함수의 집합인 드라이버 구현 합니다. 이 분할이 반드시 있도록 ODBC 3. *x*를 사용 하는 **SQLFetchScroll**, 표준 bealigned ODBC 2와 호환 되어야 하 고. *x*를 사용 하는 **SQLExtendedFetch**합니다.  
  
 ODBC 3 *.x* API 집합이 응용 프로그램이 호출 함수를 포함 **SQLFetchScroll** 및 관련 문 특성입니다. ODBC 3 *.x* 집합인 SPI 함수 드라이버 구현, 포함 **SQLFetchScroll**를 **SQLExtendedFetch**, 및 관련 문 특성입니다. 있기 때문에 ODBC API 및 SPI 간의이 분할이 공식적으로 강제 적용 하지 않습니다, ODBC 3 *.x* 응용 프로그램이 호출할 **SQLExtendedFetch** 및 관련 문 특성입니다. 그러나는 ODBC 3 자로 *.x* 이렇게 하려면 응용 프로그램입니다. Spi 및 Api에 대 한 자세한 내용은 참조에 대 한 소개 [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)합니다.  
  
 어떤 문과 함수에 대 한 자세한 특성을 ODBC 3. *x* 응용 프로그램 블록 및 스크롤 가능 커서를 사용 해야을 참조 하십시오 [블록 커서, 스크롤 가능 커서 및 ODBC 3.x 응용 프로그램에 대 한 이전 버전과 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 관리자가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [드라이버가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-does.md)
