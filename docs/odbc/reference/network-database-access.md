---
description: 네트워크 데이터베이스 액세스
title: 네트워크 데이터베이스 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 025959072b7ebadc96fd1d1a628bdfaf5d449940
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461325"
---
# <a name="network-database-access"></a>네트워크 데이터베이스 액세스
네트워크를 통해 데이터베이스에 액세스 하려면 여러 구성 요소가 필요 하며, 각 구성 요소는와 독립적 이며 프로그래밍 인터페이스 아래에 있습니다. 이러한 구성 요소는 다음 그림에 나와 있습니다.  
  
 ![네트워크를 통해 데이터베이스에 액세스하는 데 필요한 구성 요소](../../odbc/reference/media/pr04.gif "pr04")  
  
 각 구성 요소에 대 한 자세한 설명은 다음과 같습니다.  
  
-   **프로그래밍 인터페이스** 이 단원의 앞부분에서 설명한 것 처럼 프로그래밍 인터페이스에는 응용 프로그램에서 수행 하는 호출이 포함 되어 있습니다. 이러한 인터페이스 (포함 된 SQL, SQL 모듈 및 호출 수준 인터페이스)는 일반적으로 ANSI 또는 ISO 표준을 기반으로 하지만 각 DBMS에만 적용 됩니다.  
  
-   **데이터 스트림 프로토콜** 데이터 스트림 프로토콜은 DBMS와 클라이언트 간에 전송 되는 데이터의 스트림을 설명 합니다. 예를 들어, 프로토콜에는 첫 번째 바이트가 있어야 스트림의 나머지 부분에는 실행할 SQL 문, 반환 된 오류 값 또는 반환 된 데이터가 포함 될 수 있습니다. 스트림의 나머지 데이터 형식은이 플래그에 따라 달라 집니다. 예를 들어 오류 스트림에는 플래그, 2 바이트 정수 오류 코드, 2 바이트 정수 오류 메시지 길이 및 오류 메시지가 포함 될 수 있습니다.  
  
     데이터 스트림 프로토콜은 논리적 프로토콜 이며 기본 네트워크에서 사용 하는 프로토콜과는 독립적입니다. 따라서 일반적으로 여러 다른 네트워크에서 단일 데이터 스트림 프로토콜을 사용할 수 있습니다. 데이터 스트림 프로토콜은 일반적으로 고유 하며 특정 DBMS를 사용 하도록 최적화 되어 있습니다.  
  
-   **프로세스간 통신 메커니즘** IPC (프로세스 간 통신) 메커니즘은 한 프로세스가 다른 프로세스와 통신 하는 프로세스입니다. 예를 들어 명명 된 파이프, TCP/IP 소켓 및 DECnet 소켓이 있습니다. 선택한 IPC 메커니즘은 사용 중인 운영 체제 및 네트워크에 의해 제한 됩니다.  
  
-   **네트워크 프로토콜** 네트워크 프로토콜은 네트워크를 통해 데이터 스트림을 전송 하는 데 사용 됩니다. 데이터 스트림 프로토콜을 구현 하는 데 사용 되는 IPC 메커니즘을 지 원하는 통로와 파일 전송 및 인쇄 공유와 같은 기본 네트워크 작업을 지 원하는 것으로 간주할 수 있습니다. 네트워크 프로토콜에는 NetBEUI, TCP/IP, DECnet 및 SPX/IPX가 포함 되며 각 네트워크에만 해당 됩니다.
