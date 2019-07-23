---
title: 인터넷을 통한 복제 보안 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: acefbae5081033347a34ab5c116b5bbe07fce8c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051858"
---
# <a name="securing-replication-over-the-internet"></a>Securing Replication Over the Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  인터넷을 통한 복제는 특히 모바일 구독자에게 유용하지만 적절한 보안을 유지하려면 인터넷 복제를 알맞게 구성해야 합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 다음 두 가지 기술 중 하나를 통해 인터넷에서 정보를 안전하게 공유할 것을 권장합니다.  
  
-   VPN(가상 프라이빗 네트워크)  
  
-   병합 복제를 위한 웹 동기화 옵션  
  
## <a name="virtual-private-network"></a>가상 프라이빗 네트워크  
 가상 프라이빗 네트워크는 인터넷을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터를 복제하는 경우 간단하고 안전한 계층 방식을 제공합니다. 인터넷을 통한 VPN 연결은 논리적으로 사이트 간에 WAN(광역 통신망)으로 운영됩니다.  
  
 그러기 위해서는 사용자가 인터넷이나 다른 공용 네트워크( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 버전 4.0 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 운영 체제에서 사용할 수 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 지점 간 터널링 프로토콜(PPTP)이나 Windows 2000 운영 체제에서 사용할 수 있는 계층 2 터널링 프로토콜(L2TP)과 같은 프로토콜을 사용하는 네트워크)를 통해 터널링할 수 있도록 허용해야 합니다. 이 프로세스는 프라이빗 네트워크에서 사용할 수 있는 것과 유사한 보안 및 기능을 제공합니다.  
  
 VPN 설정 방법은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 설명서를 참조하십시오.  
  
## <a name="web-synchronization-through-iis"></a>IIS를 통한 웹 동기화  
 병합 복제를 위한 웹 동기화 옵션은 HTTPS 프로토콜을 사용하여 데이터를 복제하는 기능을 제공하며 이 기능은 방화벽을 통해 데이터를 복제하는 편리한 방법이 될 수 있습니다. 웹 동기화 보안에 대한 자세한 내용은 [웹 동기화 구성](../../../relational-databases/replication/configure-web-synchronization.md) 및 [웹 동기화를 위한 보안 아키텍처](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [복제 보안 설정 보기 및 수정](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
