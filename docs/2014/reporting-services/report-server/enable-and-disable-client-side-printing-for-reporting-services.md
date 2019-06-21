---
title: Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea5016aa51a25bd296d2e77516b30b84a7a28cec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103926"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 컨트롤인 **RSClientPrint**, 브라우저에서 표시 되는 보고서에 대 한 클라이언트 쪽 인쇄를 제공 합니다. 이 컨트롤은 다른 인쇄 대화 상자에 공통적인 기능을 지원하는 사용자 지정 인쇄 대화 상자를 표시합니다. 인쇄 미리 보기, 특정 페이지와 범위 지정을 위한 페이지 선택, 페이지 여백 및 방향이 여기에 포함됩니다. 클라이언트 쪽 인쇄 기능은 기본적으로 설정되어 있지만 이 기능을 사용하지 않으려면 해제할 수 있습니다.  
  
> [!NOTE]  
>  ActiveX 컨트롤을 다운로드하려면 관리자 권한이 있어야 합니다.  
  
## <a name="downloading-the-activex-control"></a>AcitveX 컨트롤 다운로드  
 인쇄 기능을 사용하려는 사용자는 클라이언트 인쇄 기능을 제공하는 ActiveX 컨트롤을 다운로드하여 설치해야 합니다. 사용자가 처음 합니다 **프린터** 아이콘이 보고서 도구 모음에서 Microsoft ActiveX 컨트롤이 컴퓨터에 다운로드 됩니다. 컨트롤을 다운로드 한 후는 **인쇄** 를 클릭할 때마다 대화 상자를 표시 합니다 **프린터** 아이콘.  
  
 브라우저 설정에 따라 컨트롤을 설치하라는 메시지가 표시되거나 컨트롤을 설치할 수 없거나 컨트롤이 백그라운드에 이미 설치되어 있을 수 있습니다.  
  
 에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer를 통해 지정 된 ActiveX 컨트롤 다운로드 및 설치에 영향을 주는 설정 합니다 **ActiveX 컨트롤 및 플러그 인** 에 노드를 **보안 설정을** 페이지 웹 콘텐츠 영역입니다. 웹 영역 보안 기본 설정을 기반으로 사용자가 인쇄 컨트롤을 다운로드하고 실행할 수 있는지 여부는 다음 설정에 따라 결정됩니다.  
  
-   서명된 AcitveX 컨트롤 다운로드  
  
-   안전한 것으로 표시된 ActiveX 컨트롤 스크립트  
  
-   ActiveX 컨트롤 및 플러그 인 실행  
  
 사용 하려는 사용자 **RSClientPrint** 클라이언트 쪽 인쇄 기능을 수행 하려면 다음을 설정 해야 합니다.  
  
-   **서명 된 ActiveX 컨트롤 다운로드** 하 고 **ActiveX 컨트롤 스크립트 스크립팅에 안전한 것으로 표시** 설치에 필요 합니다.  
  
-   **ActiveX 컨트롤 및 플러그 인 실행** 인쇄 작업 진행 합니다.  
  
 합니다 **RSClientPrint** 포함 되어 있는 것에서 유효한 디지털 인증서 ActiveX 컨트롤이 서명 되어 [!INCLUDE[msCoName](../../includes/msconame-md.md)]입니다.  
  
## <a name="enabling-and-disabling-client-side-printing"></a>클라이언트 쪽 인쇄 기능 설정 및 해제  
 보고서 서버 관리자는 보고서 서버 시스템 속성을 설정 하 여 인쇄 기능을 사용 하지 않도록 설정 옵션이 **EnableClientPrinting** 에 `false`입니다. 이렇게 하면 해당 서버에서 관리하는 모든 보고서에 대한 클라이언트 쪽 인쇄 기능이 해제됩니다. 기본적으로 **EnableClientPrinting** 로 설정 된 `true`합니다. 다음과 같은 방법으로 클라이언트 쪽 인쇄 기능을 해제할 수 있습니다.  
  
-   **기본 모드 보고서 서버**:  
  
    1.  관리자 권한으로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 시작합니다.  
  
    2.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 보고서 서버 인스턴스에 연결합니다.  
  
    3.  보고서 서버 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **속성** 옵션이 해제되어 있으면 관리자 권한으로 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 실행했는지 확인합니다.  
  
    4.  선택 **ActiveX 클라이언트 인쇄 컨트롤에 대 한 다운로드 설정**합니다.  
  
    5.  **확인**을 클릭합니다.  
  
-   **SharePoint 모드 보고서 서버**:  
  
    1.  SharePoint 중앙 관리에서 **애플리케이션 관리**를 클릭합니다.  
  
    2.  **서비스 응용 프로그램 관리**를 클릭합니다.  
  
    3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 응용 프로그램의 이름을 클릭하고 SharePoint 리본 메뉴에서 **관리** 를 클릭합니다.  
  
    4.  **시스템 설정**을 클릭합니다.  
  
    5.  **클라이언트 인쇄 사용**을 선택합니다. **클라이언트 인쇄 사용** 옵션은 페이지 아래쪽에 있습니다.  
  
    6.  **확인**을 클릭합니다.  
  
-   스크립트 또는 보고서 서버 시스템 속성을 설정 하는 코드를 작성할 **EnableClientPrinting** 를 `false.`  
  
 다음 예제 스크립트에서는 클라이언트 쪽 인쇄 기능을 해제하는 한 가지 방법을 보여 줍니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 속성을 **EnableClientPrinting** 로 설정하려면 다음 **False**를 클릭하여 다운로드를 강제로 다시 실행할 수 있습니다. 코드를 실행한 후에는 IIS를 다시 시작합니다.  
  
### <a name="sample-script"></a>예제 스크립트  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  
