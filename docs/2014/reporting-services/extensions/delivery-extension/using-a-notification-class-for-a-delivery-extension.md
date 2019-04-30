---
title: 배달 확장 프로그램에 대해 Notification 클래스 사용 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: db6467b21f84a80bb14a5e6ccad30e16d7cfb584
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180396"
---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>배달 확장 프로그램에 대해 Notification 클래스 사용
  <xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스는 <xref:Microsoft.ReportingServices.Interfaces> 네임스페이스에 있으며 배달 확장 프로그램에서 보고서 배달을 위해 사용하는 구독 정보를 나타냅니다. <xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스는 배달용 보고서 렌더링, 알림 상태 결정 및 사용자 데이터 설정 작업을 수행하는 데 사용할 수 있는 다수의 속성을 제공합니다.  
  
 ![보고서 알림 프로세스](../../media/bk-ext-03.gif "보고서 알림 프로세스")  
배달의 핵심 개체인 알림  
  
 사용자 지정 배달 확장 프로그램을 사용하는 구독과 연결된 이벤트가 발생할 경우 <xref:Microsoft.ReportingServices.Interfaces.Report> 개체가 포함된 알림이 만들어집니다. <xref:Microsoft.ReportingServices.Interfaces.Report> 개체는 주어진 보고서를 지원되는 렌더링 형식으로 렌더링하는 데 필요한 기능을 캡슐화하며 서버에 있는 보고서 URL 및 보고서 이름과 같이 보고서 특정 속성을 포함합니다. <xref:Microsoft.ReportingServices.Interfaces.Report> 클래스에 대한 자세한 내용은 [배달 확장 프로그램에 대해 보고서 클래스 사용](../delivery-extension/using-the-report-class-for-a-delivery-extension.md)을 참조하세요.  
  
 <xref:Microsoft.ReportingServices.Interfaces.Notification> 개체를 배달 확장 프로그램의 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드에 전달합니다. <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드에는 알림을 처리하고 보고서를 배달하기 위한 특정 코드가 포함되어 있어야 합니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.Notification> 클래스 사용 방법에 대한 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="retry-functionality"></a>다시 시도 기능  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서는 즉시 배달할 수 없는 알림에 대해 재시도 큐를 만들 수 있습니다. 보고서 서버에서 배달 확장 프로그램의 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> 메서드를 호출하고 나면 배달 확장 프로그램은 보고서 서버에서 나중에 배달을 다시 시도하도록 요청할 수 있습니다. 이 경우 보고서 서버에서 알림을 내부 큐에 두고 일정 시간이 경과한 후 배달을 다시 시도합니다. 관리자는 **MaxNumberOfRetries** XML 요소 및 **PeriodBetweenRetries** XML 요소를 사용하여 RSReportServer.config 파일의 배달 확장 프로그램 섹션에서 보고서 서버가 수행하는 최대 재시도 횟수 및 간격을 구성할 수 있습니다. 나중에 배달에 성공하거나 다시 시도 최대 횟수에 도달하면 알림이 재시도 큐에서 제거됩니다. 최대 재시도 횟수에 도달한 후 배달에 실패하면 알림이 삭제됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [배달 확장 프로그램 구현](../delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
