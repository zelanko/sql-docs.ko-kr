---
title: 배달 확장 프로그램 개요 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- subscriptions [Reporting Services], delivery extensions
- delivery extensions [Reporting Services], about extensions
ms.assetid: a30600a9-bbed-4519-9426-3470ff2982e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5bbc5e58b95ffb4eebc5dfa0400a566868ae5cba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63165217"
---
# <a name="delivery-extensions-overview"></a>배달 확장 프로그램 개요
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 사용자가 생성 및 게시 된 보고서를 다양 한 위치로 배달 하는 보고서를 만들고 게시할 수 있습니다. 또한 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에는 다수의 배달 확장 프로그램이 포함되어 있으며 개발자가 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 배달 기능을 더욱 확장할 수 있도록 추가 배달 확장 프로그램을 만들 수 있는 배달 API가 포함되어 있습니다.  
  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 포함된 배달 확장 프로그램을 나열합니다.  
  
|배달 확장 프로그램|Description|  
|------------------------|-----------------|  
|보고서 서버 전자 메일|SMTP 서버를 사용하여 개별 사용자나 그룹에 보고서를 전자 메일로 보냅니다.|  
|보고서 서버 파일 공유|조직 내에서 네트워크 파일 공유 위치로 보고서를 배포하는 데 사용됩니다. 지정된 일정에 따라 파일 공유 위치에 보고서를 자동으로 복사할 수 있는 기능을 제공합니다.|  
  
 ![Reporting Services 배달 확장 프로그램 검토 및 업데이트 프로그램 아키텍처](../../media/bk-reportservicedelivery.gif "Reporting Services 배달 확장 프로그램 검토 및 업데이트 프로그램 아키텍처")  
Reporting Services 배달 확장 프로그램 검토 및 업데이트 프로그램 아키텍처  
  
 배달 확장 프로그램은 구독과 함께 사용됩니다. 사용자는 구독을 만들 때 사용 가능한 배달 확장 프로그램 중 하나를 선택하여 보고서 배달 방법을 결정할 수 있습니다. 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 구독은 보고서 서버 데이터베이스에 있습니다. 이벤트가 발생하면 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서는 보고서 서버 데이터베이스에 포함된 구독에 대해 이벤트를 일치시킵니다. 이벤트와 연결된 각 구독에 대해 보고서 서버에서 알림을 만듭니다. 데이터 기반 구독의 경우 각 받는 사람에 대한 알림이 만들어집니다. 알림이 만들어지면 보고서 서버에서 특정 배달 확장 프로그램을 호출하고 알림에 지정된 확장 프로그램 설정 값을 전달합니다. 배달 확장 프로그램은 선택된 배달 확장 프로그램에서 지정된 대로 사용자에게 알림을 보냅니다.  
  
 배달 확장 프로그램은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 API를 구현합니다. 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램 API를 지원함으로써 배달 확장 프로그램은 보고서 서버에서 알림을 수신하고 알림 상태를 제공할 수 있습니다.  
  
 보고서 서버에서는 알림 및 보고서에 대한 배달 대상을 관리하지 않습니다. 대상 정보 수집은 배달 확장 프로그램에 작성하는 코드를 통해 수행됩니다.  
  
## <a name="subscriptions-and-delivery-extensions"></a>구독 및 배달 확장 프로그램  
 클라이언트 애플리케이션에서는 보고서 서버 웹 서비스의 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 및 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>의 두 메서드를 이용하는 배달 확장 프로그램을 사용하여 구독을 만듭니다. 이미 존재하는 구독을 수정하는 경우에는 <xref:ReportService2010.ReportingService2010.SetSubscriptionProperties%2A> 및 <xref:ReportService2010.ReportingService2010.SetDataDrivenSubscriptionProperties%2A> 메서드가 사용됩니다. 구독을 만들 때 사용자는 또한 구독에 대한 배달 확장 프로그램을 선택하고 필요한 확장 프로그램 설정 값을 입력하기도 합니다. 사용자가 구독을 저장하면 이것은 보고서 서버 데이터베이스에 저장됩니다. 구독에서는 일정이나 이벤트를 기준으로 알림을 만듭니다. 배달이 시작되면 선택된 배달 확장 프로그램이 먼저 구성 파일에서 구성 데이터를 로드합니다. 그런 다음 구독에 대한 확장 프로그램 설정이 검색되고 값이 설정됩니다. 마지막으로 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드가 호출되고 알림이 전송됩니다.  
  
## <a name="developer-requirements"></a>개발자 요구 사항  
 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램을 개발하려면 다음이 필요합니다.  
  
-   보고서 서버가 설치된 배포 컴퓨터가 있어야 합니다.  
  
-   [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK (소프트웨어 개발 키트)가 설치 된 개발 컴퓨터가 있어야 합니다.  
  
-   
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기능, 특히 구독 및 배달에 대해 잘 알고 있어야 합니다.  
  
-   보고서 관리자에 대한 고유의 구독 사용자 인터페이스를 구현하려는 경우에는 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 및 웹 컨트롤에 대해 잘 알고 있어야 합니다.  
  
-   Visual c # 또는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .net과 같은 언어의 개발 환경  
  
## <a name="see-also"></a>참고 항목  
 [배달 확장 프로그램 구현](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
