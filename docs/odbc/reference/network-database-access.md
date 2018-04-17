---
title: 네트워크 데이터베이스 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73ade5bb7b34927bddf625eba7512b5ff20735c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="network-database-access"></a>네트워크 데이터베이스 액세스
네트워크를 통해 데이터베이스에 액세스 하는 여러 독립적인, 각각 및 프로그래밍 인터페이스 아래에 있는 구성 요소 필요 합니다. 이러한 구성 요소는 다음 그림에 표시 됩니다.  
  
 ![구성 요소는 네트워크를 통해 데이터베이스에 액세스 하려면](../../odbc/reference/media/pr04.gif "pr04")  
  
 각 구성 요소에 대 한 추가 설명은 다음과 같습니다.  
  
-   **인터페이스를 프로그래밍할** 이 단원의 앞에서 설명한 대로 프로그래밍 인터페이스 응용 프로그램에 의해 수행 된 호출을 포함 합니다. 이러한 인터페이스 (SQL, SQL 포함 된 모듈과 호출 수준 인터페이스)는 일반적으로 ANSI 또는 ISO 표준을 기반으로 하지만 각 DBMS에 일반적으로 한정 됩니다.  
  
-   **데이터 스트림 프로토콜** DBMS와 해당 클라이언트 간에 전송 되는 데이터 스트림의 데이터 스트림 프로토콜에 설명 합니다. 예를 들어 프로토콜 스트림의 나머지 부분에 있는 설명 하기 위해 첫 번째 바이트를 필요할 수 있습니다: SQL 문 실행 시 반환 된 오류 값 또는 데이터를 반환 합니다. 나머지 스트림의 데이터의 형식은 다음이 플래그에 의존 합니다. 예를 들어 오류 스트림에 플래그, 2 바이트 정수 오류 코드, 2 바이트 정수 오류 메시지 길이 및 오류 메시지가 포함 될 수 있습니다.  
  
     데이터 스트림 프로토콜은 논리 프로토콜와 내부 네트워크에서 사용 되는 프로토콜의 관련이 없습니다. 따라서 단일 데이터 스트림을 프로토콜 다양 한 서로 다른 네트워크에 일반적으로 사용할 수 있습니다. 데이터 스트림은 일반적으로 고유의 프로토콜과 특정 DBMS와 작동 하도록 최적화 되었습니다.  
  
-   **통신 메커니즘의 프로세스 간** (IPC) 프로세스 간 통신 메커니즘은 다른 한 프로세스가 통신 하는 프로세스입니다. 명명 된 파이프, TCP/IP 소켓 및 DECnet 소켓을 예로 들 수 있습니다. IPC 메커니즘 선택은 운영 체제 및 네트워크 사용량에 따라 달라 집니다.  
  
-   **네트워크 프로토콜** 네트워크 프로토콜은 데이터 스트림이 네트워크를 통해 전송 하는 데 사용 됩니다. 작업을 지 원하는 데이터를 구현 하는 데 사용 되는 IPC 메커니즘 파일 전송과 같은 기본 네트워크 작업 지원 뿐만 아니라 프로토콜, 스트림 및 인쇄 공유 처리를 생각할 수 있습니다. 네트워크 프로토콜 NetBEUI, TCP/IP, DECnet 및 SPX/IPX를 포함 하며 각 네트워크에 고유 합니다.
