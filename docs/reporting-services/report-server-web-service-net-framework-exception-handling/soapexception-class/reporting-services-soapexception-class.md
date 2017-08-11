---
title: "Reporting Services SoapException 클래스 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e24a518bee7b192505fc93ad26d4345f9d710143
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="reporting-services-soapexception-class"></a>Reporting Services SoapException 클래스
  발생할 수 있다고 판단되는 특정 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 오류를 해결해야 합니다. 예를 들어, 사용자에게 폴더를 만들도록 요구하는 응용 프로그램에서 사용자는 이미 존재하는 폴더를 만들려고 시도할 수 있습니다. 개발자는 사용자가 응용 프로그램의 폴더 이름 및 경로 필드에 입력하는 내용을 제어하지 못하지만, 누군가가 실수로 이미 존재하는 항목을 만들려고 시도할 때 발생하는 사용자 경험은 제어할 수 있습니다.  
  
 특정 오류 조건을 catch를 쉽게 수행할 수 있도록 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 분류에서 속성을 사용 하 여 오류를 반환 하 고 분류 하는 예외에 대 한 오류 코드는 **SoapException** 클래스입니다. 자세한 내용은 "SoapException 클래스"를 참조는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 설명서입니다.  
  
 다음 표에서의 공용 속성을 나열는 **SoapException** 클래스입니다.  
  
|공용 속성|Description|  
|---------------------|-----------------|  
|**행위자**|예외를 발생시킨 코드입니다. 값은 웹 서비스 메서드에 대한 URL입니다.|  
|**세부 정보**|응용 프로그램별 오류 정보입니다. 값은 보고서 서버에서 설정되며 XML 형식입니다. 자세한 내용은 참조 [Detail 속성](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md) 및 [특정 오류 처리에 Detail 속성을 사용 하 여](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)합니다.|  
|**HelpLink**|오류와 연관된 도움말 파일에 대한 URL 또는 URN입니다. 일반적으로 웹 서비스에서 설정되는 이 값은 URL을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 도움말 및 지원으로 설정합니다. 때문에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 여러 도움말 링크는 보고서 서버 설정 도움말 발생 하는 오류에 대 한 지원의 일환으로 정보를 연결는 **세부** 속성입니다. 자세한 내용은 참조 [HelpLink 요소](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)합니다.|  
|**메시지**|오류를 설명하는 지역화된 메시지입니다. 이 텍스트는 응용 프로그램 UI로 나타날 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services의 예외 처리 소개](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [SoapException 오류 테이블](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
