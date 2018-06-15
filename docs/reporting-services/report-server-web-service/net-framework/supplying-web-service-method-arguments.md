---
title: 웹 서비스 메서드 인수 제공 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a273ce7fb8ddcb53545c4fe95db8e6062a1e5b45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025410"
---
# <a name="supplying-web-service-method-arguments"></a>웹 서비스 메서드 인수 제공
  보고서 서버 웹 서비스 메서드는 HTTP를 통해 SOAP을 사용하여 주어진 URL에 있는 서비스에 요청을 보냅니다. 서비스에서는 요청을 수신하고 처리한 다음 응답을 반환합니다. 이러한 요청과 응답은 XML 문서 형식입니다.  
  
## <a name="optional-parameters"></a>선택적 매개 변수  
 경우에 따라 웹 서비스 메서드에는 선택적인 입력 매개 변수가 있을 수 있습니다. 웹 서비스 메서드에 대한 입력 매개 변수가 선택 사항인 경우에도 해당 매개 변수를 포함시키고 매개 변수 값을 **null**([!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]의 경우 **Nothing**)로 설정해야 합니다. 매개 변수 값을 **null**로 설정하면 SOAP 요청에서 해당 매개 변수에 대한 요소 값이 **null**로 설정됩니다.  
  
 다음 예에서는 <xref:ReportService2010.ReportingService2010.CreateFolder%2A> 메서드를 사용하여 Sales 폴더에 Product Sales라는 새 폴더를 만듭니다. 폴더 속성에 대해 **null** 값을 제공하여 폴더에 대한 사용자별 속성을 제공하지 않습니다.  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>복합 데이터 형식  
 보고서 웹 서비스의 핵심 클래스는 <xref:ReportService2010.ReportingService2010>이며, 이를 사용하여 프록시 클래스의 SOAP 작업 또는 웹 메서드를 호출합니다. 이 클래스와 해당 메서드를 지원하기 위해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 웹 서비스 메서드의 입출력 매개 변수를 위한 특정 사용자 정의 복합 데이터 형식이 포함되어 있습니다. 이러한 복합 데이터 형식은 생성된 프록시 클래스의 일부이며, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 환경에서 개발할 때 사용할 수 있습니다.  
  
 프록시 클래스를 생성하면 WSDL 파일에 정의된 복합 데이터 형식이 해당 프록시의 클래스에 의해 나타나며, 여기에는 복합 데이터 형식의 다양한 SOAP 요소에 해당하는 속성이 포함됩니다. 이러한 데이터 형식의 시퀀스는 코드에서 열거할 수 있는 개체 배열이 됩니다. 그러면 SOAP 메시지로 전송된 XML 구조를 직접 사용하여 작업할 필요가 없습니다. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에서 자동으로 변환이 처리됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조&#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
