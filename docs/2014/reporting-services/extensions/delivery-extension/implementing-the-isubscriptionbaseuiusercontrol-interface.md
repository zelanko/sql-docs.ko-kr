---
title: 배달 확장 프로그램에 대 한 ISubscriptionBaseUIUserControl 인터페이스 구현 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f87046df4e41f40bc5de5f2a720247738841ff24
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376345"
---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface-for-a-delivery-extension"></a>배달 확장 프로그램에 대한 ISubscriptionBaseUIUserControl 인터페이스 구현
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램에는 보고서 관리자에서 확장 프로그램 관련 정보를 수집하기 위한 구독 UI(사용자 인터페이스) 구현이 포함될 수 있습니다. 이 UI는 사용자가 새 구독을 만들거나 기존 구독을 수정할 때 호출됩니다. 새 구독을 만드는 경우 UI에 적절한 기본값이 표시되고 이를 통해 사용자가 배달 공급자와 상호 작용할 수 있습니다. 구독을 수정하는 경우에는 UI에 현재 구독 정보가 미리 채워집니다.  
  
 배달 확장 프로그램은 구독 UI를 ASP.NET 사용자 컨트롤 형태로 제공합니다. 보고서 서버에서는 구독 UI를 표시할 때 배달 확장 프로그램에서 정의된 사용자 컨트롤을 통합합니다. 이 기능을 가능하게 하는 추상 메서드를 제공하는 기본 인터페이스는 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스입니다. 이 인터페이스는 입력 값 검사와 같은 일반적인 작업이 올바르게 수행되도록 합니다. 또한 기본 사용자 컨트롤은 구독 간의 일관성을 위해 보고서 서버에서 사용되는 기본 속성 집합을 제공합니다. 이러한 속성은 보고서 관리자와 통합되는 배달 확장 프로그램에 필요합니다.  
  
 보고서 관리자에 대한 구독 UI를 만들기 위해 배달 공급자에서 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스를 구현할 수 있습니다. <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스는 사용자가 구독 설정 값을 입력하고 배달 확장 프로그램에 필요한 설정을 처리하고 설정을 확인할 수 있도록 하는 인프라를 제공합니다.  
  
> [!NOTE]  
>  <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스를 배달 확장 프로그램의 일부로 구현할 필요는 없습니다. 대신 배달 확장 프로그램을 사용하는 구독은 항상 SOAP API 메서드 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 및 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>를 통해 만들 수 있습니다. 구독 및 배달 관리를 위한 SOAP API 기능에 대한 자세한 내용은 [구독 및 배달 메서드](../../report-server-web-service/methods/subscription-and-delivery-methods.md)를 참조하세요.  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스는 <xref:Microsoft.ReportingServices.Interfaces.IExtension>을 확장합니다. <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>을 구현하는 사용자 컨트롤도 **System.Web.UI.WebControls.WebControl**에서 상속되어야 합니다. **WebControl** 클래스에 대한 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 개발자 가이드를 참조하세요.  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스 사용 방법에 대한 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [배달 확장 프로그램 구현](implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
