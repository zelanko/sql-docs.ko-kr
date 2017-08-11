---
title: "ISubscriptionBaseUIUserControl 인터페이스 구현 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 4e76edaa727df1694a5903e1cc9870c20581c9a0
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface"></a>ISubscriptionBaseUIUserControl 인터페이스 구현
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램에는 보고서 관리자에서 확장 프로그램 관련 정보를 수집하기 위한 구독 UI(사용자 인터페이스) 구현이 포함될 수 있습니다. 이 UI는 사용자가 새 구독을 만들거나 기존 구독을 수정할 때 호출됩니다. 새 구독을 만드는 경우 UI에 적절한 기본값이 표시되고 이를 통해 사용자가 배달 공급자와 상호 작용할 수 있습니다. 구독을 수정하는 경우에는 UI에 현재 구독 정보가 미리 채워집니다.  
  
 배달 확장 프로그램은 구독 UI를 ASP.NET 사용자 컨트롤 형태로 제공합니다. 보고서 서버에서는 구독 UI를 표시할 때 배달 확장 프로그램에서 정의된 사용자 컨트롤을 통합합니다. 이 기능을 가능하게 하는 추상 메서드를 제공하는 기본 인터페이스는 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스입니다. 이 인터페이스는 입력 값 검사와 같은 일반적인 작업이 올바르게 수행되도록 합니다. 또한 기본 사용자 컨트롤은 구독 간의 일관성을 위해 보고서 서버에서 사용되는 기본 속성 집합을 제공합니다. 이러한 속성은 보고서 관리자와 통합되는 배달 확장 프로그램에 필요합니다.  
  
 보고서 관리자에 대한 구독 UI를 만들기 위해 배달 공급자에서 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스를 구현할 수 있습니다. <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스는 사용자가 구독 설정 값을 입력하고 배달 확장 프로그램에 필요한 설정을 처리하고 설정을 확인할 수 있도록 하는 인프라를 제공합니다.  
  
> [!NOTE]  
>  <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스를 배달 확장 프로그램의 일부로 구현할 필요는 없습니다. 대신 배달 확장 프로그램을 사용하는 구독은 항상 SOAP API 메서드 <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> 및 <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>를 통해 만들 수 있습니다. 구독 및 배달 관리 하기 위한 SOAP API 기능에 대 한 자세한 내용은 참조 [Subscription and Delivery Methods](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md)합니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스는 <xref:Microsoft.ReportingServices.Interfaces.IExtension>을 확장합니다. 구현 하는 사용자 정의 컨트롤 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 에서 상속 되어야 **System.Web.UI.WebControls.WebControl**합니다. 에 대 한 자세한 내용은 **WebControl** 클래스를 참조 하십시오. 사용자 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 개발자 가이드입니다.  
  
 사용 하는 방법의 예는 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스를 참조 [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
