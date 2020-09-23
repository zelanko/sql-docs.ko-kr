---
title: 보고서 뷰어 컨트롤 시작
description: 보고서 뷰어 컨트롤은 Reporting Services RDL 보고서를 WebForms 및 WinForms 앱에 통합하는 데 사용할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 09/01/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: conceptual
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 009c70da7365cc232dc5b00da6b4f1f62bfca8e2
ms.sourcegitcommit: 04fb4c2d7ccddd30745b334b319d9d2dd34325d6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89569963"
---
# <a name="integrate-reporting-services-using-the-report-viewer-controls---get-started"></a>보고서 뷰어 컨트롤을 사용하여 Reporting Services 통합 - 시작하기

보고서 뷰어 컨트롤은 Reporting Services RDL 보고서를 WebForms 및 WinForms 앱에 통합하는 데 사용할 수 있습니다. 최근 업데이트에 대한 자세한 내용은 [변경 로그](changelog.md)를 참조하세요.

## <a name="add-the-report-viewer-control-to-a-new-web-project"></a>새 웹 프로젝트에 보고서 뷰어 컨트롤 추가

1. 새 **ASP.NET 빈 웹 사이트**를 만들거나 기존 ASP.NET 프로젝트를 엽니다.

    .NET Framework 4.6 이상의 모든 버전을 사용할 수 있습니다.

    ![ASP.NET 빈 웹 사이트를 새로 만드는 스크린샷](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project-4-6.png)

2. **NuGet 패키지 관리자 콘솔**을 통해 보고서 뷰어 컨트롤 NuGet 패키지를 설치합니다.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. 프로젝트에 새 .aspx 페이지를 추가하고 페이지 내에서 사용하도록 보고서 뷰어 컨트롤 어셈블리를 등록합니다.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. 페이지에 **ScriptManagerControl**을 추가합니다.

5. 페이지에 보고서 뷰어 컨트롤을 추가합니다. 원격 보고서 서버에 호스팅된 보고서를 참조하도록 아래 코드 조각을 업데이트할 수 있습니다.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
마지막 페이지는 다음과 같아야 합니다.

```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

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
            <ServerReport ReportServerUrl="https://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>
```

## <a name="update-an-existing-project-to-use-the-report-viewer-control"></a>보고서 뷰어 컨트롤을 사용하도록 기존 프로젝트 업데이트

어셈블리 참조를 프로젝트의 web.config 및 뷰어 컨트롤을 참조하는 모든 .aspx 페이지를 포함하는 버전 *15.0.0.0*으로 업데이트해야 합니다.

### <a name="sample-webconfig-changes"></a>샘플 web.config 변경 내용

```xml
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  https://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.6">
      <assemblies>
        <!-- All assemblies updated to version 15.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 15.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.6"/>
    <httpHandlers>
      <!-- Version updated to 15.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 15.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>샘플 .aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 15.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="add-the-report-viewer-control-to-a-new-windows-forms-project"></a>새 Windows Forms 프로젝트에 보고서 뷰어 컨트롤 추가

1. 새 **Windows Forms 애플리케이션**을 만들거나 기존 프로젝트를 엽니다.

    .NET Framework 4.6 이상의 모든 버전을 사용할 수 있습니다.
    
    ![새 Windows Forms 애플리케이션을 만드는 스크린샷](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project-4-6.png)

2. **NuGet 패키지 관리자 콘솔**을 통해 보고서 뷰어 컨트롤 NuGet 패키지를 설치합니다.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. 코드에서 새 컨트롤을 추가하거나 [도구 상자에 컨트롤을 추가](#add-the-control-to-visual-studio-toolbar)합니다.

    ```csharp
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

## <a name="how-to-set-100-height-on-the-report-viewer-control"></a>보고서 뷰어 컨트롤에서 100% 높이를 설정하는 방법

뷰어 컨트롤의 높이를 100%로 설정하면 부모 요소에 높이가 정의되어 있거나 모든 상위 항목에 백분율 높이가 정의되어야 합니다.

### <a name="set-the-height-of-all-the-ancestors-to-100"></a>모든 상위 항목의 높이를 100%로 설정

```html
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
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

### <a name="set-the-parents-height-attribute"></a>부모의 높이 특성 설정

뷰포트 백분율 길이 대한 자세한 내용은 [뷰포트 백분율 길이](http://www.w3.org/TR/css3-values/#viewport-relative-lengths)를 참조하세요.

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

## <a name="add-the-control-to-visual-studio-toolbar"></a>Visual Studio 도구 모음에 컨트롤 추가

보고서 뷰어 컨트롤은 이제 NuGet 패키지로 제공되며, 더 이상 기본적으로 Visual Studio 도구 상자에 표시되지 않습니다. 이 도구 상자에 수동으로 컨트롤을 추가할 수 있습니다.

1. 위에서 언급한 대로 WinForms 또는 WebForms 중 하나에 대한 NuGet 패키지를 설치합니다.

2. 도구 상자에 나열된 보고서 뷰어 컨트롤을 제거합니다.

    ![ReportViewer 컨트롤을 삭제하는 스크린샷](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. 도구 상자의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음, **항목 선택...** 을 선택합니다.

    ![도구 상자에서 항목 선택 옵션을 보여 주는 스크린샷](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. **.NET Framework 구성 요소**에서 **찾아보기**를 선택합니다.

    ![.NET Framework 구성 요소 대화 상자에 있는 찾아보기 단추의 스크린샷](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. 설치한 NuGet 패키지에서 **Microsoft.ReportViewer.WinForms.dll** 또는 **Microsoft.ReportViewer.WebForms.dll**을 선택합니다.

    > [!NOTE] 
    > NuGet 패키지는 프로젝트의 솔루션 디렉터리에 설치됩니다. dll에 대한 경로는 메시지는 다음과 유사합니다. `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` 또는 `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`

6. 도구 상자 내에서 새 컨트롤이 표시됩니다. 그런 다음 원하는 경우 도구 상자 내에서 다른 탭으로 이동할 수 있습니다.

    ![도구 상자의 새 ReportViewer 컨트롤을 보여 주는 스크린샷](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

## <a name="common-issues"></a>일반적인 문제
    
뷰어 컨트롤은 최신 브라우저용으로 디자인되었습니다. 이 컨트롤은 브라우저가 IE 호환성 모드를 사용하여 페이지를 렌더링하는 경우 예상대로 작동하지 않을 수 있습니다. 인트라넷 사이트는 기본 브라우저 동작을 재정의하기 위해 메타 태그가 필요할 수 있습니다.

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
```

## <a name="nugetorg-pages"></a>NuGet.org 페이지

다음은 NuGet.org 사이트에 게시된 보고서 뷰어 컨트롤의 WebForm 및 WinForm 버전 관련 문서에 대한 링크입니다.

- Microsoft.ReportingServices.ReportViewerControl.WebForms [https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WebForms/)
- Microsoft.ReportingServices.ReportViewerControl.Winforms [https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WinForms/](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.WinForms/)


## <a name="forum-feedback"></a>포럼 피드백

[Reporting Services 포럼](https://docs.microsoft.com/answers/topics/sql-server-reporting-services.html)에서 문제를 게시하여 팀에 알려주세요.

## <a name="see-also"></a>참고 항목

[보고서 뷰어 컨트롤의 데이터 컬렉션](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  

