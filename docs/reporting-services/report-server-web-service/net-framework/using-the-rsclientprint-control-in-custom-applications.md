---
title: "사용자 지정 응용 프로그램에서 RSClientPrint 컨트롤을 사용 하 여 | Microsoft Docs"
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
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8afee187160da9d35efd0c7079b649bac7e73740
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>사용자 지정 응용 프로그램에서 RSClientPrint 컨트롤 사용
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX 컨트롤 **RSPrintClient**, HTML 뷰어에 표시 되는 보고서에 대 한 클라이언트 쪽 인쇄를 제공 합니다. 제공 된 **인쇄** 대화 상자를 사용자가 인쇄 작업을 시작, 보고서 미리 보기, 인쇄할 페이지를 지정 하 고 여백을 변경 합니다. 클라이언트 쪽 인쇄 작업 과정에서 보고서 서버는 이미지(EMF) 렌더링 확장 프로그램으로 보고서를 렌더링하고 운영 체제의 인쇄 기능으로 인쇄 작업을 만들어 프린터에 보냅니다.  
  
 클라이언트 쪽 인쇄 기능은 사용자 컴퓨터의 브라우저 인쇄 설정을 무시하고 대신 인쇄 출력을 만드는 데 보고서의 페이지 크기, 여백, 머리글 및 바닥글 텍스트를 사용하여 HTML 보고서의 인쇄 품질을 제어하고 향상시킬 수 있습니다. 인쇄 컨트롤은 보고서의 속성 값을 읽어 페이지 크기와 여백 설정을 지정합니다.  
  
 타사 도구 모음이 나 뷰어에서 클라이언트 쪽 인쇄 기능을 사용 하도록 설정 하는 개발자를 통해 ActiveX 컨트롤에 액세스할 수는 **RSClientPrint** COM 개체입니다. 컨트롤은 무료로 배포됩니다. 다음 목록에서는 컨트롤 사용에 대한 권장 사항을 나열합니다.  
  
-   컨트롤을 사용하여 웹 기반 보고서의 인쇄 품질을 향상시킬 수 있습니다. 개체를 지정할 수 있습니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-호환 되는 프로그래밍 언어 또는 스크립트입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Forms 응용 프로그램에서는 컨트롤을 사용할 수 없습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 프로그램 파일에서 .cab 파일을 복사하여 사용자 지정 응용 프로그램 코드베이스에 추가합니다.  
  
-   사용 하 여는 \<개체 > 태그의 제어를 지정할 수 있습니다.  
  
-   OBJECT CODEBASE 특성에서 .cab 파일의 상대 URL이나 정규화된 URL을 지정합니다.  
  
-   .cab 파일에 대한 사용자의 응용 프로그램 버전 정보를 지정하여 응용 프로그램에 사용되는 버전을 추적합니다.  
  
-   이미지(EMF) 렌더링에 대한 온라인 설명서 항목을 검토하여 인쇄 미리 보기와 출력을 위해 페이지가 렌더링되는 방법을 이해합니다.  
  
## <a name="rsprintclient-overview"></a>RSPrintClient 개요  
 이 컨트롤은 특정 페이지와 범위, 페이지 여백 및 방향을 지정하는 페이지 선택 기능, 인쇄 미리 보기 기능을 비롯하여 다른 인쇄 대화 상자에 공통적인 기능을 지원하는 사용자 지정 인쇄 대화 상자를 표시합니다. 컨트롤은 CAB 파일로 패키지됩니다. 텍스트는 **인쇄** 대화 상자에서 지원 되는 언어의 모든 언어로 지역화 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. **RSPrintClient** ActiveX 컨트롤 이미지 렌더링 확장 프로그램 (EMF)를 사용 하 여 보고서를 인쇄 합니다. 다음 EMF 장치 정보 사용: StartPage, EndPage, MarginBottom, MarginLeft, MarginTop, MarginRight, PageHeight 및 PageWidth 합니다. 이미지 렌더링에 대한 다른 장치 정보 설정은 지원되지 않습니다.  
  
### <a name="language-support"></a>언어 지원  
 인쇄 컨트롤은 여러 언어로 사용자 인터페이스 텍스트를 제공하며 여러 단위의 입력 값을 허용합니다. 사용 되는 언어와 단위 시스템에 의해 결정 됩니다는 **문화권** 및 **UICulture** 속성입니다. 두 속성 모두 LCID 값을 사용합니다. 지원되는 언어의 변형 언어에 대한 LCID를 지정하는 경우 이에 가장 근접한 언어가 사용됩니다. 지원되지 않는 LCID를 지정하는 경우 이와 근접한 LCID가 없으면 영어(미국)가 사용됩니다.  
  
## <a name="using-rsclientprint-in-code"></a>코드에서 RSClientPrint 사용  
 **RSClientPrint** 개체 ActiveX 컨트롤 및 해당 메서드 및 속성에 프로그래밍 방식으로 액세스 하는 데 사용 됩니다. 이 컨트롤은 인쇄 미리 보기를 위한 모달 대화 상자를 제공합니다.  
  
### <a name="specifying-default-values"></a>기본값 지정  
 초기화할 수는 **인쇄** 보고서의 페이지 및 여백 값이 있는 대화 상자. 기본적으로는 **인쇄** 대화 상자는 보고서 정의의 값으로 초기화 됩니다. 기본값을 사용하거나 개체의 속성을 설정하여 다른 값을 지정할 수 있습니다.  
  
 모든 치수는 밀리미터 단위로 설정됩니다. 경우 런타임에 단위가 변환 발생는 **문화권** 및 **u r e** 미터법을 사용 하지 않는 로캘로 설정 됩니다.  
  
 페이지 크기와 여백에 사용 되는 값을 이해 하려면 사용할 수 있습니다는 **GetProperties** 기본 값을 검색 하는 메서드입니다.  
  
-   **PageHeight** 및 **PageWidth** 기본 페이지 높이 너비를 지정 합니다. 인쇄 컨트롤이 시작되면 이러한 속성 값을 기준으로 현재 선택한 프린터에서 사용할 수 있는 가장 근접한 용지 크기가 선택됩니다. 경우 **PageWidth** 보다 크면 **PageHeight**, 고 방향은 가로로 설정 됩니다. 그렇지 않으면 용지 방향이 세로로 설정됩니다.  
  
-   **LeftMargin**, **RightMargin**, **TopMargin**, 및 **BottomMargin** 12.2 밀리미터로 기본적으로 모두 설정 되어 있습니다.  
  
 이러한 속성에 저장 됩니다는 **항목** 보고서 서버에 대 한 속성 컬렉션입니다. 보고서 정의가 업데이트될 때마다 속성 값을 덮어씁니다.  
  
### <a name="rsclientprint-properties"></a>RSClientPrint 속성  
  
|속성|유형|RW|기본값|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|보고서 설정|왼쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|MarginRight|Double|RW|보고서 설정|오른쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|MarginTop|Double|RW|보고서 설정|위쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|MarginBottom|Double|RW|보고서 설정|아래쪽 여백을 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서에 지정되지 않은 경우 기본값은 12.2밀리미터입니다.|  
|PageWidth|Double|RW|보고서 설정|페이지 너비를 가져오거나 설정합니다. 보고서 정의 즉 개발자가 설정 되지 않은 경우 기본값은 215.9 밀리미터입니다.|  
|PageHeight|Double|RW|보고서 설정|페이지 높이를 가져오거나 설정합니다. 개발자가 설정하지 않았거나 보고서 정의에 지정되지 않은 경우 기본값은 279.4밀리미터입니다.|  
|Culture|Int32|RW|브라우저 로캘|LCID(로캘 ID)를 지정합니다. 이 값에 따라 사용자 입력 단위가 결정됩니다. 예를 들어 사용자가 **3**, 경우 언어가 프랑스어 또는 언어는 영어 (미국) 이면 인치 값이 밀리미터 단위로 측정 됩니다. 유효한 값: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082 합니다.|  
|UICulture|문자열|RW|클라이언트 culture|대화 상자의 문자열 지역화를 지정합니다. 인쇄 대화 상자에서 텍스트 이러한 언어로 지역화 됩니다: 중국어 간체, 중국어 번체, 영어, 프랑스어, 독일어, 이탈리아어, 일본어, 한국어, 및 스페인어입니다. 유효한 값: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082 합니다.|  
|Authenticate|Boolean|RW|False|사용 가능한 세션이 없는 인쇄에 대한 연결을 시작하기 위해 컨트롤이 보고서 서버에 대해 GET 명령을 실행할지 여부를 지정합니다.|  
  
### <a name="when-to-set-the-authenticate-property"></a>인증 속성 설정 시기  
 브라우저 세션 내에서 인쇄 하면 필요가 없습니다 설정 하는 **Authenticate** 속성입니다. 활성 세션의 컨텍스트 내에서 인쇄 제어에서 보고서 서버까지의 모든 요청은 브라우저를 통해 처리됩니다. 브라우저는 보고서 서버와 통신하는 데 필요한 세션 변수를 설정합니다.  
  
 인쇄 컨트롤은 HTTP를 실행 해야 합니다 (예: 보고서를 먼저 열지 않고도 프린터에 직접 보내기) 세션 아웃을 인쇄 하면 **가져오기** 요청을 보고서 서버와 함께 세션을 설정 합니다. 문제에는 **가져오기** 요청 설정한 **Authenticate** 를 **True**합니다.  
  
 발급 해야는 **가져오기** 요청이 Windows를 사용 하는 경우 통합 보안 이나 기본 인증이 있습니다. 폼 인증을 사용 하는 경우는 **Authenticate** 속성은 무시 됩니다. 응용 프로그램 코드에서 세션을 설정하고 제공한 사용자 지정 보안 확장 프로그램을 사용하여 사용자를 인증해야 합니다. 폼 인증을 사용하는 경우 인증 쿠키에 대한 만료 값을 적절한 간격으로 세션을 유지하는 값으로 설정합니다. 값이 너무 낮으면 쿠키가 만료될 때마다 로그온 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
### <a name="clsids"></a>CLSID  
 온-프레미스 보고서를 실행 중인 경우 다음과 같은 CLSID 값을 사용합니다.  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 Microsoft Azure SQL Reporting에서 보고서를 실행 중인 경우 다음과 같은 CLSID 값을 사용합니다.  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>Print 메서드에 대한 RSPrintClient 지원  
 **RSClientPrint** 지원 개체는 **인쇄** 메서드 인쇄 대화 상자를 시작 하는 데 사용 합니다. **인쇄** 메서드는 인수는 다음과 같습니다.  
  
|인수|입력/출력|유형|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|입력|문자열|보고서 서버 가상 디렉터리를 지정 합니다 (예를 들어 `https://adventure-works/reportserver`).|  
|ReportPathParameters|입력|문자열|보고서 서버 폴더 네임스페이스에 있는 보고서의 전체 이름을 매개 변수를 포함하여 지정합니다. 보고서는 URL 액세스를 통해 검색됩니다. 예: "/ AdventureWorks Sample Reports/Employee Sales summary&empid = 1234"|  
|ReportName|입력|문자열|보고서의 짧은 이름입니다. 위의 예에서 짧은 이름은 Employee Sales Summary입니다. 짧은 이름은 인쇄 대화 상자와 인쇄 큐에 나타납니다.|  
  
### <a name="example"></a>예제  
 다음 HTML 예제의.cab 파일을 지정 하는 방법을 보여 줍니다 **인쇄** 방법과 javascript에서 속성:  
  
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
  
## <a name="see-also"></a>참고 항목  
 [인쇄 컨트롤 &#40;를 사용 하 여 브라우저에서 보고서 인쇄 보고서 작성기 및 SSRS &#41;](../../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [이미지 장치 정보 설정](../../../reporting-services/image-device-information-settings.md)  
  
  
