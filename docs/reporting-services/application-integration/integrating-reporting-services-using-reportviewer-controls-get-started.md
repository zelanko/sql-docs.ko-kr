---
title: "ReportViewer 2016 컨트롤 시작 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a6a0bbee9141df565966df3e90f396e33c9b96a7
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>Reporting Services ReportViewer 컨트롤을 사용 하 여 시작-통합

개발자가 ASP.Net 웹 사이트 및 Reporting Services 2016 ReportViewer 컨트롤을 통해 Windows forms 앱에서 페이지 매긴된 보고서를 포함할 수 있습니다는 방법에 대해 알아봅니다. 새 프로젝트에서 컨트롤을 추가 하거나 기존 프로젝트를 업데이트할 수 있습니다.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>새 웹 프로젝트에 ReportViewer 컨트롤 추가

1. 새 **ASP.NET 빈 웹 사이트** 또는 기존 ASP.NET 프로젝트를 엽니다.

    ![ssRS--새-ASPNET-프로젝트 만들기](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. ReportViewer 2016 제어 nuget 패키지를 통해 설치 된 **Nuget 패키지 관리자 콘솔**합니다.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 프로젝트에 새.aspx 페이지를 추가 하 고 페이지 내에서 사용 하기 위해 ReportViewer 컨트롤 어셈블리를 등록 합니다.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 추가 **ScriptManagerControl** 페이지에 있습니다.

5. 페이지에 ReportViewer 컨트롤을 추가 합니다. 아래 코드 조각 원격 보고서 서버에 호스팅된 보고서를 참조 하도록 업데이트할 수 있습니다.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
마지막 페이지는 다음과 같습니다.

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

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>ReportViewer 컨트롤을 사용 하도록 기존 프로젝트를 업데이트 합니다.

기존 프로젝트에 ReportViewer 2016 컨트롤의 사용, Nuget 통해 컨트롤을 추가 및 버전으로 어셈블리 참조를 업데이트 하려면 *14.0.0.0*합니다. 프로젝트의 web.config 및 ReportViewer 컨트롤을 참조 하는 모든.aspx 페이지의 업데이트도 포함 됩니다.

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

### <a name="sample-aspx"></a>샘플.aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>새 Windows forms 프로젝트에 ReportViewer 컨트롤 추가

1. 새 **Windows Forms 응용 프로그램** 또는 기존 프로젝트를 엽니다.

    ![ssRS--새-winforms-프로젝트 만들기](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. ReportViewer 2016 제어 nuget 패키지를 통해 설치 된 **Nuget 패키지 관리자 콘솔**합니다.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 코드에서 새 컨트롤을 추가 또는 [도구 상자에 컨트롤을 추가할](##adding-control-to-visual-studio-toolbar)합니다.

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

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>보고서 뷰어 2016 컨트롤에 100% 높이 설정 하는 방법

새 보고서 뷰어 2016 컨트롤 HTML5 표준 모드의 페이지에 대해 최적화 된 모든 최신 브라우저에서 작동 합니다. 이전 RVC 컨트롤과 이전에 100% 높이 속성을 설정 하면 정상적으로 완료 상위 항목 중에 지정 된 높이 하는 경우에 합니다. HTML5에서이 동작이 변경 되었습니다. 새 RVC 컨트롤에서이 속성을 설정 하면 부모 요소에 정의 된 높이 하는 경우에 제대로 작동, 즉, auto의 값이 아님 또는 RVC의 모든 상위 항목 100% 높이 너무 합니다.

이렇게 하려면 두 가지 예는 다음과 같습니다.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>100% 높이의 모든 부모 요소를 설정 하 여

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

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>Reportviewer 컨트롤의 부모에 스타일 높이 특성을 설정 하 여

뷰포트 백분율 길이 대 한 자세한 내용은 참조 [뷰포트 백분율 길이](https://www.w3.org/TR/css3-values/#viewport-relative-lengths)합니다.

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

이제 보고서 뷰어 컨트롤은 NuGet 패키지로 제공 됩니다. 이 때문에 기본적으로 Visual Studio 도구 상자에 표시 하는 보고서 뷰어 컨트롤을 표시 되지 않습니다. 다음을 수행 하 여 도구 상자에 컨트롤을 추가할 수 있습니다.

1. WinForms 또는 WebForms 위에서 언급 한 대로 대 한 NuGet 패키지를 설치 합니다.

2. 도구 상자에 나열 된 ReportViewer 컨트롤을 제거 합니다. 이는 12.x의 버전으로 제어 합니다.

    ![ssRS-제거-오래-rvcontrol-도구 상자](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 도구 상자에서 아무 곳 이나 클릭 마우스 오른쪽 단추로 선택한 후 **항목 선택...** .

    ![ssRS-도구 상자--항목 선택](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. 에 **.NET Framework 구성 요소**선택, **찾아보기**합니다.

    ![ssRS-도구 상자-찾아보기](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 선택 된 **Microsoft.ReportViewer.WinForms.dll** 또는 **Microsoft.ReportViewer.WebForms.dll** 설치한 NuGet 패키지에서 합니다.

    > [!NOTE] 
    > NuGet 패키지는 프로젝트의 솔루션 디렉터리에 설치 됩니다. Dll 경로 다음과 같은으로: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` 또는 `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`합니다.

6. 도구 상자 내에서 새 컨트롤에 표시 됩니다. 이동할 수 있습니다 다음 도구 상자 내에서 다른 탭으로 하려는 경우.

    ![ssRS-도구 상자-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>알아두어야 할 사항

- 이렇게 하면 현재 프로젝트 내에서 설치 된 NuGet 패키지에 대 한 참조가 추가 됩니다. 도구 상자에 있는 항목은 다른 프로젝트에 유지 됩니다. 새 솔루션/프로젝트에 NuGet 패키지를 설치할 때 도구 상자 항목 이전 버전을 참조할 수도 있습니다. 

- 컨트롤은 어셈블리를 더 이상 사용할 수 없는 경우에 도구 상자에 유지 됩니다. 해당 프로젝트를 삭제 하는 경우 Visual Studio 시도 하 고 도구 상자에서 컨트롤을 추가 하는 경우 오류가 throw 됩니다. 이 오류를 해결 하려면 도구 상자에서 컨트롤을 제거 하 고 위의 단계를 사용 하 여 다시 추가 합니다.


## <a name="common-issues"></a>일반적인 문제
    
- 2016 ReportViewer 컨트롤은 최신 브라우저에서 사용 되는 설계 되었습니다. 브라우저 IE 호환 모드에서 웹 페이지를 렌더링 하는 경우 컨트롤이 작동 하지 않을 수 있습니다. 인트라넷 사이트에는 호환 모드에서 인트라넷 페이지 렌더링 것을 권장 설정을 재정의 하려면 다음 메타 태그가 필요할 수 있습니다.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>사용자 의견 제공

팀에서 문제에서 볼 수 있는 컨트롤에 대 한 알 수 있도록는 [Reporting Services MSDN 포럼](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) 또는에서 전자 메일을 통해 [ RVCFeedback@microsoft.com ](mailto:RVCFeedback@microsoft.com)합니다.

## <a name="see-also"></a>참고 항목

[2016 ReportingViewer 컨트롤에서 데이터 수집](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
문의: [Reporting Services 포럼을 시도 하십시오.](http://go.microsoft.com/fwlink/?LinkId=620231)


