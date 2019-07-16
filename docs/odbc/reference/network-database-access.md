---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f8eaebca02ef3987e3613b5dd896e0f7c130086
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938030"
---
# <a name="network-database-access"></a>네트워크 데이터베이스 액세스
네트워크를 통해 데이터베이스를 액세스, 구성 요소를 각각의 독립적인 프로그래밍 인터페이스를 아래에 있는 숫자에 필요 합니다. 이러한 구성 요소는 다음 그림에 표시 됩니다.  
  
 ![네트워크를 통해 데이터베이스에 액세스 하려면 구성 요소](../../odbc/reference/media/pr04.gif "pr04")  
  
 각 구성 요소에 대 한 추가 설명은 다음과 같습니다.  
  
-   **프로그래밍 인터페이스가** 이 섹션의 앞부분에서 설명한, 프로그래밍 인터페이스를 포함 응용 프로그램에서 호출 합니다. 이러한 인터페이스 (SQL, SQL에 포함 된 모듈 및 호출 수준 인터페이스)는 일반적으로 ANSI 또는 ISO 표준을 기반으로 하지만 일반적으로 각 DBMS 관련 됩니다.  
  
-   **데이터 Stream 프로토콜** DBMS와 해당 클라이언트 간에 전송 되는 데이터 스트림 하는 데이터 스트림 프로토콜에 설명 합니다. 예를 들어 프로토콜 스트림의 나머지 부분에 있는 설명 하기 위해 첫 번째 바이트 필요할: SQL 문을 반환 된 오류 값을 실행 하거나 데이터를 반환 합니다. 나머지 스트림의 데이터 형식의 다음이 플래그에 따라 다릅니다. 예를 들어 오류 스트림을 플래그를 "," 2 바이트 정수 오류 코드 ",", 2 바이트 정수 오류 메시지 길이 "및" 오류 메시지가 포함 될 수 있습니다.  
  
     데이터 스트림 프로토콜 논리 프로토콜 이며 기본 네트워크에서 사용 하는 프로토콜 독립적입니다. 따라서 단일 데이터 스트림 프로토콜을 다양 한 서로 다른 네트워크에 일반적으로 사용할 수 있습니다. 데이터 스트림 프로토콜은 일반적으로 전용 및 특정 DBMS를 사용 하 여 작동 하도록 최적화 되었습니다.  
  
-   **통신 메커니즘의 프로세스 간** 프로세스 간 통신 (IPC) 메커니즘은 한 프로세스가 다른와 통신 하는 프로세스입니다. 명명 된 파이프, TCP/IP 소켓 및 DECnet 소켓을 예로 들 수 있습니다. IPC 메커니즘의 선택한 운영 체제 및 네트워크를 사용 하 여 제한 됩니다.  
  
-   **네트워크 프로토콜** 네트워크 프로토콜은 네트워크를 통해 데이터 스트림을 전송 하는 데 사용 됩니다. 지원 데이터를 구현 하는 데 사용 되는 IPC 메커니즘 파일 전송 등의 기본 네트워크 작업을 지원할 뿐만 아니라 프로토콜, 스트림 및 인쇄 공유는 배관을 생각할 수 있습니다. 네트워크 프로토콜 NetBEUI, TCP/IP, DECnet 및 SPX/IPX 등이 포함 되며 각 네트워크에 고유 합니다.
