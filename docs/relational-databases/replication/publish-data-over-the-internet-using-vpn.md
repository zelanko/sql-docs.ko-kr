---
title: "VPN을 사용하여 인터넷을 통해 데이터 게시 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- VPNs [SQL Server replication]
- Web publishing [SQL Server replication], VPNs
- Internet [SQL Server replication], VPNs
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60900fc1134fbe6da352ff05a30edf4607da9319
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="publish-data-over-the-internet-using-vpn"></a>VPN을 사용하여 인터넷을 통해 데이터 게시
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] VPN(가상 개인 네트워크) 기술을 사용하면 집, 지점, 원격 클라이언트 및 다른 회사에서 사용자가 인터넷을 통해 회사 네트워크에 연결하여 안전하게 통신할 수 있습니다. 사용자는 LAN(근거리 통신망)에서처럼 Windows 인증을 사용할 수 있습니다. 모든 유형의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제는 VPN을 통해 데이터를 복제할 수 있지만 웹 동기화에는 VPN이 필요하지 않으므로 병합 복제를 사용할 경우 웹 동기화 사용을 고려해야 합니다. 자세한 내용은 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)을 참조하세요.  
  
 VPN에는 클라이언트 소프트웨어가 포함되어 있어 컴퓨터에서 인터넷이나 인트라넷(특별한 경우)으로 전용 컴퓨터 또는 서버의 소프트웨어에 연결할 수 있습니다. 사용자 인증 방법 외에도 양쪽 모두에서 암호화할 수도 있습니다. 인터넷을 통한 VPN 연결은 논리적으로 사이트 간에 WAN(광역 통신망)으로 운영됩니다.  
  
 VPN은 다른 네트워크를 사용하여 네트워크의 구성 요소를 연결합니다. 사용자는 인터넷이나 다른 공용 네트워크( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Point-to-Point Tunneling Protocol(PPTP) 또는 Layer Two Tunneling Protocol(L2TP)과 같은 프로토콜 사용)를 통해 터널을 만들어 연결할 수 있습니다. 이 과정은 개인 네트워크에서만 사용할 수 있었던 같은 수준의 보안 및 기능을 제공합니다. PPTP는 Microsoft Windows NT 4.0 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 이상의 운영 체제에서 사용할 수 있으며 L2TP는 Windows 2000 이상에서 사용할 수 있습니다.  
  
 사용자는 인터넷의 중간 라우팅 인프라를 볼 수 없고 데이터는 전용 개인 링크로 전달되는 것처럼 표시됩니다. 사용자가 연결되어 있는 동안 VPN은 사용자 컴퓨터와 회사 서버간에 지점간 연결입니다.  
  
 원격 클라이언트가 VPN을 사용하여 연결하도록 구성하고 클라이언트에 인터넷 액세스 권한이 있어 회사 LAN에 로그인하면 원격 클라이언트가 LAN으로 직접 연결된 것처럼 복제를 구성할 수 있습니다. 보안상의 이유로 VPN을 통해 연결한 사용자와 LAN을 통해 직접 연결한 사용자 간에 서로 다른 네트워크 리소스를 사용하도록 할 수 있습니다.  
  
 VPN 설정 방법은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷을 통한 복제](../../relational-databases/replication/replication-over-the-internet.md)  
  
  
