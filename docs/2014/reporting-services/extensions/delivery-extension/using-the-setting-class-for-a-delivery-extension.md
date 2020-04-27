---
title: 배달 확장 프로그램에 대해 Setting 클래스 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 594cf28391ae4523e1a95ad79ee5b1280ff72218
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63179846"
---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>배달 확장 프로그램에 대해 Setting 클래스 사용
  <xref:Microsoft.ReportingServices.Interfaces.Setting> 클래스는 <xref:Microsoft.ReportingServices.Interfaces> 네임스페이스에 있으며 배달 확장 프로그램에 대한 확장 프로그램 설정 정보를 나타냅니다. <xref:Microsoft.ReportingServices.Interfaces.Setting> 클래스는 배달 확장 프로그램이 제대로 작동하는 데 필요한 설정 정보를 저장하기 위한 인프라를 제공합니다. 예를 들어 보고서 서버 전자 메일 배달에서 사용자는 받는 사람 주소, 보내는 사람 주소, 전자 메일 제목 줄 등과 같이 전자 메일 배달을 위한 특정 설정을 제공해야 합니다. 사용자 지정 배달 공급자의 경우에도 사용자가 배달 확장 프로그램에서 알림 및 보고서를 전달할 수 있도록 특정 설정을 제공해야 합니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.Setting> 클래스는 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> 인터페이스의 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 속성을 구현할 때 사용됩니다. <xref:Microsoft.ReportingServices.Interfaces.Setting> 클래스는 구독 또는 알림이 만들어질 때 사용자가 제공하는 확장 프로그램 설정을 처리하는 데도 사용됩니다.  
  
 <xref:Microsoft.ReportingServices.Interfaces.Setting> 클래스 사용 방법에 대한 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [배달 확장 프로그램 구현](implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
