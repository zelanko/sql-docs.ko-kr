---
title: "배달 확장 프로그램에 대 한 알림 클래스를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 064d5556dca130324f69dd49d14f3caa76c8eec8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>배달 확장 프로그램에 대해 Notification 클래스 사용
  <xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스는 <xref:Microsoft.ReportingServices.Interfaces> 네임스페이스에 있으며 배달 확장 프로그램에서 보고서 배달을 위해 사용하는 구독 정보를 나타냅니다. <xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스는 배달용 보고서 렌더링, 알림 상태 결정 및 사용자 데이터 설정 작업을 수행하는 데 사용할 수 있는 다수의 속성을 제공합니다.  
  
 ![보고서 알림 프로세스](../../../reporting-services/extensions/delivery-extension/media/bk-ext-03.gif "알림 프로세스를 보고 합니다.")  
배달의 핵심 개체인 알림  
  
 사용자 지정 배달 확장 프로그램을 사용하는 구독과 연결된 이벤트가 발생할 경우 <xref:Microsoft.ReportingServices.Interfaces.Report> 개체가 포함된 알림이 만들어집니다. <xref:Microsoft.ReportingServices.Interfaces.Report> 개체는 주어진 보고서를 지원되는 렌더링 형식으로 렌더링하는 데 필요한 기능을 캡슐화하며 서버에 있는 보고서 URL 및 보고서 이름과 같이 보고서 특정 속성을 포함합니다. 에 대 한 자세한 내용은 <xref:Microsoft.ReportingServices.Interfaces.Report> 클래스를 참조 하십시오. [Report 클래스를 사용 하 여 배달 확장 프로그램에 대 한](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)합니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.Notification> 개체를 배달 확장 프로그램의 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드에 전달합니다. <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드에는 알림을 처리하고 보고서를 배달하기 위한 특정 코드가 포함되어 있어야 합니다.  
  
 사용 하는 방법의 예는 <xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스를 참조 하십시오. [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
## <a name="retry-functionality"></a>다시 시도 기능  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서는 즉시 배달할 수 없는 알림에 대해 재시도 큐를 만들 수 있습니다. 보고서 서버에서 배달 확장 프로그램의 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드를 호출하고 나면 배달 확장 프로그램은 보고서 서버에서 나중에 배달을 다시 시도하도록 요청할 수 있습니다. 이 경우 보고서 서버에서 알림을 내부 큐에 두고 일정 시간이 경과한 후 배달을 다시 시도합니다. 관리자는 보고서 서버에서 수행 하는 재시도 횟수 및 사용 하 여 RSReportServer.config 파일의 배달 확장 프로그램 섹션에서 기간 최대 수를 구성할 수 있습니다는 **MaxNumberOfRetries** XML 요소 및 **PeriodBetweenRetries** XML 요소입니다. 나중에 배달에 성공하거나 다시 시도 최대 횟수에 도달하면 알림이 재시도 큐에서 제거됩니다. 최대 재시도 횟수에 도달한 후 배달에 실패하면 알림이 삭제됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [배달 확장 프로그램 구현](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

