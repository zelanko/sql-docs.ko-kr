---
title: HTML 장치 정보 설정 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- HTML [Reporting Services], rendering
- device information settings [Reporting Services], HTML rendering
ms.assetid: f505f478-dd6d-444a-957c-34f7cfb98911
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a8acf400f03ec77aff21d839dee132ba5258f54f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403638"
---
# <a name="html-device-information-settings"></a>HTML 장치 정보 설정
다음 표에서는 HTML 형식으로 렌더링하기 위한 장치 정보 설정을 보여 줍니다.  
  
> [!IMPORTANT]  
>  아래 표에 **(\*)** 와 함께 나열된 장치 정보 설정은 더 이상 사용되지 않으므로 새 응용 프로그램에서 사용하지 않아야 합니다. 자세한 내용은 [SQL Server 2016의 SQL Server Reporting Services에서 지원되지 않는 기능](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)   
  
|설정|값|  
|-------------|-----------|  
|**AccessibleTablix**|화면 판독기에 사용되는 추가적인 내게 필요한 옵션 메타데이터를 사용하여 렌더링할지 여부를 나타냅니다. 추가적인 내게 필요한 옵션 메타데이터를 사용하면 렌더링되는 보고서가 Electronic and Information Technology Accessibility Standards (Section 508) 문서의 "Web-based Intranet and Internet Information and Applications" 섹션(1194.22)에 나오는 다음 기술 표준과 호환됩니다.<br /><br /> (g) 데이터 테이블의 행 및 열 머리글을 식별해야 합니다.<br /><br /> (h) 행 또는 열 머리글의 논리적 수준이 둘 이상인 데이터 테이블에서 태그를 사용하여 데이터 셀과 머리글 셀을 연결해야 합니다.|  
|**ActionScript(\*)**|드릴스루 또는 책갈피 클릭 등의 동작 이벤트가 발생할 때 사용할 JavaScript 함수 이름을 지정합니다. 이 매개 변수를 지정하면 동작 이벤트가 서버에 대한 포스트백 대신 명명된 JavaScript 함수를 트리거합니다.|  
|**BookmarkID**|보고서에서 이동할 책갈피 ID입니다.|  
|**DocMap**|보고서 문서 구조를 표시할지, 아니면 숨길지 나타냅니다. 이 매개 변수의 기본값은 **true**입니다.|  
|**ExpandContent**|보고서가 가로 크기를 제한하는 테이블 구조에 포함되어야 하는지 여부를 나타냅니다.|  
|**FindString**|보고서에서 검색할 텍스트입니다. 이 매개 변수의 기본값은 빈 문자열입니다.|  
|**GetImage(\*)**|HTML 뷰어 사용자 인터페이스에 대한 특정 아이콘을 가져옵니다.|  
|**HTMLFragment**|전체 HTML 문서 대신 HTML 조각이 만들어지는지 여부를 나타냅니다. HTML 조각은 TABLE 요소에 보고서 내용을 포함하며 HTML 및 BODY 요소를 생략합니다. 기본 값은 **false**입니다. SOAP API의 **M:ReportExecution2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@, ReportExecution2005.Warning[]@,System.String[]@)** 메서드를 사용하여 HTML로 렌더링하는 경우 이미지를 사용하여 보고서를 렌더링하려면 이 장치 정보를 **true** 로 설정해야 합니다. **HTMLFragment** 속성이 **true** 로 설정된 SOAP을 사용하여 렌더링하면 이미지를 올바르게 요청하는 데 사용할 수 있는 세션 정보가 포함된 URL이 만들어집니다. 이미지는 보고서 서버 데이터베이스에 업로드된 리소스여야 합니다.|  
|**ImageConsolidation**|렌더링되는 차트, 지도, 계기 및 표시기 이미지를 하나의 큰 이미지로 통합할지 여부를 나타냅니다. 이미지를 통합하면 보고서에 데이터 시각화 항목이 다수 포함된 경우 클라이언트 브라우저에서 보고서 성능이 향상됩니다. 근래에 사용되는 대부분의 브라우저에서 이 설정의 기본값은 **true** 입니다.|  
|**JavaScript**|렌더링된 보고서에서 JavaScript가 지원되는지 여부를 나타냅니다. 기본값은 **true**입니다.|  
|**LinkTarget**|보고서에서 하이퍼링크에 대한 대상입니다. **LinkTarget**=*window_name*과 같이 창의 이름을 제공하여 창 또는 프레임을 대상으로 하거나 **LinkTarget**=_blank를 사용하여 새 창을 대상으로 할 수 있습니다. 기타 유효한 대상 이름에는 _self, _parent 및 _top이 포함됩니다.|  
|**OnlyVisibleStyles(\*)**|현재 렌더링된 페이지에 대한 공유 스타일만 생성됨을 나타냅니다.|  
|**OutlookCompat**|Outlook에서 보고서를 보기 좋게 만들어 주는 메타데이터와 함께 렌더링할지 여부를 나타냅니다. 기타의 경우 기본값은 **false**입니다.|  
|**매개 변수**|도구 모음의 매개 변수 영역을 표시할지, 아니면 숨길지 나타냅니다. 이 매개 변수를 **true**값으로 설정하면 도구 모음의 매개 변수 영역이 표시됩니다. 이 매개 변수의 기본값은 **true**입니다.|  
|**PrefixId**|**HTMLFragment**와 함께 사용할 경우 생성된 HTML 조각의 모든 **ID** 특성에 지정된 접두사가 추가됩니다.|  
|**ReplacementRoot(\*)**|ReportViewer 컨트롤 외부에 렌더링될 때 보고서의 모든 드릴스루, 토글 및 책갈피 링크에 추가할 문자열입니다. 예를 들어 이 문자열은 사용자가 클릭할 경우 사용자 지정 페이지로 리디렉션하는 데 사용됩니다.|  
|**ResourceStreamRoot(\*)**|모든 이미지 리소스(예: 토글 또는 정렬을 위한 이미지)에 대해 URL에 추가할 문자열입니다.|  
|**섹션**|렌더링할 보고서의 페이지 번호입니다. **0** 은 보고서의 모든 섹션이 렌더링됨을 나타냅니다. 기본값은 **1**입니다.|  
|**StreamRoot(\*)**|보고서 서버에서 반환된 HTML 보고서에서 IMG 요소의 **src** 특성 값 앞에 접두사를 추가하는 데 사용되는 경로입니다. 기본적으로 보고서 서버에서 경로가 제공됩니다. 이 설정을 사용하여 보고서의 이미지에 대한 루트 경로를 지정할 수 있습니다(예: **https://\<servername>/resources/companyimages**).|  
|**StyleStream**|스타일 및 스크립트가 문서에 만들어지지 않고 별도의 스트림으로 만들어지는지 여부를 나타냅니다. 기본 값은 **false**입니다.|  
|**도구 모음**|도구 모음을 표시할지, 아니면 숨길지 나타냅니다. 이 매개 변수의 기본값은 **true**입니다. 이 매개 변수 값이 **false**이면 문서 구조를 제외한 나머지 옵션이 모두 무시됩니다. 이 매개 변수를 생략하면 도구 모음이 지원하는 렌더링 형식에 맞게 자동으로 표시됩니다.<br /><br /> 보고서 뷰어 도구 모음은 URL 액세스를 사용하여 보고서를 렌더링할 때 렌더링됩니다. 도구 모음은 SOAP API를 통해 렌더링되지 않습니다. 하지만 **Toolbar** 장치 정보 설정은 SOAP **Render** 메서드 사용 시 보고서가 표시되는 방식에 영향을 줍니다. SOAP을 사용하여 HTML로 렌더링할 때 이 매개 변수 값이 **true** 이면 보고서의 첫 번째 섹션만 렌더링됩니다. 값이 **false**이면 전체 HTML 보고서가 단일 HTML 페이지로 렌더링됩니다.|  
|**UserAgent**|요청 중인 브라우저의 **user-agent** 문자열로, HTTP 요청에서 찾을 수 있습니다.|  
|**Zoom(\*)**|보고서 확대/축소 값으로서 정수 백분율 또는 문자열 상수입니다. 표준 문자열 값에는 **Page Width** 및 **Whole Page**가 포함됩니다. 이 매개 변수는 Internet Explorer 5.0 이전 버전의 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 및 모든[!INCLUDE[msCoName](../includes/msconame-md.md)] 이외의 브라우저에서 무시됩니다. 이 매개 변수의 기본값은 **100**입니다.|  
|**DataVisualizationFitSizing**|테이블릭스 안에 있을 경우 데이터 시각화 맞춤 동작을 나타냅니다. 여기에는 차트, 계기 및 지도가 포함됩니다.<br /><br /> 가능한 값은 **근사치** 및 **정확한 수치**입니다.<br /><br /> 기본값은 **근사치**입니다. **rsreportserver.config** 파일에서 설정이 제거될 경우 기본 동작은 **정확한 수치**입니다.<br /><br /> 정확한 크기를 결정하기 위한 처리는 더 오래 걸릴 수 있기 때문에 **정확한 수치** 를 설정하면 성능에 영향을 줄 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [장치 정보 설정을 렌더링 확장 프로그램에 전달](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [기술 참조&#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
