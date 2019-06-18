---
title: 배달 확장 프로그램에 대한 IDeliveryExtension 인터페이스 구현 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 229d08da8be91a462b243fbb5580395fd03867ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193636"
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>배달 확장 프로그램에 대한 IDeliveryExtension 인터페이스 구현
  배달 확장 프로그램 클래스는 알림 내용을 기준으로 사용자에게 보고서 알림을 배달하는 데 사용됩니다. 배달 확장 프로그램 클래스는 배달 확장 프로그램에 전달되는 사용자 설정을 검사하기 위한 인프라도 제공합니다. 또한 배달 확장 프로그램 클래스에는 클라이언트가 확장 프로그램의 이름, 확장 프로그램에서 지원하는 설정, 배달 확장 프로그램에서 사용 가능한 렌더링 형식 등에 대한 정보를 얻는 데 사용할 수 있는 특정 속성이 포함되어야 합니다.  
  
 ![IDeliveryExtension 인터페이스 프로세스](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "IDeliveryExtension 인터페이스 프로세스")  
IDeliveryExtension 인터페이스를 통해 사용자 데이터의 검사가 가능하며 클라이언트에서는 필수 배달 설정에 대한 정보를 얻을 수 있습니다.  
  
 배달 확장 프로그램 클래스를 만들려면 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 및 <xref:Microsoft.ReportingServices.Interfaces.IExtension>을 구현합니다. **IDeliveryExtension** 인터페이스를 통해 배달 확장 프로그램에서 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드를 사용하여 보고서 알림을 배달하고 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A> 메서드를 사용하여 수신되는 확장 프로그램 설정을 검사할 수 있습니다. **IExtension** 인터페이스를 통해서는 배달 확장 프로그램에서 지역화된 확장 프로그램 이름을 구현하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 파일에 저장된 확장 프로그램별 구성 정보를 처리할 수 있습니다. **IExtension**을 구현하면 배달 확장 프로그램에 <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A> 속성이 포함됩니다. [!INCLUDE[ssRS](../../../includes/ssrs.md)] 배달 확장 프로그램이 **LocalizedName** 속성을 지원하는 것이 좋으며, 그럴 경우 사용자 인터페이스에서 확장 프로그램에 대해 보고서 관리자와 같은 친숙한 이름이 사용자에게 표시됩니다.  
  
 배달 확장 프로그램에서는 **IDeliveryExtension** 인터페이스의 **ExtensionSettings** 속성도 구현해야 합니다. 보고서 서버에서는 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 속성에 의해 반환된 값을 사용하여 배달 확장 프로그램에 필요한 설정을 평가합니다. 배달 확장 프로그램과 상호 작용하는 클라이언트에서는 보고서 서버 웹 서비스의 <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> 메서드를 사용하여 배달 확장 프로그램에 대한 설정 목록을 반환합니다.  
  
 또한 배달 확장 프로그램 클래스를 사용하여 RSReportServer.config 파일에 저장된 사용자 지정 구성 데이터를 검색하고 처리할 수 있습니다. 사용자 지정 구성 데이터를 처리하는 방법은 <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A> 메서드를 참조하십시오.  
  
 예제 **IDeliveryExtension** 클래스 구현은 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
