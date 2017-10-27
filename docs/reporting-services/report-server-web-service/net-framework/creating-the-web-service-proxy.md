---
title: "웹 서비스 프록시를 만드는 | Microsoft Docs"
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
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 1c39d81ec9a1d2cd24f01b9dccfed13e8560a770
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="creating-the-web-service-proxy"></a>웹 서비스 프록시 만들기
  클라이언트와 웹 서비스는 입력 및 출력 매개 변수를 XML로 캡슐화하는 SOAP 메시지를 사용하여 통신할 수 있습니다. 프록시 클래스는 매개 변수를 XML 요소에 매핑한 다음 네트워크를 통해 SOAP 메시지를 보냅니다. 이와 같이 프록시 클래스 덕분에 SOAP 수준에서 웹 서비스와 통신할 필요가 없으며 SOAP 및 웹 프록시를 지원하는 임의의 개발 환경에서 웹 서비스 메서드를 호출할 수 있습니다.  
  
 두 가지 방법으로 사용 하 여 개발 프로젝트에 프록시 클래스를 추가 하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]:에서 WSDL 도구와는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], 및에서 웹 참조를 추가 하 여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]합니다. 다음 섹션에서는 이 두 가지 방법에 대해 자세히 설명합니다.  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>WSDL 도구를 사용하여 프록시 추가  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK에는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 개발 환경에서 사용할 웹 서비스 프록시를 생성할 수 있는 WSDL(웹 서비스 기술 언어) 도구(Wsdl.exe)가 포함되어 있습니다. 웹 서비스를 지 원하는 언어로 클라이언트 프록시를 만들 수는 가장 일반적인 방법은 (현재 C# 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) WSDL 도구를 사용 하는 것입니다.  
  
 **Wsdl.exe를 사용 하 여 프로젝트에 프록시 클래스를 추가 하려면**  
  
1.  명령 프롬프트에서 Wsdl.exe를 사용하여 (최소한) URL을 보고서 서버 웹 서비스에 지정함으로써 프록시 클래스를 만듭니다.  
  
     예를 들어 다음 명령 프롬프트 문은 보고서 서버 웹 서비스의 관리 끝점에 대한 URL을 지정합니다.  
  
    ```  
    wsdl /language:CS /n:"Microsoft.SqlServer.ReportingServices2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     WSDL 도구에서는 프록시 생성을 위해 다수의 명령 프롬프트 인수를 사용합니다. 위의 예에서는 C# 언어 및 웹 서비스 끝점을 두 개 이상 사용하는 경우 이름 충돌 방지를 위해 프록시에 사용하도록 제안된 네임스페이스를 지정하고 ReportingService2010.cs라는 C# 파일을 생성합니다. 이 예에서 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]을 지정한다면 이름이 ReportingService2010.vb인 프록시 파일을 생성하게 됩니다. 이 파일은 명령을 실행하는 위치인 디렉터리에 만들어집니다.  
  
2.  프록시 클래스를 어셈블리 파일(확장명 .dll)에 컴파일하고 이 클래스를 프로젝트에서 참조하거나 프로젝트 항목으로 추가합니다.  
  
    > [!NOTE]  
    >  프록시 클래스를 수동으로 프로젝트에 추가할 경우 System.Web.Services.dll에 대한 참조를 추가해야 합니다. Visual Studio .NET에서 웹 참조를 사용하여 프록시를 추가하는 경우에는 참조가 자동으로 만들어집니다. 자세한 내용은 이 항목의 후반에 나오는 "Visual Studio에서 웹 참조를 사용하여 프록시 추가"를 참조하십시오.  
  
     프록시 클래스를 프로젝트에 항목으로 추가하면 연결된 파일이 솔루션 탐색기에 나타납니다.  
  
3.  서비스를 프로그래밍 방식으로 호출하려면 프록시 클래스의 인스턴스를 만듭니다.  
  
     다음 코드 예제는 프로젝트에서 <xref:ReportService2010.ReportingService2010> 프록시 클래스의 인스턴스를 만들기 위한 구문을 보여 줍니다.  
  
```vb  
Dim service As New ReportingService2010()  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
  
```  
  
 전체 구문을 포함하여 Wsdl.exe 도구에 대한 자세한 내용은 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 설명서의 "WDSL 도구(Web Services Description Language Tool)"를 참조하십시오. 웹 서비스 프록시에 대한 자세한 내용은 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 설명서의 "XML 웹 서비스 프록시 만들기(Creating an XML Web Service Proxy)"를 참조하십시오.  
  
## <a name="adding-the-proxy-using-a-web-reference-in-visual-studio"></a>Visual Studio에서 웹 참조를 사용하여 프록시 추가  
 웹 참조를 통해 프로젝트에서 웹 서비스를 하나 이상 사용할 수 있습니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서는 사용자가 다음의 간단한 단계를 수행하여 웹 서비스 참조를 프로젝트에 추가할 수 있습니다.  
  
 **프로젝트에 웹 참조를 추가 하려면**  
  
1.  **솔루션 탐색기**를 사용 하는 웹 서비스 프로젝트를 선택 합니다.  
  
2.  에 **프로젝트** 메뉴를 클릭 하 여 **웹 참조 추가**합니다.  
  
     **웹 참조 추가** 대화 상자가 열립니다.  
  
3.  에 **URL** 필드를 보고서 서버 웹 서비스의 전체 경로 입력 합니다.  
  
     보고서 서버 웹 서비스의 보고서 실행 끝점에 대한 간단한 URL은 다음과 같습니다.  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     URL에는 보고서 서버 웹 서비스가 배포된 도메인, 서비스가 포함된 폴더의 이름 및 서비스에 대한 검색 파일의 이름이 포함됩니다. 다양 한 URL 요소 설명과 참조 [SOAP API 액세스](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md)합니다.  
  
     웹 서비스에서 제공하는 메서드 및 속성에 대한 설명은 왼쪽의 브라우저 창에 나타납니다.  
  
    > [!NOTE]  
    >  보고서 서버 웹 서비스와 관련 된 항목에 대 한 자세한 내용은 참조 [보고서 서버 웹 서비스 메서드](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)합니다.  
  
4.  프로젝트에서 보고서 서버 웹 서비스를 사용할 수 있고 보고서 서버에 액세스할 수 있는 충분한 권한이 있는지 확인합니다.  
  
5.  에 **웹 참조 이름** 필드에 사용할 이름을 입력 합니다. 보고서 서버 웹 서비스를 프로그래밍 방식으로 액세스 하기 위해 코드에서.  
  
6.  선택 된 **참조 추가** 를 응용 프로그램 웹 서비스에에서 대 한 참조를 만드는 단추입니다.  
  
     새 참조에 표시 **솔루션 탐색기** 현재 프로젝트에 대 한 Web References 노드 아래에 지정 된 대로 라는 **웹 참조 이름** 필드입니다.  
  
7.  **솔루션 탐색기**, 프로젝트의 항목에 사용할 수 있는 웹 참조 클래스에 대 한 네임 스페이스를 확인 하려면 웹 참조 폴더를 확장 합니다.  
  
     웹 참조 폴더 내의 폴더에 표시 됩니다는 관련된 파일을 프로젝트에 대 한 웹 참조를 추가한 후 **솔루션 탐색기**합니다.  
  
 웹 참조를 추가한 후 다음 구문을 사용하여 프록시 클래스의 인스턴스를 만듭니다.  
  
```vb  
Dim rs As New myNamespace.myReferenceName.ReportExecutionService()  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
myNamespace.myReferenceName.ReportExecutionService rs = new myNamespace.myReferenceName.ReportExecutionService();  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
```  
  
 추가할 수도 있습니다는 **를 사용 하 여** (**가져오기** 에 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) 지시문을 보고서 서버 웹 서비스 참조에 있습니다. 이 지시문을 사용할 경우에는 네임스페이스에서 형식을 정규화하지 않아도 됩니다. 이렇게 하려면 다음 코드를 파일에 추가합니다.  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 웹 서비스](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [웹 서비스와.NET Framework를 사용 하 여 응용 프로그램 빌드](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [기술 참조 &#40; Ssrs&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

