---
title: Windows 애플리케이션에서 SOAP API 사용
description: Reporting Services SOAP API를 사용하여 보고서 서버의 기능에 액세스할 수 있습니다. 서비스를 호출하여 Windows 앱의 웹 서비스에 액세스합니다.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
helpviewer_keywords:
- rendered reports [Reporting Services]
- Windows applications [Reporting Services]
- Windows Forms [Reporting Services]
- SOAP [Reporting Services], Windows applications
ms.assetid: e4804792-20cd-4df2-9257-fb958ff447b4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 78bdfb5335f00df64e1ae3a98a6a34aa26f71881
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198203"
---
# <a name="integrating-reporting-services-using-soap---windows-application"></a>SOAP를 사용하여 Reporting Services 통합 - Windows 애플리케이션
  Reporting Services SOAP API를 통해 보고서 서버의 전체 기능에 액세스할 수 있습니다. SOAP API는 웹 서비스이므로 쉽게 액세스하여 사용자 지정 비즈니스 애플리케이션에 엔터프라이즈 보고 기능을 제공할 수 있습니다. 서비스를 호출하는 코드를 작성하기만 하면 Windows 애플리케이션에서 웹 서비스에 액세스할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 사용하여 웹 서비스의 속성 및 메서드를 표시하고 친숙한 인프라와 도구를 통해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기술 기반의 비즈니스 애플리케이션을 빌드할 수 있는 프록시 클래스를 생성할 수 있습니다.  
  
## <a name="integrating-report-management-functionality-using-windows-forms"></a>Windows Forms를 사용하여 보고서 관리 기능 통합  
 URL 액세스와 달리 SOAP API는 보고서 서버를 통해 사용 가능한 전체 관리 기능 집합을 표시합니다. 다시 말해서 개발자가 SOAP을 통해 보고서 관리자의 전체 관리 기능을 사용할 수 있습니다. 그러므로 Windows Forms를 사용하여 완전한 관리 도구를 개발할 수 있습니다. 예를 들어 Windows 애플리케이션에서 사용자들이 보고서 서버 네임스페이스의 내용을 검색할 수 있도록 설정해야 할 경우가 있습니다. 이런 경우 웹 서비스 <xref:ReportService2010.ReportingService2010.ListChildren%2A> 메서드를 사용하여 보고서 서버 데이터베이스의 모든 항목을 나열한 다음 Listview, Treeview 또는 Combobox 컨트롤을 사용하여 이러한 항목을 사용자에게 표시할 수 있습니다. 다음 웹 서비스 코드를 사용하면 사용자가 폼에서 단추를 클릭할 때 사용자의 내 보고서 폴더에서 사용 가능한 보고서의 현재 목록을 검색하도록 할 수 있습니다.  
  
```vb  
' Button click event that retrieves a list of reports from  
' the My Reports folder and displays them in a combo box  
Private Sub listReportsButton_Click(sender As Object, e As System.EventArgs)  
   ' Create a new Web service object and set credentials  
   ' to Windows Authentication  
   Dim rs As New ReportingService2010()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return the list of items in My Reports  
   Dim items As CatalogItem() = rs.ListChildren("/Adventureworks 2008 Sample Reports", False)  
  
   Dim ci As CatalogItem  
   For Each ci In  items  
      ' If the item is a report, add it to   
      ' a combo box  
      If ci.TypeName = "Report" Then  
         catalogComboBox.Items.Add(ci.Name)  
      End If  
   Next ci  
End Sub 'listReportsButton_Click  
```  
  
```csharp  
// Button click event that retrieves a list of reports from  
// the My Reports folder and displays them in a combo box  
private void listReportsButton_Click(object sender, System.EventArgs e)  
{  
   // Create a new Web service object and set credentials  
   // to Windows Authentication  
   ReportingService2010 rs = new ReportingService2010();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return the list of items in My Reports  
   CatalogItem[] items = rs.ListChildren("/Adventureworks 2008 Sample Reports", false);  
  
   foreach (CatalogItem ci in items)  
   {  
      // If the item is a report, add it to   
      // a combo box  
      if (ci.TypeName == "Report")  
         catalogComboBox.Items.Add(ci.Name);  
   }  
}  
```  
  
 여기서 사용자가 콤보 상자에서 보고서를 선택하고 웹 브라우저 컨트롤이나 이미지 컨트롤을 사용하여 폼에서 보고서를 미리 볼 수 있도록 설정할 수 있습니다.  
  
## <a name="enabling-report-viewing-and-navigation-using-windows-forms"></a>Windows Forms를 사용하여 보고서 보기 및 탐색 사용  
 보고서를 Windows Forms 애플리케이션에 통합하는 데 사용할 수 있는 두 가지 메서드가 있습니다.  
  
 SOAP API를 사용하여 지원되는 모든 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드 사용 렌더링 형식으로 보고서를 렌더링할 수 있습니다. SOAP을 통해 보고서 보기 및 탐색을 사용하면 다음과 같이 약간의 단점이 있습니다.  
  
-   URL 액세스를 통한 HTML 뷰어에 포함된 보고서 도구 모음의 기본 제공 기능을 활용할 수 없습니다.  
  
-   HTML로 렌더링할 경우 <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A> 메서드를 사용하여 이미지나 리소스를 추가 스트림 형태로 별도로 렌더링해야 합니다.  
  
-   URL 액세스를 사용하면 SOAP API에 비해 보고서 렌더링 성능이 약간 높아집니다.  
  
 하지만 SOAP API의 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드를 사용하면 보고서를 렌더링하여 프로그래밍 방식으로 다양한 출력 형식으로 저장할 수 있습니다. 이 점을 사용자 개입이 필요한 URL 액세스에 비해 이점으로 손꼽을 수 있습니다. SOAP API <xref:ReportExecution2005.ReportExecutionService.Render%2A> 메서드를 사용하여 보고서를 렌더링하는 경우 지원되는 모든 출력 형식으로 렌더링할 수 있습니다.  
  
 또한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]에 포함되어 체험용으로 배포 가능한 보고서 뷰어 컨트롤을 사용할 수도 있습니다. 보고서 뷰어 컨트롤을 통해 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 사용자 지정 애플리케이션에 쉽게 포함시킬 수 있습니다. 보고서 뷰어 컨트롤은 사전 디자인을 갖추어 완전히 제작된 보고서를 애플리케이션 기능 집합의 일부로 제공하려는 개발자에게 적합합니다. 예를 들어 웹 사이트 관리 애플리케이션에 회사 웹 사이트에서의 클릭 동향 분석을 보여 주는 보고서를 포함할 수 있습니다. 애플리케이션에 컨트롤을 포함하는 것은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버 구성 요소를 애플리케이션 배포에 포함하는 대신 사용할 수 있는 간소화된 방법입니다. 이러한 컨트롤은 보고서 기능을 제공하며 단, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 제공되는 보고서 제작, 게시, 배포 및 배달에 대한 추가 지원은 없습니다.  
  
 보고서 뷰어 컨트롤에는 기능이 풍부한 Windows 클라이언트 애플리케이션용과 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 애플리케이션용의 두 가지 버전이 있습니다. 이러한 컨트롤은 로컬 처리 및 원격 처리 모드를 모두 지원합니다. 로컬 처리 모드의 경우 애플리케이션은 보고서 정의 및 데이터 세트을 제공하고 보고서 처리를 시작합니다. 원격 처리 모드의 경우에는 데이터 검색 및 보고서 처리는 보고서 서버에서 수행되며 컨트롤은 표시 및 보고서 탐색에 사용됩니다. 이 모델에서는 데스크톱에서 엔터프라이즈 수준까지 확장될 수 있는 기능이 풍부한 애플리케이션을 구축할 수 있습니다.  
  
 보고서 뷰어 컨트롤은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 온라인 도움말에 설명되어 있습니다. 자세한 내용은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 제품 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [웹 서비스와 .NET Framework를 사용하여 애플리케이션 빌드](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [애플리케이션에 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [웹 애플리케이션에서 SOAP API 사용](../../reporting-services/application-integration/integrating-reporting-services-using-soap-web-application.md)  
  
  
