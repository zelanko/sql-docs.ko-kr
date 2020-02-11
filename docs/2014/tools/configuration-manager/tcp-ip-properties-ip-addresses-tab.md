---
title: TCP/IP 속성 (IP 주소 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: afb62458cb76a1187dce06efadeca00fc8a382f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151439"
---
# <a name="tcp-ip-properties-ip-addresses-tab"></a>TCP/IP 속성 (IP 주소 탭)
  **TCP/IP 속성(IP 주소 탭)** 대화 상자를 사용하여 특정 IP 주소에 대한 TCP/IP 프로토콜 옵션을 구성할 수 있습니다. **IPAll** 을 선택하면 모든 주소에 대해 **TCP 동적 포트** 및 **TCP 포트**만 동시에 구성할 수 있습니다.  
  
 변경 내용은가 다시 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 될 때 적용 됩니다. SQL Server Browser 서비스를 시작 및 중지하는 방법은 온라인 설명서의 "방법: SQL Server Browser 서비스 시작 및 중지"를 참조하십시오.  
  
## <a name="static-vs-dynamic-ports"></a>정적 포트 대 동적 포트  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기본 인스턴스는 들어오는 연결을 1443번 포트에서 수신합니다. 보안상의 이유 또는 클라이언트 애플리케이션 요구 사항으로 인해 포트를 변경할 수 있습니다. 기본적으로 SQL Server Express를 비롯한 명명된 인스턴스는 동적 포트에서 수신하도록 구성됩니다. 정적 포트를 구성하려면 **TCP 동적 포트** 상자를 비워 놓고 **TCP 포트** 상자에 사용 가능한 포트 번호를 제공합니다. 방화벽에서 포트를 여는 방법은 온라인 설명서에서 SQL Server 액세스를 허용하도록 Windows 방화벽 구성을 참조하십시오.  
  
## <a name="dynamic-ports"></a>동적 포트  
 시작 시 동적 포트에서 수신하도록 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 운영 체제에서 사용 가능한 포트를 확인하고 해당 포트의 엔드포인트를 엽니다. 들어오는 연결은 연결할 포트 번호를 지정해야 합니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 때마다 포트 번호가 변경될 수 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 포트를 모니터링하고 들어오는 연결을 해당 인스턴스의 현재 포트로 보내는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 제공합니다. 동적 포트를 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작할 때 포트 번호가 변경되어 방화벽 설정을 변경해야 할 수 있으므로 방화벽을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하는 것이 복잡해집니다. 방화벽을 통한 연결 문제를 방지하려면 정적 포트를 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 구성하십시오.  
  
## <a name="options"></a>옵션  
 **활성**  
 컴퓨터에서 IP 주소가 활성 상태임을 나타냅니다. **IPAll**에는 사용할 수 없습니다.  
  
 **Enabled**  
 **TCP/IP 속성(프로토콜 탭)** 의 **모두 수신합니다** 속성이 **아니요**로 설정되어 있으면 이 속성은 SQL Server가 IP 주소에서 수신하고 있는지 여부를 나타냅니다. **TCP/IP 속성(프로토콜 탭)** 의 **모두 수신합니다** 속성이 **예**로 설정되어 있으면 이 속성은 무시됩니다. **IPAll**에는 사용할 수 없습니다.  
  
 **IP 주소**  
 이 연결에서 사용하는 IP 주소를 확인 또는 변경합니다. 컴퓨터에서 사용하는 IP 주소 및 IP 루프백 주소 127.0.0.1을 나열합니다. **IPAll**에는 사용할 수 없습니다. IP 주소는 IPv4 또는 IPv6 형식일 수 있습니다.  
  
 **IPAll**  
 동적 포트를 사용할 수 없는 경우 빈칸입니다. 동적 포트를 사용하려면 0으로 설정하십시오.  
  
 **IPAll**의 경우 사용된 동적 포트의 포트 번호를 표시합니다.  
  
 **TCP 동적 포트**  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 수신하는 포트를 확인 또는 변경합니다. 기본적으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 기본 인스턴스는 1443번 포트에서 수신합니다.  
  
 
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 동일한 IP 주소에서 여러 포트를 수신할 수 있으며 1433,1500,1501의 형식으로 각 포트를 쉼표로 구분하여 나열합니다. 이 필드는 2047자로 제한됩니다.  
  
 여러 포트를 수신하도록 단일 IP 주소를 구성하려면 **TCP/IP 속성** 대화 상자의 **프로토콜 탭**에서 **모두 수신합니다** 매개 변수도 **아니요**로 설정해야 합니다. 자세한 내용은 SQL Server 온라인 설명서의 "방법: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "방법: 여러 TCP 포트에서 수신하도록 데이터베이스 엔진 구성"을 참조하십시오.  
  
## <a name="adding-or-removing-ip-addresses"></a>IP 주소 추가 및 제거  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 사용할 수 있었던 IP 주소를 표시합니다. 사용 가능한 IP 주소가 변경되는 경우로는 네트워크 카드를 추가 또는 제거한 경우, 동적으로 할당한 IP 주소가 만료된 경우, 네트워크 구조를 재구성하는 경우 또는 노트북 컴퓨터를 다른 건물의 네트워크로 연결하는 것과 같이 컴퓨터의 물리적 위치를 변경하는 경우가 있습니다. IP 주소를 변경하려면 **IP 주소** 입력란을 편집하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로토콜 선택](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [SQL Server Browser 서비스](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
