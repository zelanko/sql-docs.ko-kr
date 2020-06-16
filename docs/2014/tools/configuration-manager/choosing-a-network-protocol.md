---
title: 네트워크 프로토콜 선택 | Microsoft Docs
description: 공유 메모리, TCP/IP 및 명명 된 파이프와 같은 SQL Server 데이터베이스 엔진에 연결 하는 데 사용할 수 있는 네트워크 프로토콜을 비교 하 고 대조 합니다.
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0b1212117f5428da0a2b1a8e01232a2b97e5cc12
ms.sourcegitcommit: c8e45e0fdab8ea2ae1c7e709346354576b18ca1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84716700"
---
# <a name="choosing-a-network-protocol"></a>네트워크 프로토콜 선택
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 연결하려면 네트워크 프로토콜을 사용할 수 있어야 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 동시에 여러 프로토콜에 대 한 요청을 처리 합니다. 클라이언트에서는 단일 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결합니다. 클라이언트 프로그램에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 수신하는 프로토콜을 알지 못하는 경우 여러 프로토콜을 순서대로 시도하도록 클라이언트를 구성하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 네트워크 프로토콜을 설정, 해제 및 구성할 수 있습니다.  
  
## <a name="shared-memory"></a>공유 메모리  
 공유 메모리는 가장 간단한 프로토콜이며 구성 가능한 설정이 없습니다. 공유 메모리 프로토콜을 사용하는 클라이언트는 동일한 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에만 연결할 수 있으므로 대부분의 데이터베이스 작업에 유용하지 않습니다. 다른 프로토콜이 제대로 구성되지 않는 것으로 의심되는 경우 문제 해결에 공유 메모리 프로토콜을 사용하십시오.  
  
> [!NOTE]  
>  MDAC 2.8 또는 이전 버전을 사용하는 클라이언트에서는 공유 메모리 프로토콜을 사용할 수 없으며 이를 사용하려고 시도하면 자동으로 명명된 파이프 프로토콜로 전환됩니다.  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP는 인터넷에서 광범위하게 사용되는 일반적인 프로토콜입니다. TCP/IP는 다양한 하드웨어 아키텍처 및 운영 체제가 있는 컴퓨터의 상호 연결된 네트워크를 통해 통신합니다. TCP/IP는 네트워크 트래픽의 라우팅을 위한 표준을 포함하며 고급 보안 기능을 제공합니다. TCP/IP는 현재 비즈니스에서 가장 많이 사용되는 프로토콜입니다. 컴퓨터에서 TCP/IP를 사용하도록 구성하는 과정은 복잡할 수 있지만 대부분의 네트워크 컴퓨터에 이미 올바르게 구성되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에 표시되지 않은 TCP/IP 설정을 구성하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 문서를 참조하십시오.  
  
## <a name="named-pipes"></a>명명된 파이프  
 명명된 파이프는 LAN(Local Area Network)을 위해 개발된 프로토콜입니다. 메모리의 일부는 한 프로세스에서 다른 프로세스로 정보를 전달하는 데 사용됩니다. 즉, 한 곳의 출력은 다른 곳의 입력이 됩니다. 두 번째 프로세스는 로컬(첫 번째와 동일한 컴퓨터에서) 또는 원격(네트워크 컴퓨터에서)일 수 있습니다.  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>명명된 파이프 대 TCP/IP 소켓  
 고속 LAN(Local Area Network) 환경에서 TCP/IP(Transmission Control Protocol/Internet Protocol) 소켓 및 명명된 파이프 클라이언트를 성능 측면에서 비교할 수 있습니다. 그러나 TCP/IP 소켓 및 명명된 파이프 클라이언트 간의 성능 차이는 WAN(Wide Area Networks) 또는 전화 접속 네트워크와 같이 느린 네트워크에서 명백하게 드러납니다. 이것은 피어 간 통신에 사용되는 IPC(Interprocess Communication) 메커니즘의 차이 때문입니다.  
  
 명명된 파이프에서 네트워크 통신은 일반적으로 좀 더 대화형입니다. 피어에서는 다른 피어가 읽기 명령으로 요청하기 전에 데이터를 보내지 않습니다. 네트워크 읽기 작업에서는 일반적으로 데이터를 읽기 전에 일련의 명명된 파이프 메시지 피킹이 수행됩니다. 이는 느린 네트워크에서 매우 많은 비용을 소요할 수 있으며 과도한 네트워크 트래픽으로 다른 네트워크 클라이언트에게 영향을 줍니다.  
  
 통신의 대상이 로컬 파이프인지 또는 네트워크 파이프인지를 명확하게 하는 것도 중요합니다. 서버 애플리케이션이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 실행하는 컴퓨터에서 로컬로 실행되는 경우 로컬 명명된 파이프 프로토콜을 선택할 수 있습니다. 로컬 명명된 파이프는 커널 모드로 실행되며 매우 빠릅니다.  
  
 TCP/IP 소켓에서의 데이터 전송은 좀 더 효율적이며 오버헤드도 적습니다. 또한 데이터 전송 시 창 작업, 지연된 승인 등과 같은 TCP/IP Sockets 성능 강화 메커니즘을 사용할 수 있으므로 느린 네트워크에서 특히 유용합니다. 애플리케이션 유형에 따라 이러한 성능 차이는 중요할 수 있습니다.  
  
 TCP/IP 소켓은 백로그 큐도 지원합니다. 따라서 파이프 사용량이 많을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하려고 하면 오류가 발생할 수 있는 명명된 파이프에 비해 전송을 원활하게 하는 제한적인 효과를 제공합니다.  
  
 일반적으로 TCP/IP는 느린 LAN, WAN 또는 전화 접속 네트워크에 적절하며 명명된 파이프는 네트워크 속도가 문제되지 않는 경우 더 많은 기능과 편리한 사용 및 구성 옵션을 제공합니다.  
  
## <a name="enabling-the-protocol"></a>프로토콜 사용  
 프로토콜은 작업할 클라이언트 및 서버 양쪽에서 설정되어야 합니다. 서버는 사용 가능한 모든 프로토콜에서 동시에 요청을 수신할 수 있습니다. 클라이언트 컴퓨터에서는 한 개의 프로토콜을 선택하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 마법사에 나열된 순서로 프로토콜 사용을 시도할 수 있습니다.  
  
 프로토콜을 구성하고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결하는 방법에 대한 간략한 자습서는 [자습서: 데이터베이스 엔진 시작](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)을 참조하세요.  
  
  
