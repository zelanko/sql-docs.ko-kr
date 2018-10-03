---
title: 사용자 지정 응용 프로그램에서 RSClientPrint 컨트롤 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4f3299b67ffb55723a59326ec884d9ad30617e24
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212664"
---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>사용자 지정 응용 프로그램에서 RSClientPrint 컨트롤 사용
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX 컨트롤인 **RSPrintClient**는 HTML 뷰어에 표시되는 보고서에 대한 클라이언트 쪽 인쇄 기능을 제공합니다. 사용자는 제공된 **인쇄** 대화 상자를 사용하여 인쇄 작업 시작, 보고서 미리 보기, 인쇄할 페이지 지정, 여백 조정 등의 작업을 수행할 수 있습니다. 클라이언트 쪽 인쇄 작업 과정에서 보고서 서버는 이미지(EMF) 렌더링 확장 프로그램으로 보고서를 렌더링하고 운영 체제의 인쇄 기능으로 인쇄 작업을 만들어 프린터에 보냅니다.  
  
 클라이언트 쪽 인쇄 기능은 사용자 컴퓨터의 브라우저 인쇄 설정을 무시하고 대신 인쇄 출력을 만드는 데 보고서의 페이지 크기, 여백, 머리글 및 바닥글 텍스트를 사용하여 HTML 보고서의 인쇄 품질을 제어하고 향상시킬 수 있습니다. 인쇄 컨트롤은 보고서의 속성 값을 읽어 페이지 크기와 여백 설정을 지정합니다.  
  
 타사 도구 모음이나 뷰어에서 클라이언트 쪽 인쇄 기능을 설정하려는 개발자는 **RSClientPrint** COM 개체를 통해 ActiveX 컨트롤에 액세스할 수 있습니다. 컨트롤은 무료로 배포됩니다. 다음 목록에서는 컨트롤 사용에 대한 권장 사항을 나열합니다.  
  
-   컨트롤을 사용하여 웹 기반 보고서의 인쇄 품질을 향상시킬 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 호환 프로그래밍 언어나 스크립트에서 개체를 지정할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Forms 응용 프로그램에서는 컨트롤을 사용할 수 없습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 프로그램 파일에서 .cab 파일을 복사하여 사용자 지정 응용 프로그램 코드베이스에 추가합니다.  
  
-   \<OBJECT> 태그를 사용하여 컨트롤을 지정합니다.  
  
-   OBJECT CODEBASE 특성에서 .cab 파일의 상대 URL이나 정규화된 URL을 지정합니다.  
  
-   .cab 파일에 대한 사용자의 응용 프로그램 버전 정보를 지정하여 응용 프로그램에 사용되는 버전을 추적합니다.  
  
-   이미지(EMF) 렌더링에 대한 온라인 설명서 항목을 검토하여 인쇄 미리 보기와 출력을 위해 페이지가 렌더링되는 방법을 이해합니다.  
  
## <a name="rsprintclient-overview"></a>RSPrintClient 개요  
 이 컨트롤은 특정 페이지와 범위, 페이지 여백 및 방향을 지정하는 페이지 선택 기능, 인쇄 미리 보기 기능을 비롯하여 다른 인쇄 대화 상자에 공통적인 기능을 지원하는 사용자 지정 인쇄 대화 상자를 표시합니다. 컨트롤은 CAB 파일로 패키지됩니다. **인쇄** 대화 상자의 텍스트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 지원하는 모든 언어로 지역화됩니다. **RSPrintClient** ActiveX 컨트롤은 이미지 렌더링 확장 프로그램(EMF)을 사용하여 보고서를 인쇄합니다. StartPage, EndPage, MarginBottom, MarginLeft, MarginTop, MarginRight, PageHeight 및 PageWidth와 같은 EMF 장치 정보를 사용합니다. 이미지 렌더링에 대한 다른 장치 정보 설정은 지원되지 않습니다.  
  
### <a name="language-support"></a>언어 지원  
 인쇄 컨트롤은 여러 언어로 사용자 인터페이스 텍스트를 제공하며 여러 단위의 입력 값을 허용합니다. 사용되는 언어와 단위는 **Culture** 및 **UICulture** 속성에 의해 결정됩니다. 두 속성 모두 LCID 값을 사용합니다. 지원되는 언어의 변형 언어에 대한 LCID를 지정하는 경우 이에 가장 근접한 언어가 사용됩니다. 지원되지 않는 LCID를 지정하는 경우 이와 근접한 LCID가 없으면 영어(미국)가 사용됩니다.  
  
## <a name="using-rsclientprint-in-code"></a>코드에서 RSClientPrint 사용  
 **RSClientPrint** 개체는 ActiveX 컨트롤과 해당 메서드 및 속성에 프로그래밍 방식으로 액세스하는 데 사용됩니다. 이 컨트롤은 인쇄 미리 보기를 위한 모달 대화 상자를 제공합니다.  
  
### <a name="specifying-default-values"></a>기본값 지정  
 보고서 여백 값과 페이지 값으로 **인쇄** 대화 상자를 초기화할 수 있습니다. 기본적으로 **인쇄** 대화 상자는 보고서 정의 값으로 초기화됩니다. 기본값을 사용하거나 개체의 속성을 설정하여 다른 값을 지정할 수 있습니다.  
  
 모든 치수는 밀리미터 단위로 설정됩니다. **Culture** 및 **UICulture**가 미터법을 사용하지 않는 로캘로 설정되는 경우 런타임 시 단위가 변환됩니다.  
  
 페이지 크기와 여백에 사용되는 값을 확인하려면 **GetProperties** 메서드를 사용하여 기본값을 검색합니다.  
  
-   **PageHeight** 및 **PageWidth**는 기본 페이지 높이와 너비를 지정합니다. 인쇄 컨트롤이 시작되면 이러한 속성 값을 기준으로 현재 선택한 프린터에서 사용할 수 있는 가장 근접한 용지 크기가 선택됩니다. **PageWidth**가 **PageHeight**보다 크면 용지 방향이 가로로 설정됩니다. 그렇지 않으면 용지 방향이 세로로 설정됩니다.  
  
-   **LeftMargin**, **RightMargin**, **TopMargin** 및 **BottomMargin**은 기본적으로 모두 12.2밀리미터로 설정됩니다.  
  
 속성은 보고서 서버의 **Item** 속성 컬렉션에 저장됩니다. 보고서 정의가 업데이트될 때마다 속성 값을 덮어씁니다.  
  
### <a name="rsclientprint-properties"></a>RSClientPrint 속성  
  
|속성|형식|RW|Default|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|보고서 설정|왼쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|MarginRight|Double|RW|보고서 설정|오른쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|MarginTop|Double|RW|보고서 설정|위쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|MarginBottom|Double|RW|보고서 설정|아래쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|PageWidth|Double|RW|보고서 설정|페이지 너비를 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서 정의에 지정되지 않은 경우 기본값은 215.9밀리미터입니다.|  
|PageHeight|Double|RW|보고서 설정|페이지 높이를 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서 정의에 지정되지 않은 경우 기본값은 279.4밀리미터입니다.|  
|Culture|Int32|RW|브라우저 로캘|LCID(로캘 ID)를 지정합니다. 이 값에 따라 사용자 입력 단위가 결정됩니다. 예를 들어, 사용자가 `3`, 언어가 영어 (미국) 이면 인치 프랑스어 이면 값이 밀리미터 단위로 측정 됩니다. 유효한 값은 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082와 같습니다.|  
|UICulture|String|RW|클라이언트 culture|대화 상자의 문자열 지역화를 지정합니다. 인쇄 대화 상자의 텍스트는 독일어, 스페인어, 영어, 이탈리아어, 일본어, 중국어 간체, 중국어 번체, 프랑스어 및 한국어와 같은 언어로 지역화됩니다. 유효한 값은 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082와 같습니다.|  
|Authenticate|Boolean|RW|False|사용 가능한 세션이 없는 인쇄에 대한 연결을 시작하기 위해 컨트롤이 보고서 서버에 대해 GET 명령을 실행할지 여부를 지정합니다.|  
  
### <a name="when-to-set-the-authenticate-property"></a>인증 속성 설정 시기  
 브라우저 세션 내에서 인쇄할 때 `Authenticate` 속성을 설정할 필요가 없습니다. 활성 세션의 컨텍스트 내에서 인쇄 제어에서 보고서 서버까지의 모든 요청은 브라우저를 통해 처리됩니다. 브라우저는 보고서 서버와 통신하는 데 필요한 세션 변수를 설정합니다.  
  
 보고서를 먼저 열어 보지 않고 직접 프린터로 보내는 것처럼 사용 가능하지 않은 세션을 인쇄하는 경우 인쇄 컨트롤은 HTTP `GET` 요청을 실행하여 보고서 서버에 세션을 설정해야 합니다. `GET` 요청을 실행하려면 `Authenticate`를 `True`로 설정합니다.  
  
 Windows 통합 보안 또는 기본 인증을 사용하는 경우에만 `GET` 요청을 실행합니다. 폼 인증을 사용하는 경우 `Authenticate` 속성이 무시됩니다. 응용 프로그램 코드에서 세션을 설정하고 제공한 사용자 지정 보안 확장 프로그램을 사용하여 사용자를 인증해야 합니다. 폼 인증을 사용하는 경우 인증 쿠키에 대한 만료 값을 적절한 간격으로 세션을 유지하는 값으로 설정합니다. 값이 너무 낮으면 쿠키가 만료될 때마다 로그온 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
### <a name="clsids"></a>CLSID  
 온-프레미스 보고서를 실행 중인 경우 다음과 같은 CLSID 값을 사용합니다.  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 Microsoft Azure SQL Reporting에서 보고서를 실행 중인 경우 다음과 같은 CLSID 값을 사용합니다.  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>Print 메서드에 대한 RSPrintClient 지원  
 **RSClientPrint** 개체는 인쇄 대화 상자를 시작하는 데 사용되는 **Print** 메서드를 지원합니다. 다음은 **Print** 메서드에 사용되는 인수입니다.  
  
|인수|입력/출력|형식|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|입력|String|보고서 서버 가상 디렉터리를 지정 합니다 (예를 들어 https://adventure-works/reportserver)합니다.|  
|ReportPathParameters|입력|String|보고서 서버 폴더 네임스페이스에 있는 보고서의 전체 이름을 매개 변수를 포함하여 지정합니다. 보고서는 URL 액세스를 통해 검색됩니다. 예제: "/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234"|  
|ReportName|입력|String|보고서의 짧은 이름입니다. 위의 예에서 짧은 이름은 Employee Sales Summary입니다. 짧은 이름은 인쇄 대화 상자와 인쇄 큐에 나타납니다.|  
  
### <a name="example"></a>예제  
 다음 HTML 예에서는 JavaScript에서 .cab 파일, **Print** 메서드 및 속성을 지정하는 방법을 보여 줍니다.  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>관련 항목  
 [인쇄 컨트롤을 사용하여 브라우저에서 보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../report-builder/print-reports-report-builder-and-ssrs.md)   
 [이미지 장치 정보 설정](../../image-device-information-settings.md)  
  
  
