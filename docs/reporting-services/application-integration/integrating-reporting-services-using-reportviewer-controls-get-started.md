---
title: "ReportViewer 2016 컨트롤 시작하기 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: application-integration
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: "12"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: 9b177bb647fd1c9daf5fb330f3bff15cf3e73ab3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>ReportViewer 컨트롤을 사용하여 Reporting Services 통합 - 시작하기

개발자가 Reporting Services 2016 ReportViewer 컨트롤을 통해 ASP.NET 웹 사이트 및 Windows Forms 앱에서 페이지를 매긴 보고서를 포함하는 방법에 대해 알아봅니다. 새 프로젝트에 컨트롤을 추가하거나 기존 프로젝트를 업데이트할 수 있습니다.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>새 웹 프로젝트에 ReportViewer 컨트롤 추가

1. 새 **ASP.NET 빈 웹 사이트**를 만들거나 기존 ASP.NET 프로젝트를 엽니다.

    ![ssRS-새-ASPNET-프로젝트-만들기](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. **NuGet 패키지 관리자 콘솔**을 통해 ReportViewer 2016 컨트롤 NuGet 패키지를 설치합니다.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 프로젝트에 새 .aspx 페이지를 추가하고 페이지 내에서 사용하도록 ReportViewer 컨트롤 어셈블리를 등록합니다.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 페이지에 **ScriptManagerControl**을 추가합니다.

5. 페이지에 ReportViewer 컨트롤을 추가합니다. 원격 보고서 서버에 호스팅된 보고서를 참조하도록 아래 코드 조각을 업데이트할 수 있습니다.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
마지막 페이지는 다음과 같아야 합니다.

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="http://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>ReportViewer 컨트롤을 사용하도록 기존 프로젝트 업데이트

기존 프로젝트에서 ReportViewer 2016 컨트롤을 사용하려면 NuGet을 통해 컨트롤을 추가하고 *14.0.0.0* 버전으로 어셈블리 참조를 업데이트합니다. 여기에는 프로젝트의 web.config 및 ReportViewer 컨트롤을 참조하는 모든 .aspx 페이지의 업데이트도 포함됩니다.

### <a name="sample-webconfig-changes"></a>샘플 web.config 변경 내용

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  http://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 14.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 14.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 14.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 14.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>샘플 .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>새 Windows Forms 프로젝트에 ReportViewer 컨트롤 추가

1. 새 **Windows Forms 응용 프로그램**을 만들거나 기존 프로젝트를 엽니다.

    ![ssRS-새-winforms-프로젝트-만들기](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. **NuGet 패키지 관리자 콘솔**을 통해 ReportViewer 2016 컨트롤 NuGet 패키지를 설치합니다.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 코드에서 새 컨트롤을 추가하거나 [도구 상자에 컨트롤을 추가](##adding-control-to-visual-studio-toolbar)합니다.

    ```
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>Report Viewer 2016 컨트롤에서 100% 높이를 설정하는 방법

새 Report Viewer 2016 컨트롤은 HTML5 표준 모드 페이지에 최적화되어 있으며 모든 최신 브라우저에서 작동합니다. 이전에 RVC 컨트롤을 사용하여 100% 높이 속성을 설정하는 경우에는 상위 항목 중에 지정된 높이가 없는 경우에도 정상적으로 작동했습니다. 이 동작은 HTML5에서 변경되었습니다. 새 RVC 컨트롤에서 이 속성을 설정하면 부모 요소에 정의된 높이가 있는 경우(예를 들어 자동 값이 아니라) 또는 RVC의 모든 상위 항목에 100% 높이가 있는 경우에만 제대로 작동합니다.

다음은 이를 수행하는 두 가지 예제입니다.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>모든 부모 요소의 높이를 100%로 설정

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>reportviewer 컨트롤의 부모에서 스타일 높이 특성을 설정

뷰포트 백분율 길이 대한 자세한 내용은 [뷰포트 백분율 길이](https://www.w3.org/TR/css3-values/#viewport-relative-lengths)를 참조하세요.

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>Visual Studio 도구 모음에 컨트롤 추가

이제 보고서 뷰어 컨트롤은 NuGet 패키지로 제공됩니다. 이 때문에 보고서 뷰어 컨트롤은 기본적으로 Visual Studio 도구 상자에 표시되지 않습니다. 다음을 수행하여 도구 모음에 컨트롤을 추가할 수 있습니다.

1. 위에서 언급한 대로 WinForms 또는 WebForms 중 하나에 대한 NuGet 패키지를 설치합니다.

2. 도구 상자에서 ReportViewer 컨트롤을 제거합니다. 이는 12.x 버전을 사용하는 컨트롤입니다.

    ![ssRS-이전-rvcontrol-도구 상자-제거](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 도구 상자의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **항목 선택...**을 선택합니다.

    ![ssRS-도구 상자-항목-선택](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. **.NET Framework 구성 요소**에서 **찾아보기**를 선택합니다.

    ![ssRS-도구 상자-찾아보기](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 설치한 NuGet 패키지에서 **Microsoft.ReportViewer.WinForms.dll** 또는 **Microsoft.ReportViewer.WebForms.dll**을 선택합니다.

    > [!NOTE] 
    > NuGet 패키지는 프로젝트의 솔루션 디렉터리에 설치됩니다. dll에 대한 경로는 메시지는 다음과 유사합니다. `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` 또는 `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`

6. 도구 상자 내에서 새 컨트롤이 표시됩니다. 그런 다음 원하는 경우 도구 상자 내에서 다른 탭으로 이동할 수 있습니다.

    ![ssRS-도구 상자-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>알아두어야 할 사항

- 이렇게 하면 현재 프로젝트 내에서 설치된 NuGet 패키지에 참조가 추가됩니다. 도구 상자에 있는 항목은 다른 프로젝트에 유지됩니다. 새 솔루션/프로젝트에 NuGet 패키지를 설치할 때 도구 상자 항목은 이전 버전을 참조할 수도 있습니다. 

- 컨트롤은 어셈블리를 더 이상 사용할 수 없는 경우에도 도구 상자에서 유지됩니다. 해당 프로젝트를 삭제하면 사용자가 시도하고 도구 상자에서 컨트롤을 추가하는 경우 Visual Studio에서 오류가 발생합니다. 이 오류를 해결하려면 도구 상자에서 컨트롤을 제거하고 위의 단계를 사용하여 다시 추가합니다.


## <a name="common-issues"></a>일반적인 문제
    
- ReportViewer 2016 컨트롤은 최신 브라우저에서 사용되도록 설계되었습니다. 브라우저가 IE 호환 모드에서 웹 페이지를 렌더링하는 경우 컨트롤이 작동하지 않을 수 있습니다. 인트라넷 사이트에서는 호환 모드에서 인트라넷 페이지 렌더링을 권장하는, 설정 재정의를 위한 메타 태그가 필요할 수 있습니다.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>사용자 의견 제공

[Reporting Services MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices)이나 [RVCFeedback@microsoft.com](mailto:RVCFeedback@microsoft.com)의 전자 메일을 통해 컨트롤과 관련된 문제에 대해 알려 주세요.

## <a name="see-also"></a>관련 항목:

[2016 ReportingViewer 컨트롤에서 데이터 수집](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](http://go.microsoft.com/fwlink/?LinkId=620231)

