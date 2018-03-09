---
title: "ODBC 아키텍처 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7e1d59692492b2b14a51a8541e01d5e06a1a6d88
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-architecture"></a>ODBC 아키텍처
ODBC 아키텍처에는 네 가지 구성 요소에 있습니다.  
  
-   **응용 프로그램** SQL 문을 제출 하 고 결과 검색 하는 처리 및 호출 ODBC 함수를 수행 합니다.  
  
-   **드라이버 관리자** 로드 및 언로드 드라이버 응용 프로그램 대신 합니다. 프로세스 ODBC 함수 호출 또는 드라이버에 전달 합니다.  
  
-   **드라이버** 프로세스 ODBC 함수 호출 특정 데이터 원본에 대 한 SQL 요청을 제출 하 고 응용 프로그램에 결과 반환 합니다. 필요한 경우 드라이버 관련된 DBMS에 의해 지원 되는 구문에 맞는 요청 있도록 응용 프로그램의 요청을 수정 합니다.  
  
-   **데이터 원본** Consists 데이터의 사용자가 액세스와 관련 된 운영 체제, DBMS 및 네트워크 플랫폼 (있는 경우)는 DBMS에 액세스 하는 데 사용 합니다.  
  
 ODBC 아키텍처에 대해 다음 사항을 note 합니다. 동시에 둘 이상의 데이터 원본에서 데이터에 액세스 하도록 응용 프로그램을 허용 하는 첫 번째, 여러 개의 드라이버 및 데이터 원본을 존재할 수 있습니다. 다음 두 위치에서 ODBC API를 사용 하는 두 번째로,: 및 드라이버 관리자와 각 드라이버 사이의 응용 프로그램 및 드라이버 관리자입니다. 드라이버 관리자와 드라이버 간의 인터페이스는 라고도 *서비스 공급자 인터페이스* 또는 *SPI*합니다. ODBC 응용 프로그래밍 인터페이스 (API)와 서비스 공급자 인터페이스 (SPI)는 동일 합니다. 즉, 드라이버 관리자와 각 드라이버에는 동일한 기능을 같은 인터페이스가 있어야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [응용 프로그램](../../odbc/reference/applications.md)  
  
-   [드라이버 관리자](../../odbc/reference/the-driver-manager.md)  
  
-   [드라이버](../../odbc/reference/drivers.md)  
  
-   [데이터 원본](../../odbc/reference/data-sources.md)
