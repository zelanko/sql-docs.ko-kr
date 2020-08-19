---
description: ODBC 아키텍처
title: ODBC 아키텍처 | Microsoft Docs
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
ms.openlocfilehash: 3afeb698d7eff9d09161a091e3de0194fea93ec2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429005"
---
# <a name="odbc-architecture"></a>ODBC 아키텍처
ODBC 아키텍처에는 다음과 같은 네 가지 구성 요소가 있습니다.  
  
-   **응용 프로그램** 처리를 수행 하 고 ODBC 함수를 호출 하 여 SQL 문을 전송 하 고 결과를 검색 합니다.  
  
-   **드라이버 관리자** 응용 프로그램을 대신 하 여 드라이버를 로드 하 고 언로드합니다. 는 ODBC 함수 호출을 처리 하거나 드라이버에 전달 합니다.  
  
-   **드라이버** 는 ODBC 함수 호출을 처리 하 고, 특정 데이터 소스에 SQL 요청을 전송 하 고, 결과를 응용 프로그램에 반환 합니다. 필요한 경우 드라이버가 연결 된 DBMS에서 지 원하는 구문을 따르도록 응용 프로그램의 요청을 수정 합니다.  
  
-   **데이터 원본** 사용자가 액세스 하려고 하는 데이터 및 DBMS에 액세스 하는 데 사용 되는 연결 된 운영 체제, DBMS 및 네트워크 플랫폼 (있는 경우)으로 구성 됩니다.  
  
 ODBC 아키텍처에 대 한 다음 사항에 유의 하십시오. 먼저 여러 드라이버와 데이터 원본이 있을 수 있습니다 .이를 통해 응용 프로그램은 둘 이상의 데이터 원본에서 데이터에 동시에 액세스할 수 있습니다. 둘째, ODBC API는 응용 프로그램 및 드라이버 관리자와 드라이버 관리자와 각 드라이버 사이에서 두 곳에 사용 됩니다. 드라이버 관리자와 드라이버 간의 인터페이스를 *서비스 공급자 인터페이스* 또는 *SPI*라고도 합니다. ODBC의 경우 API (응용 프로그래밍 인터페이스)와 SPI (서비스 공급자 인터페이스)는 동일 합니다. 즉, 드라이버 관리자와 각 드라이버는 동일한 기능에 대해 동일한 인터페이스를 가집니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [애플리케이션](../../odbc/reference/applications.md)  
  
-   [드라이버 관리자](../../odbc/reference/the-driver-manager.md)  
  
-   [드라이버](../../odbc/reference/drivers.md)  
  
-   [데이터 원본](../../odbc/reference/data-sources.md)
