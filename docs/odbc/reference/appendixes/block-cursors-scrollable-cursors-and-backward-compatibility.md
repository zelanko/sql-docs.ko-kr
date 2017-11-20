---
title: "블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72c256f326366d631dada13fbfe002c8d4674eda
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>블록 커서, 스크롤 가능 커서 및 이전 버전과 호환성
둘 다의 존재 여부 **SQLFetchScroll** 및 **SQLExtendedFetch** 사이 API 응용 프로그래밍 인터페이스 (), 일련의 함수는 ODBC의 첫 번째 일반 분할 나타냅니다는 호출 응용 프로그램 및 서비스 공급자 인터페이스 (SPI), 일련의 함수는 드라이버 구현 합니다. 이 분할은 필요한 있도록 ODBC 3. *x*를 사용 하 여 **SQLFetchScroll**, standards bealigned 하며 ODBC 2와 호환 해야 합니다. *x*를 사용 하 여 **SQLExtendedFetch**합니다.  
  
 ODBC 3*.x* 인 API의 집합, 응용 프로그램 호출 함수는 포함 **SQLFetchScroll** 및 관련 문 특성입니다. ODBC 3*.x* SPI에 있는 함수의 드라이버 구현에 포함 **SQLFetchScroll**, **SQLExtendedFetch**, 및 관련 문 특성입니다. 없기 때문에 ODBC API와 SPI 간의이 분할이 공식적으로 지정 하지 ODBC 3에 대 한*.x* 호출 하는 응용 프로그램 **SQLExtendedFetch** 및 관련 문 특성입니다. 그러나 ODBC 3에 대 한 없는 이유는*.x* 응용 프로그램을이 작업을 수행 합니다. Api 및 Spi 하는 방법에 대 한 자세한 내용은 소개를 참조 하십시오. [ODBC 아키텍처](../../../odbc/reference/odbc-architecture.md)합니다.  
  
 어떤 함수 및 문에 대 한 정보에 대 한 특성 ODBC 3. *x* 응용 프로그램 블록 및 스크롤 가능 커서와 함께 사용 해야, 참조 [블록 커서, 스크롤 가능 커서 및 ODBC 3.x 응용 프로그램에 대 한 이전 버전과 호환성](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [드라이버 관리자가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [드라이버가 수행하는 작업](../../../odbc/reference/appendixes/what-the-driver-does.md)

