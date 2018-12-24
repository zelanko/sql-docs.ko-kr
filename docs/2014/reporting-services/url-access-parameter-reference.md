---
title: URL 액세스 매개 변수 참조 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], display options
- URL access [Reporting Services], report display parameters
ms.assetid: 1c3e680a-83ea-4979-8e79-fa2337ae12a3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2bdae6fe44e416786e842eb2ecc36d213d771cf7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179243"
---
# <a name="url-access-parameter-reference"></a>URL 액세스 매개 변수 참조
  보고서의 모양과 느낌을 구성하는 URL의 일부로 다음 매개 변수를 사용할 수 있습니다. 이 섹션에는 가장 일반적인 매개 변수가 나열됩니다. 매개 변수는 대/소문자를 구분하지 않으며, 매개 변수 접두사는 보고서 서버로 전달되는 경우 *rs:* 로 시작하고 HTML 뷰어로 전달되는 경우 *rc:* 로 시작합니다. 디바이스 또는 렌더링 확장 프로그램에 특정하는 매개 변수를 지정할 수도 있습니다. 장치별 매개 변수에 대 한 자세한 내용은 참조 하세요. [URL에 장치 정보 설정 지정](specify-device-information-settings-in-a-url.md)합니다.  
  
> [!IMPORTANT]  
>  URL에는 SharePoint를 통해 요청을 라우팅하는 `_vti_bin` 프록시 구문과 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP 프록시를 포함하는 것이 중요합니다. 프록시는 몇 가지 컨텍스트를 HTTP 요청에 추가하며 이 컨텍스트는 SharePoint 모드 보고서 서버에 대한 보고서의 올바른 실행을 보장하는 데 필요합니다. 예제를 보려면 [액세스 보고서 Server Items Using URL Access](access-report-server-items-using-url-access.md)합니다.  
>   
>  URL에 보고서 매개 변수를 포함하는 방법에 대한 자세한 내용과 예를 보려면 [Pass a Report Parameter Within a URL](pass-a-report-parameter-within-a-url.md)을 참조하십시오.  
  
## <a name="html-viewer-commands-rc"></a>HTML 뷰어 명령(rc:)  
 다음 표에서 접두사로 사용 하는 URL 액세스 매개 변수를 설명 *rc:* HTML 뷰어를 대상 하는 데 사용 됩니다.  
  
|매개 변수|Description|값|  
|---------------|-----------------|------------|  
|*도구 모음*|도구 모음을 표시하거나 숨깁니다.<br /><br /> **\*\* 중요 \* \***  *rc: toolbar* = `false` 에 호스팅된 보고서를 대상으로 도메인 이름 대신 IP를 사용 하는 URL 액세스 문자열 주소에 대해 작동 하지 않습니다는 SharePoint 사이트입니다.|이 매개 변수 값이 `false`이면 모든 나머지 옵션이 무시됩니다. 이 매개 변수를 생략하면 도구 모음이 지원하는 렌더링 형식에 맞게 자동으로 표시됩니다. 이 매개 변수의 기본값은 `true`합니다.<br /><br /> `true` <br /> `false`|  
|*매개 변수*|도구 모음의 매개 변수 영역을 표시하거나 숨깁니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales&rc:Parameters=Collapsed`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Parameters=Collapsed`|이 매개 변수를 `true`로 설정하면 도구 모음의 매개 변수 영역이 표시됩니다. 이 매개 변수를 `false`로 설정하면 매개 변수 영역이 표시되지 않고 사용자가 영역을 표시할 수 없습니다. 이 매개 변수를 `Collapsed` 값으로 설정하면 매개 변수 영역이 표시되지 않지만 최종 사용자가 영역을 토글할 수 있습니다. 이 매개 변수의 기본값은 `true`입니다. 유효한 값은<br /><br /> `true` <br /> `false` <br /> `Collapsed`|  
|*확대/축소*|보고서 확대/축소 값을 정수 백분율 또는 문자열 상수로 설정합니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales&rc:Zoom=Page Width`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Zoom=Page Width`|표준 문자열 값에는 `Page Width` 및 `Whole Page`가 포함됩니다. Internet Explorer 5.0 이전 버전과 모든 비[!INCLUDE[msCoName](../includes/msconame-md.md)] 브라우저에서는 이 매개 변수가 무시됩니다. 이 매개 변수의 기본값은 `100`입니다.|  
|*섹션*|보고서에 표시할 페이지를 설정합니다.<br /><br /> `Native` 보고서의 2 페이지를 표시 하는 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales&rc:Section=2`<br /><br /> `SharePoint` 보고서의 2 페이지를 표시 하는 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:Section=2`|보고서의 페이지 수보다 큰 값을 입력하면 마지막 페이지가 표시됩니다. `0`보다 작은 값을 입력하면 보고서의 1페이지가 표시됩니다. 이 매개 변수의 기본값은 `1`입니다.|  
|*FindString*|보고서에서 텍스트의 특정 집합을 검색합니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales&rc:FindString=Mountain-400`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rc:FindString=Mountain-400`||  
|*StartFind*|검색할 마지막 섹션을 지정합니다.<br /><br /> `Native` 모드 예제 Product Catalog 예제에서 "Mountain-400" 텍스트의 첫 번째 검색 1 페이지부터 5 페이지까지 보고서는:<br /><br /> `http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400`|이 매개 변수의 기본값은 보고서의 마지막 페이지입니다.|  
|*EndFind*|검색에 사용할 마지막 페이지 번호를 설정합니다. 예를 들어 값 `5` 검색할 마지막 페이지가 보고서의 5 페이지 임을 나타냅니다. 이 매개 변수는 *StartFind* 매개 변수와 함께 사용하십시오. 위의 예제를 참조 하세요 *StartFind* 합니다.|기본값은 현재 페이지 번호입니다.|  
|*FallbackPage*|검색 또는 문서 구조 선택을 실패할 때 표시할 페이지 번호를 설정합니다.|기본값은 현재 페이지 번호입니다.|  
|*GetImage*|HTML 뷰어 사용자 인터페이스에 대한 특정 아이콘을 가져옵니다.||  
|*아이콘*|특정 렌더링 확장 프로그램의 아이콘을 가져옵니다.||  
|*스타일 시트*|HTML 뷰어에 적용할 스타일시트를 지정합니다.||  
|장치 정보 설정|형식의 장치 정보 설정을 지정 `rc:tag=value`, 여기서 *태그* 장치 정보 현재 사용 되는 렌더링 확장 프로그램별 설정의 이름입니다 (에 대 한 설명을 참조는  *형식* 매개 변수). 예를 들어 이미지 렌더링 확장 프로그램에서 URL 액세스 문자열에 다음 매개 변수를 사용하는 JPEG 이미지에 보고서를 렌더링할 수 있도록 *OutputFormat* 디바이스 정보 설정을 사용할 수 있습니다. `…&rs:Format=IMAGE&rc:OutputFormat=JPEG` 모든 확장 프로그램별 장치 정보 설정에 대한 자세한 내용은 [렌더링 확장 프로그램에 대한 장치 정보 설정&#40;Reporting Services&#41;](device-information-settings-for-rendering-extensions-reporting-services.md)을 참조하세요.||  
  
## <a name="report-server-commands-rs"></a>보고서 서버 명령(rs:)  
 다음 표에서 접두사로 사용 하는 URL 액세스 매개 변수를 설명 *rs:* 보고서 서버를 대상 하는 데 사용 됩니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*Command*|해당 항목 유형에 따라 카탈로그 항목에 동작을 수행합니다. 기본값은 URL 액세스 문자열에 참조된 카탈로그 항목의 유형에 의해 결정됩니다. 유효한 값은<br /><br /> `ListChildren` 및 `GetChildren` 폴더의 내용을 표시 합니다. 폴더 항목은 일반 항목 탐색 페이지 내에 표시됩니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`|  
||`Render` 지정된 된 보고서를 렌더링합니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`|  
||`GetSharedDatasetDefinition` 공유 데이터 집합과 관련 된 XML 정의 표시 합니다. 쿼리, 데이터 집합 매개 변수, 기본값, 데이터 집합 필터, 데이터 정렬 및 대/소문자 구분 등의 데이터 옵션을 포함하여 공유 데이터 집합 속성이 정의에 저장됩니다. 이 값을 사용하려면 공유 데이터 집합에 대한 **보고서 정의 읽기** 권한이 있어야 합니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
||`GetDataSourceContents` 주어진된 공유 데이터 원본의 속성을 XML로 표시 됩니다. 브라우저에서 XML를 지원 하 고 인증된 된 사용자가 있다면 `Read Contents` 데이터 원본, 데이터 원본 정의에 대 한 권한이 표시 됩니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`|  
||`GetResourceContents` 리소스를 렌더링 하 고 리소스가 브라우저와 호환 되 면이 HTML 페이지에 표시 합니다. 그렇지 않으면 파일 또는 리소스를 열거나 디스크에 저장하라는 메시지가 나타납니다.<br /><br /> `Native` 모드 예제:<br /><br /> `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`<br /><br /> `SharePoint` 모드 예제:<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`|  
||`GetComponentDefinition` 게시 된 보고서 항목과 연결 된 XML 정의 표시 합니다. 있어야 `Read Contents` 이 값을 사용 하도록 게시 된 보고서 항목에 대 한 권한이 있습니다.|  
|*형식*|보고서를 렌더링할 형식을 지정합니다. 일반적인 값은 `ATOM`, `HTML4.0`, `MHTML`, `IMAGE`, `EXCEL`, `WORD`, `CSV`, `PDF`, `XML`입니다. 기본값은 `HTML4.0`입니다. 자세한 내용은 [Export a Report Using URL Access](export-a-report-using-url-access.md)를 참조하세요.<br /><br /> 예를 들어 `Native` 모드 보고서 서버에서 직접 보고서 PDF 복사본을 가져오는 경우 다음을 사용합니다.<br /><br /> `http://myrshost/ReportServer?/myreport&rs:Format=PDF`<br /><br /> 예를 들어 `SharePoint` 모드입니다.<br /><br /> `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF`|  
|*ParameterLanguage*|브라우저 언어와 독립적으로 URL에 전달되는 매개 변수의 언어를 제공합니다. 기본값은 브라우저 언어입니다. 값 수는 문화권 값 같은 `en-us` 또는 `de-de.`<br /><br /> 브라우저 언어를 재정의하고 문화권 값을 de-DE로 지정하는 `Native` 모드의 예제입니다.<br /><br /> `http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE`|  
|*스냅숏*|보고서 기록 스냅숏을 기반으로 보고서를 렌더링합니다. 자세한 내용은 [렌더링 된 보고서 기록 스냅숏 Using URL Access](render-a-report-history-snapshot-using-url-access.md)합니다.<br /><br /> 타임스탬프가 13:40:02인 2003-04-07 날짜의 보고서 기록 스냅숏을 검색하는 `Native` 모드의 예제입니다.<br /><br /> `http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02`|  
|*PersistStreams*|보고서를 단일 지속형 스트림에서 렌더링합니다. 이 매개 변수는 이미지 렌더러에서 렌더링된 보고서를 한 번에 한 청크씩 전송하는 데 사용됩니다. 이 매개 변수를 URL 액세스 문자열에 사용한 후에는 *GetNextStream* 매개 변수 대신 *PersistStreams* 매개 변수를 사용하여 지속형 스트림의 다음 청크를 가져옵니다. 이 URL 명령은 결과적으로 지속형 스트림의 끝을 나타내는 0바이트 스트림을 반환합니다. 기본값은 `false`입니다.|  
|*GetNextStream*|*PersistStreams* 매개 변수를 사용하여 액세스하는 지속형 스트림의 다음 데이터 청크를 가져옵니다. 자세한 내용은 *PersistStreams*에 대한 설명을 참조하십시오. 기본값은 `false`입니다.|  
|*세션 Id*|클라이언트 응용 프로그램과 보고서 서버 간에 설정된 활성 보고서 세션을 지정합니다. 이 매개 변수의 값은 세션 식별자로 설정됩니다.<br /><br /> 세션 ID를 쿠키로 지정하거나 URL의 일부로 지정할 수 있습니다. 보고서 서버가 세션 쿠키를 사용하지 않도록 구성된 경우 지정된 세션 ID가 없는 첫 번째 요청은 세션 ID가 있는 항목으로 리디렉션됩니다. 보고서 서버 세션에 대 한 자세한 내용은 참조 하세요. [Identifying Execution State](report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)합니다.|  
|*ClearSession*|`true` 값은 보고서 서버가 보고서 세션에서 보고서를 제거하도록 합니다. 인증된 사용자와 연관된 모든 보고서 인스턴스가 보고서 세션에서 제거됩니다. 보고서 인스턴스는 다양한 보고서 매개 변수 값을 사용하여 여러 번 실행되는 동일한 보고서로 정의됩니다. 기본값은 `false`입니다.|  
|*ResetSession*|`true` 값은 보고서 서버가 보고서 세션과 모든 보고서 스냅숏의 연결을 제거하여 보고서 세션을 다시 설정하도록 합니다. 기본값은 `false`입니다.|  
|*ShowHideToggle*|보고서의 섹션의 표시/숨기기 상태를 토글합니다. 토글할 섹션을 나타내는 양의 정수를 지정합니다.|  
  
## <a name="report-viewer-web-part-commands-rv"></a>보고서 뷰어 웹 파트 명령(rv:)  
 다음 표에서는 SharePoint와 통합된 보고서 뷰어 웹 파트를 타켓팅하는 데 사용되는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 예약된 보고서 매개 변수 이름에 대해 설명합니다. 이러한 매개 변수 이름은 접두사 *rv:* 로 시작합니다. 보고서 뷰어 웹 파트에는 *rs:ParameterLanguage* 매개 변수도 사용할 수 있습니다.  
  
|매개 변수|작업|  
|---------------|------------|  
|*도구 모음*|보고서 뷰어 웹 파트에 대한 도구 모음 표시를 제어합니다. 기본값은 `Full`입니다. 사용할 수 있는 값에는<br /><br /> `Full`: 전체 도구 모음을 표시합니다.<br /><br /> `Navigation`: 도구 모음에 페이지 매김만 표시합니다.<br /><br /> `None`: 도구 모음을 표시하지 않습니다.<br /><br /> <br /><br /> 예를 들어 `SharePoint` 모드에서는 도구 모음에 페이지 매김만 표시합니다.<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:Toolbar=Navigation`|  
|*HeaderArea*|보고서 뷰어 웹 파트에 대한 머리글 표시를 제어합니다. 기본값은 `Full`입니다. 사용할 수 있는 값에는<br /><br /> `Full`: 전체 머리글을 표시합니다.<br /><br /> `BreadCrumbsOnly`: 응용 프로그램에는 사용자에 게 알려 머리글에 bread-crumb 탐색만 표시 합니다.<br /><br /> `None`: 머리글을 표시하지 않습니다.<br /><br /> <br /><br /> 예를 들어 `SharePoint` 모드에서는 머리글에 bread-crumb 탐색만 표시합니다.<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:HeaderArea=BreadCrumbsOnly`|  
|*DocMapAreaWidth*|보고서 뷰어 웹 파트에서 매개 변수 영역의 표시 너비(픽셀 단위)를 제어합니다. 기본값은 보고서 뷰어 웹 파트 기본값과 같습니다. 값은 음의 정수가 아니어야 합니다.|  
|*AsyncRender*|보고서가 비동기적으로 렌더링되는지 여부를 제어합니다. 기본값은 `true`, 보고서를 비동기적으로 렌더링 됨을 지정 합니다. 부울 값 `true` 또는 `false`여야 합니다.|  
|*ParamMode*|보고서 뷰어 웹 파트의 매개 변수 프롬프트 영역이 전체 페이지 뷰에서 표시되는 방식을 제어합니다.  기본값은 `Full`입니다. 유효한 값은<br /><br /> `Full`: 매개 변수 프롬프트 영역을 표시 합니다.<br /><br /> `Collapsed`: 매개 변수 프롬프트 영역을 축소 합니다.<br /><br /> `Hidden`: 매개 변수 프롬프트 영역을 숨깁니다.<br /><br /> 예를 들어 `SharePoint` 모드에서는 매개 변수 프롬프트 영역을 축소합니다.<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ParamMode=Collapsed`|  
|*DocMapMode*|보고서 뷰어 웹 파트의 문서 구조 영역이 전체 페이지 뷰에서 표시되는 방식을 제어합니다. 기본값은 `Full`입니다. 유효한 값은<br /><br /> `Full`: 문서 구조 영역을 표시합니다.<br /><br /> `Collapsed`: 문서 구조 영역을 축소 합니다.<br /><br /> `Hidden`: 문서 구조 영역을 숨깁니다.|  
|*DockToolBar*|보고서 뷰어 웹 파트의 도구 모음이 위쪽이나 아래쪽에 도킹되는지 여부를 제어합니다. 유효한 값은 `Top` 고 `Bottom`입니다. 기본값은 `Top`입니다.<br /><br /> <br /><br /> 예를 들어 `SharePoint` 모드에서는 도구 모음을 아래쪽에 도킹합니다.<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:DockToolBar=Bottom`|  
|*ToolBarItemsDisplayMode*|도구 모음 항목 표시 여부를 제어합니다. 비트 열거 값입니다. 도구 모음 항목을 추가하려면 합계 값에 항목의 값을 추가합니다. 예를 들어 동작 없음 메뉴의 경우 rv:ToolBarItemsDisplayMode=63(또는 0x3F)(1+2+4+8+16+32)을 사용하며, 동작 메뉴의 경우에만 rv:ToolBarItemsDisplayMode=960(또는 0x3C0)을 사용합니다.  기본값은 `-1`, 도구 모음 항목을 모두 포함 합니다. 유효한 값은<br /><br /> 1(0x1): **뒤로** 단추<br /><br /> 2 (0x2): 텍스트 검색 컨트롤<br /><br /> 4 (0x4): 페이지 탐색 컨트롤<br /><br /> 8(0x8): **새로 고침** 단추<br /><br /> 16(0x10): **확대/축소** 목록 상자<br /><br /> 32(0x20): **ATOM 피드** 단추<br /><br /> 64(0x40): **동작** 의 **인쇄**메뉴 옵션<br /><br /> 128(0x80): **동작** 의 **내보내기**하위 메뉴<br /><br /> 256(0x100: **동작** 의 **보고서 작성기로 열기**메뉴 옵션<br /><br /> 512(0x200: **동작** 의 **구독**메뉴 옵션<br /><br /> 1024(0x400: **동작** 의 **새 데이터 경고**메뉴 옵션<br /><br /> 예를 들어 `SharePoint` 모드 에서만 표시 합니다 **다시** 단추, 텍스트 검색 컨트롤, 페이지 탐색 컨트롤 및 **새로 고침** 단추입니다.<br /><br /> `http://myspsite/_vti_bin/reportserver?http://myspsite002%fShared+Documents%2fmyreport.rdl&rv:DocMapMode=Displayed&rv:ToolBarItemsDisplayMode=15`|  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스&#40;SSRS&#41;](url-access-ssrs.md)  
  
  
