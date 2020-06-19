---
title: IP 주소 추가 대화 상자(SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistener.addipaddress.f1
ms.assetid: 98c9ad3b-ff3c-4c1d-b344-59a72fca137c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3c06569a6e7363b05139281a9699b72ba37d779c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937207"
---
# <a name="add-ip-address-dialog-box-sql-server-management-studio"></a>IP 주소 추가 대화 상자(SQL Server Management Studio)
   이 F1 도움말 항목에서는 **IP 주소 추가** 대화 상자의 옵션에 대해 설명합니다. 이 대화 상자는 **새 가용성 그룹 수신기** 대화 상자 및 **의** 또는 **의** 복제본 선택 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 페이지에 있는 [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] 수신기 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]탭에서 액세스합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 가용성 그룹 수신기에 서브넷을 추가하려면 각 서브넷의 IP 주소와 IPv4 주소의 서브넷 마스크를 알고 있어야 합니다.  
  
##  <a name="add-ip-address-options"></a><a name="PageOptions"></a> IP 주소 추가 옵션  
 **서브넷**  
 이 드롭 목록을 사용하여 가용성 그룹 수신기에 추가할 서브넷 주소를 선택합니다. 기본적으로 서브넷은 IPv4 주소와 IPv6 주소를 모두 가지고 있습니다. **IP 주소 추가** 대화 상자를 처음 사용하는 경우 **서브넷** 드롭 목록에 가용성 그룹의 복제본을 호스팅하는 각 서브넷에 대한 두 서브넷 주소가 모두 표시됩니다. 지정된 서브넷을 수신기에 추가하려면 서브넷 주소 중 하나를 선택합니다.  
  
 **IP 주소 추가** 대화 상자를 완료한 후 **확인** 을 클릭하여 선택한 서브넷 주소를 수신기에 추가하면 **서브넷** 드롭 목록에서 해당 서브넷 주소가 필터링됩니다. 선택하지 않은 서브넷 주소는 모두 드롭 목록에 남아 있습니다. 서브넷당 하나의 서브넷 주소만 수신기에 추가해야 합니다. 그렇지 않으면 수신기를 만들 수 없습니다.  
  
 **주소**  
 이 필드를 사용하여 선택한 서브넷 주소에 대한 고정 IP 주소를 입력합니다. 이 IP 주소는 네트워크 관리자에게 문의하십시오. 선택한 서브넷 주소에 대한 올바른 주소를 입력해야 합니다. 그렇지 않으면 수신기를 만들 수 없습니다.  
  
 **IPv4 주소**  
 서브넷의 IPv4 서브넷 주소를 선택한 경우 올바른 IPv4 정적 주소를 여기에 입력합니다.  
  
 **서브넷 마스크**  
 IPv4 주소의 경우 이 읽기 전용 필드에 선택한 서브넷의 서브넷 마스크가 표시됩니다.  
  
 **IPv6 주소**  
 서브넷의 IPv6 서브넷 주소를 선택한 경우 올바른 IPv6 정적 주소를 여기에 입력합니다.  
  
 **확인**  
 지정한 고정 IP 주소와 함께 선택한 주소의 서브넷을 추가하려면 클릭합니다. 이러한 값을 포함하는 행이 **새 가용성 그룹 수신기** 또는 **복제본 선택** 대화 상자의 서브넷 표에 추가됩니다.  
  
> [!IMPORTANT]  
>  **IP 주소 추가** 대화 상자에는 IP 주소가 표시되지 않습니다. 또한 가용성 그룹 수신기에 이미 추가한 서브넷에 대한 두 번째 서브넷 주소를 이 대화 상자에서 추가할 수 없습니다.  
  
 **취소**  
 선택을 취소하고 서브넷에 대한 고정 IP 주소를 추가하지 않고 **새 가용성 그룹 수신기** 대화 상자 또는 **수신기** 탭으로 돌아가려면 클릭합니다.  
  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [AlwaysOn 클라이언트 연결(SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
