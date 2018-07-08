---
title: SOAP API 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Web service [Reporting Services], WSDL
- Web service [Reporting Services], SOAP
- calling Web service
- SOAP [Reporting Services], accessing
- Report Server Web service, SOAP
- Web service [Reporting Services], WSDL
- WSDL [Reporting Services]
- XML Web service [Reporting Services], SOAP
- Report Server Web service, WSDL
- referencing WSDL
ms.assetid: 63bb870a-4dbf-46bd-8921-78f8ebe5fd75
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: afce018e4e177d9ac7283b488b3222cbc3dae1e2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230233"
---
# <a name="accessing-the-soap-api"></a>SOAP API 액세스
  보고서 서버 웹 서비스는 HTTP를 통한 SOAP(Simple Object Access Protocol)을 사용하며 클라이언트 프로그램과 보고서 서버 간의 통신 인터페이스 역할을 합니다. 웹 서비스는 보고서 실행용과 보고서 관리용으로 끝점을 두 개 제공하며 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 전체 기능에 액세스하는 데 사용할 수 있는 메서드 및 복합 형식 개체 집합으로 구성됩니다. 서비스를 호출하려면 Reporting Services WSDL(웹 서비스 기술 언어)을 참조해야 합니다.  
  
## <a name="referencing-the-reporting-services-wsdl"></a>Reporting Services WSDL 참조  
 웹 서비스를 성공적으로 호출하려면 서비스에 액세스하는 방법, 서비스에서 지원하는 작업, 서비스에 필요한 매개 변수, 서비스에서 반환하는 내용 등에 대해 알고 있어야 합니다. WSDL은 이러한 정보를 컴퓨터에서 읽거나 처리할 수 있는 XML 문서로 제공합니다.  
  
 보고서 서버 웹 서비스는 세 가지 끝점으로 표시되며, WSDL 파일의 이름은 각 끝점에 대해 서로 다릅니다. <xref:ReportService2010> 끝점은 기본 모드 또는 SharePoint 통합 모드에서 보고서 서버의 개체를 관리하는 메서드를 포함합니다. 이 끝점에 대한 WSDL은 `ReportService2010.asmx?wsdl.`을 통해 액세스됩니다.  
  
> [!NOTE]  
>  <xref:ReportService2005> 및 <xref:ReportService2006> 끝점은 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서 더 이상 사용되지 않습니다. <xref:ReportService2010> 끝점에는 두 끝점의 기능이 모두 포함되어 있으며 추가 관리 기능도 포함되어 있습니다.  
  
-   <xref:ReportExecution2005> 끝점을 통해 개발자는 보고서 서버의 보고서를 프로그래밍 방식으로 처리하고 렌더링할 수 있습니다. 이 끝점에 대한 WSDL은 `ReportExecution2005.asmx?wsdl`을 통해 액세스됩니다.  
  
 WSDL은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK와 같이 SOAP 및 웹 서비스를 지원하는 개발 키트에서 사용할 수 있습니다.  
  
 다음 예는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 관리 WSDL 파일에 대한 URL의 형식을 보여 줍니다.  
  
```  
http://server/reportserver/ReportService2010.asmx?wsdl  
```  
  
 다음 표에서는 URL의 각 요소에 대해 설명합니다.  
  
|URL 요소|Description|  
|-----------------|-----------------|  
|*server*|보고서 서버가 배포된 서버의 이름입니다.|  
|*reportserver*|XML 웹 서비스가 포함된 폴더의 이름입니다. 이 폴더는 설치 중 구성됩니다.|  
|*\<endpoint name>.asmx*|웹 서비스 끝점의 이름입니다.|  
  
 WSDL 형식에 대한 자세한 내용은 http://www.w3.org/TR/wsdl에서 W3C(World Wide Web 컨소시엄) WSDL 사양을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [웹 서비스와 .NET Framework를 사용하여 응용 프로그램 빌드](net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [보고서 서버 웹 서비스](report-server-web-service.md)  
  
  
