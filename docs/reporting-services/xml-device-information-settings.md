---
title: "XML 장치 정보 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1264d292be499cf8c70efeea1ef39beed325cd5f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="xml-device-information-settings"></a>XML 장치 정보 설정
  다음 표는 XML 형식으로 렌더링하기 위한 장치 정보 설정을 나열합니다.  
  
|설정|값|세부 정보|  
|-------------|------------|-------------|  
|**XSLT**|XML 파일에 적용할 XSLT의 보고서 서버 네임스페이스 경로입니다(예: **/Transforms/myxslt**).|xsl 파일은 보고서 서버에 게시된 리소스여야 하며 보고서 서버 항목 경로를 통해 이에 액세스해야 합니다. 이 설정의 값은 보고서에 지정된 XSLT에 따라 적용됩니다. **XSLT** 설정이 적용된 경우 **OmitSchema** 설정은 무시됩니다.|  
|**MIMEType**|XML 파일의 MIME(Multipurpose Internet Mail Extensions) 형식입니다.||  
|**UseFormattedValues**|**true**<br /><br /> **false**|XML 데이터를 생성할 때 입력란의 서식 지정된 값을 렌더링할지 여부를 나타냅니다.<br /><br /> false 값은 입력란의 기본 값이 사용됨을 나타냅니다.|  
|**Indented**|**true**<br /><br /> **false**|들여쓰기한 XML을 생성할지 여부를 나타냅니다. 기본값인 **false** 는 들여쓰기 안 한 압축 XML을 생성합니다.|  
|**OmitNamespace**|**true**<br /><br /> **false**|XML에서 기본 네임스페이스를 생략할지 여부를 나타냅니다.<br /><br /> true이면 XML에서 기본 네임스페이스가 지정되지 않습니다.<br /><br /> false이면 XML에서 보고서의 DataSchema 속성 값을 사용하여 기본 네임스페이스가 지정됩니다. DataSchema 속성의 기본값은 보고서 이름입니다.<br /><br /> 기본 값은**false**입니다.|  
|**OmitSchema**|**true**<br /><br /> **false**|XML에서 스키마 위치를 생략할지 여부를 나타냅니다. 이 위치는 SchemaLocation 특성입니다.<br /><br /> OmitSchema의 기본값은 다음과 같이 OmitNamespace 값에 따라 달라집니다.<br /><br /> 기본적으로 OmitNamespace가 False이면 OmitSchema는 **False** 입니다. 사용자는 OmitSchema를 True로 설정하여 기본값을 무시할 수 있습니다.<br /><br /> OmitNamespace가 True이면 OmitSchema는 OmitShema에 대해 명시적으로 구성된 값에 관계없이 **True** 로 동작합니다.|  
|**인코딩**|.NET Framework에서 지원하는 문자 인코딩의 IANA(Internet Assigned Numbers Authority) 이름입니다.|기본값은 **UTF-8**입니다. 다른 값의 예로 ASCII, UTF-7 및 UTF-16을 들 수 있습니다.|  
|**FileExtension**|생성된 파일에 사용할 파일 확장명입니다.||  
|**스키마**|**true** 값은 XML 스키마가 렌더링됨을 나타냅니다. 기본 값은 **false**입니다.|XSD(XML 스키마 정의)가 렌더링되는지 아니면 실제 XML 데이터가 렌더링되는지를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수를 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
