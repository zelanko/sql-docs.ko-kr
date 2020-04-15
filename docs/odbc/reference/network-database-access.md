---
title: 네트워크 데이터베이스 액세스 | 마이크로 소프트 문서
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
ms.openlocfilehash: 2237c725d6fe3696d1f28d80c09f22183f718de8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295586"
---
# <a name="network-database-access"></a>네트워크 데이터베이스 액세스
네트워크를 통해 데이터베이스에 액세스하려면 프로그래밍 인터페이스와 독립적이며 아래에 상주하는 여러 구성 요소가 필요합니다. 이러한 구성 요소는 다음 그림에 나와 있습니다.  
  
 ![네트워크를 통해 데이터베이스에 액세스하는 데 필요한 구성 요소](../../odbc/reference/media/pr04.gif "pr04")  
  
 각 구성 요소에 대한 추가 설명은 다음과 같습니다.  
  
-   **프로그래밍 인터페이스** 이 섹션의 앞에서 설명한 대로 프로그래밍 인터페이스에는 응용 프로그램에서 만든 호출이 포함되어 있습니다. 이러한 인터페이스(임베디드 SQL, SQL 모듈 및 호출 수준 인터페이스)는 일반적으로 ANSI 또는 ISO 표준을 기반으로 하지만 각 DBMS에 만연합니다.  
  
-   **데이터 스트림 프로토콜** 데이터 스트림 프로토콜은 DBMS와 클라이언트 간에 전송되는 데이터 스트림을 설명합니다. 예를 들어 프로토콜은 스트림의 나머지 부분에 포함 된 내용을 설명 하기 위해 첫 번째 바이트를 요구할 수 있습니다.: SQL 문을 실행 하는 SQL 문, 반환 된 오류 값 또는 반환 된 데이터. 그러면 스트림의 나머지 데이터의 형식은 이 플래그에 따라 달라집니다. 예를 들어 오류 스트림에는 플래그, 2바이트 정수 오류 코드, 2바이트 정수 오류 메시지 길이 및 오류 메시지가 포함될 수 있습니다.  
  
     데이터 스트림 프로토콜은 논리적 프로토콜이며 기본 네트워크에서 사용하는 프로토콜과 는 독립적입니다. 따라서, 단일 데이터 스트림 프로토콜은 일반적으로 다수의 상이한 네트워크에서 사용될 수 있다. 데이터 스트림 프로토콜은 일반적으로 독점적이며 특정 DBMS와 함께 작동하도록 최적화되었습니다.  
  
-   **프로세스 간 통신 메커니즘** 프로세스 간 통신(IPC) 메커니즘은 한 프로세스가 다른 프로세스와 통신하는 프로세스입니다. 예를 들어 명명된 파이프, TCP/IP 소켓 및 DECnet 소켓이 있습니다. IPC 메커니즘의 선택은 사용 중인 운영 체제 및 네트워크에 의해 제한됩니다.  
  
-   **네트워크 프로토콜** 네트워크 프로토콜은 네트워크를 통해 데이터 스트림을 전송하는 데 사용됩니다. 데이터 스트림 프로토콜을 구현하는 데 사용되는 IPC 메커니즘을 지원하는 배관뿐만 아니라 파일 전송 및 인쇄 공유와 같은 기본 네트워크 작업을 지원하는 배관으로 간주될 수 있습니다. 네트워크 프로토콜에는 NetBEUI, TCP/IP, DECnet 및 SPX/IPX가 포함되며 각 네트워크에 만연합니다.
