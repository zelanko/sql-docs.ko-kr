---
title: 배달 확장 프로그램 구현 준비 | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- interfaces [Reporting Services]
- delivery extensions [Reporting Services], implementing
ms.assetid: aee1608d-374f-4ad3-bc23-fe07fdaa52b7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 949ab416b0d30f7bb20ec2b797a04121d49b9811
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63193719"
---
# <a name="preparing-to-implement-a-delivery-extension"></a>배달 확장 프로그램 구현 준비
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램을 구현하기 전에 먼저 구현할 인터페이스를 정의해야 합니다. 우선 배달 확장 프로그램을 사용할 방식, 배달 확장 프로그램에 필요한 설정, 보고서 알림을 배달하기 위해 구현할 특정 기능 등을 결정해야 합니다.  
  
 각 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램은 다음 기능을 제공해야 합니다.  
  
-   확장 프로그램 및 지역화된 확장 프로그램 이름을 나타내는 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 인터페이스 구현  
  
-   보고서 알림을 최종 사용자에게 배달하는 데 사용할 수 있는 배달 확장 프로그램을 만드는 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 구현  
  
-   구독에 대한 특정 사용자 데이터를 처리할 수 있는 기능  
  
 각 배달 확장 프로그램은 다음 기능을 포함하도록 개선할 수 있습니다.  
  
-   최종 사용자가 보고서 관리자를 사용하여 배달 확장 프로그램을 사용하는 보고서 구독을 만들 수 있는 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 사용자 컨트롤 구현  
  
 다음 표에서는 배달 확장 프로그램에 대해 사용할 수 있는 인터페이스 및 클래스를 설명합니다.  
  
|인터페이스 또는 클래스|Description|  
|------------------------|-----------------|  
|<xref:Microsoft.ReportingServices.Interfaces.IExtension> 인터페이스|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 확장 프로그램을 나타냅니다.|  
|<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 인터페이스|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 배달 확장 프로그램을 나타냅니다.|  
|<xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 인터페이스|배달 확장 프로그램에 필요한 보고서 서버에 대한 정보를 포함합니다(예: 사용 가능한 렌더링 확장 프로그램 목록).|  
|<xref:Microsoft.ReportingServices.Interfaces.Setting> 클래스|확장 프로그램에 대한 설정을 나타냅니다.|  
|<xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스|배달 확장 프로그램에서 보고서를 배달하는 데 사용하는 구독 정보를 포함합니다.|  
|<xref:Microsoft.ReportingServices.Interfaces.Report> 클래스|배달 확장 프로그램에서 사용자에게 보고서를 배달할 수 있도록 하는 보고서 특정 정보 및 메서드를 나타냅니다.|  
|<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 클래스|렌더링 확장 프로그램의 출력을 나타냅니다. <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 개체에는 렌더링 확장 프로그램에서 반환된 스트림을 처리하기 위해 배달 확장 프로그램에서 요구되는 연관 파일 이름 및 형식 정보가 포함됩니다.|  
|<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 인터페이스|보고서 관리자에서 사용자로부터 전자 메일 주소나 파일 공유 경로 등과 같은 배달 확장 프로그램별 구독 정보를 검색할 수 있는 방법을 나타내는 사용자 컨트롤입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
