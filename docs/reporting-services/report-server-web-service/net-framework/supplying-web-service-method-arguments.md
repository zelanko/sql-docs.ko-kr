---
title: "웹 서비스 메서드 인수를 제공 합니다. | Microsoft Docs"
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 761571f88c2321c823dc240cfa9bb3ba75d9414b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="supplying-web-service-method-arguments"></a>웹 서비스 메서드 인수 제공
  보고서 서버 웹 서비스 메서드는 HTTP를 통해 SOAP을 사용하여 주어진 URL에 있는 서비스에 요청을 보냅니다. 서비스에서는 요청을 수신하고 처리한 다음 응답을 반환합니다. 이러한 요청과 응답은 XML 문서 형식입니다.  
  
## <a name="optional-parameters"></a>선택적 매개 변수  
 경우에 따라 웹 서비스 메서드에는 선택적인 입력 매개 변수가 있을 수 있습니다. 웹 서비스 메서드에 대 한 입력된 매개 변수는 선택 사항, 경우에 여전히 포함 하며 매개 변수 값을 설정 **null** (**Nothing** 에 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). 매개 변수 값을 설정 **null** SOAP 요청에 해당 매개 변수에 대해 요소 값을 설정 **null**합니다.  
  
 다음 예에서는 <xref:ReportService2010.ReportingService2010.CreateFolder%2A> 메서드를 사용하여 Sales 폴더에 Product Sales라는 새 폴더를 만듭니다. 제공 하 여 한 **null** 폴더에 대 한 사용자 고유의 속성이 폴더 속성에 대 한 값이 제공 됩니다.  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>복합 데이터 형식  
 보고서 웹 서비스의 핵심 클래스는 <xref:ReportService2010.ReportingService2010>이며, 이를 사용하여 프록시 클래스의 SOAP 작업 또는 웹 메서드를 호출합니다. 이 클래스와 해당 메서드를 지원하기 위해 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 웹 서비스 메서드의 입출력 매개 변수를 위한 특정 사용자 정의 복합 데이터 형식이 포함되어 있습니다. 이러한 복잡 한 데이터 형식에서 개발할 때 사용할 수 있는 생성 된 프록시 클래스의 일부인는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 환경입니다.  
  
 프록시 클래스를 생성하면 WSDL 파일에 정의된 복합 데이터 형식이 해당 프록시의 클래스에 의해 나타나며, 여기에는 복합 데이터 형식의 다양한 SOAP 요소에 해당하는 속성이 포함됩니다. 이러한 데이터 형식의 시퀀스는 코드에서 열거할 수 있는 개체 배열이 됩니다. 그러면 SOAP 메시지로 전송된 XML 구조를 직접 사용하여 작업할 필요가 없습니다. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]에서 자동으로 변환이 처리됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
