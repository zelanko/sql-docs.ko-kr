---
title: ODBC 아키텍처 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07435dc1a5fbe800f2260e914f315cfe93dd8d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305134"
---
# <a name="odbc-architecture"></a>ODBC 아키텍처
ODBC 아키텍처에는 다음 네 가지 구성 요소가 있습니다.  
  
-   **응용 프로그램** 처리를 수행하고 ODBC 함수를 호출하여 SQL 문을 제출하고 결과를 검색합니다.  
  
-   **드라이버 관리자** 응용 프로그램을 대신하여 드라이버를 로드하고 언로드합니다. ODBC 함수를 처리하여 호출하거나 드라이버에 전달합니다.  
  
-   **드라이버 (동그류** ODBC 함수 호출을 처리하고, 특정 데이터 원본에 SQL 요청을 제출하고, 결과를 응용 프로그램에 반환합니다. 필요한 경우 드라이버는 요청이 연결된 DBMS에서 지원하는 구문을 준수하도록 응용 프로그램의 요청을 수정합니다.  
  
-   **데이터 원본** 사용자가 액세스하려는 데이터와 DBMS에 액세스하는 데 사용되는 관련 운영 체제, DBMS 및 네트워크 플랫폼(있는 경우)으로 구성됩니다.  
  
 ODBC 아키텍처에 대한 다음 사항을 참고하십시오. 첫째, 여러 드라이버와 데이터 원본이 존재할 수 있으므로 응용 프로그램이 두 개 이상의 데이터 원본에서 동시에 데이터에 액세스할 수 있습니다. 둘째, ODBC API는 응용 프로그램과 드라이버 관리자, 드라이버 관리자와 각 드라이버 사이의 두 위치에서 사용됩니다. 드라이버 관리자와 드라이버 간의 인터페이스를 *서비스 공급자 인터페이스* 또는 *SPI라고도*합니다. ODBC의 경우 응용 프로그램 프로그래밍 인터페이스(API)와 서비스 공급자 인터페이스(SPI)는 동일합니다. 즉, 드라이버 관리자와 각 드라이버는 동일한 기능에 동일한 인터페이스를 갖습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [애플리케이션](../../odbc/reference/applications.md)  
  
-   [드라이버 관리자](../../odbc/reference/the-driver-manager.md)  
  
-   [드라이버](../../odbc/reference/drivers.md)  
  
-   [데이터 소스](../../odbc/reference/data-sources.md)
