---
title: "URL 액세스 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services]
- links [Reporting Services], URL access
- URL access [Reporting Services], about URL access
- parameters [Reporting Services], URL access
- report servers [Reporting Services], URL access
- hyperlinks [Reporting Services]
ms.assetid: 52c3f2a3-3d6d-4fee-9c46-83f366919398
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f91b97d1877e365813f3aa2445fabea1a263ab2b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="url-access-ssrs"></a>URL 액세스(SSRS)
  SQL Server Reporting Services(SSRS)에서 보고서 서버의 URL 액세스를 사용하면 URL 요청을 통해 보고서 서버에 명령을 보낼 수 있습니다. 예를 들어 기본 모드 보고서 서버 또는 SharePoint 라이브러리에서 보고서 렌더링을 사용자 지정할 수 있습니다. 특정 보고서 매개 변수 값 집합을 사용하여 보고서를 보거나 보고서의 관심 있는 특정 페이지를 본 경우 미리 정의된 URL 액세스 매개 변수를 사용하여 이 정보를 URL에 캡슐화할 수 있습니다. 또한 렌더링 형식 및 보고서 뷰어의 디자인에 대한 매개 변수를 포함하여 보고서 서버에서 보고서를 처리하는 방식을 사용자 지정할 수 있습니다. 그런 다음 이 URL을 전자 메일이나 웹 페이지에 직접 붙여넣어 다른 사용자가 브라우저에서 같은 방식으로 보고서에 액세스하도록 할 수 있습니다.  
  
 URL 액세스를 통해 수행할 수 있는 다음 동작의 예를 들면 다음과 같습니다.  
  
-   HTML 뷰어에 명령(예: 디자인 조정) 보내기  
  
-   카탈로그 폴더의 자식 나열  
  
-   카탈로그 항목의 XML 정의 검색  
  
-   특정 보고서 기록 스냅숏 렌더링  
  
-   보고서 세션 관리  
  
 URL 액세스를 통해 사용할 수 있는 설정 및 명령의 전체 목록은 [URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)를 참조하세요.  
  
## <a name="url-access-concepts"></a>URL 액세스 개념  
 보고서 서버에 대한 URL 요청에는 보고서 서버에서 처리하는 매개 변수가 포함됩니다. 보고서 서버에서 URL 요청을 처리하는 방법은 매개 변수, 매개 변수 접두사, URL에 포함된 항목의 종류 등에 따라 다릅니다. 보고서 서버 URL은 W3C(World Wide Web 컨소시엄)와 IETF의 공동 초안 표준에서 제안한 대로 URL 형식 지정 지침을 따릅니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] URL 기능은 표준 URL 주소 지정을 지원하는 대부분의 인터넷 브라우저나 응용 프로그램에서 호환됩니다.  
  
### <a name="url-access-syntax"></a>URL 액세스 구문  
 URL 요청에는 임의의 순서로 나열된 여러 매개 변수가 포함될 수 있습니다. 매개 변수는 앰퍼샌드(&)로 구분되고 이름/값 쌍은 등호(=)로 구분됩니다.  
  
```  
  
rswebserviceurl  
?  
reportpath  
      [&prefix:param=value]...n]  
  
```  
  
### <a name="syntax-description"></a>구문 설명  
 *rswebserviceurl*  
 보고서 서버의 웹 서비스 URL입니다. 기본 모드의 경우 Reporting Services 구성 관리자에 구성된 보고서 서버 인스턴스의 웹 서비스 URL입니다([보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md) 참조). 예를 들어  
  
```  
http://myrshost/reportserver  
https://machine.adventure-works.com/reportserver_MYNAMEDINSTANCE  
```  
  
 SharePoint 통합 모드의 경우 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 와 통합된 SharePoint 사이트의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]프록시 URL입니다. 예를 들어  
  
```  
http://myspsite/subsite/_vti_bin/reportserver  
```  
  
> [!TIP]  
>  URL에는 SharePoint를 통해 요청을 라우팅하는 `_vti_bin` 프록시 구문과 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP 프록시를 포함하는 것이 중요합니다. 프록시는 몇 가지 컨텍스트를 HTTP 요청에 추가하며 이 컨텍스트는 SharePoint 모드 보고서 서버에 대한 보고서의 올바른 실행을 보장하는 데 필요합니다.  
  
 *pathinfo*  
 기본 모드 보고서 서버 데이터베이스 항목의 상대 경로 이름 또는 SharePoint 카탈로그 항목의 정규화된 URL입니다.  
  
 카탈로그 항목의 경로입니다. 기본 모드의 경우 보고서 서버 데이터베이스 항목의 상대 경로(슬래시(**/**로 시작)입니다. 예를 들어  
  
```  
/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2  
```  
  
 SharePoint 통합 모드의 경우 SharePoint 라이브러리 항목의 정규화된 URL(항목 확장명 포함)입니다. 예를 들어  
  
```  
http://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl  
```  
  
 **&**  
 URL 액세스 매개 변수의 이름/값 쌍을 구분하는 데 사용됩니다.  
  
 **prefix**  
 (선택 사항) 보고서 서버 내에서 실행 중인 특정 프로세스에 액세스하는 URL 액세스 매개 변수의 접두사(예: `rs:` 또는 `rc:`)입니다.  
  
> [!NOTE]  
>  URL 액세스 매개 변수의 접두사가 포함되지 않은 경우 매개 변수는 보고서 서버에서 보고서 매개 변수로 처리됩니다. 보고서 매개 변수는 매개 변수 접두사를 사용하지 않으며 대/소문자를 구분합니다.  
  
 **param**  
 매개 변수 이름입니다.  
  
 *value*  
 사용 중인 매개 변수의 값에 해당하는 URL 텍스트입니다.  
  
 **참고:** 사용 가능한 URL 액세스 매개 변수의 목록은 [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md)을(를) 참조하십시오. URL에 보고서 매개 변수를 전달하는 예제는 [Pass a Report Parameter Within a URL](../reporting-services/pass-a-report-parameter-within-a-url.md)을 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|링크|  
|-----------------------|-----------|  
|보고서, 공유 데이터 원본 및 리소스와 같은 보고서 서버 항목 액세스|[URL 액세스를 사용 하 여 보고서 서버 항목 액세스](../reporting-services/access-report-server-items-using-url-access.md)|  
|보고서 매개 변수를 보고서로 전달|[URL에 보고서 매개 변수 전달](../reporting-services/pass-a-report-parameter-within-a-url.md)|  
|URL 액세스 문자열에서 날짜, 통화 등의 로캘별 해석을 정의하는 보고서 매개 변수의 로캘 설정|[URL에 보고서 매개 변수 언어 설정](../reporting-services/set-the-language-for-report-parameters-in-a-url.md)|  
|보고서 렌더링 방식을 사용자 지정하는 렌더링 확장자별 설정 보내기|[URL에 장치 정보 설정 지정](../reporting-services/specify-device-information-settings-in-a-url.md)|  
|보고서를 브라우저에서 보지 않고 파일 형식으로 직접 내보내기|[URL 액세스를 사용 하 여 보고서 내보내기](../reporting-services/export-a-report-using-url-access.md)|  
|보고서를 열고 문자열 위치로 직접 이동|[URL 액세스를 사용 하 여 보고서 검색](../reporting-services/search-a-report-using-url-access.md)|  
|특정 보고서 기록 스냅숏 렌더링|[URL 액세스를 사용 하 여 보고서 기록 스냅숏 렌더링](../reporting-services/render-a-report-history-snapshot-using-url-access.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [URL에 보고서 매개 변수 전달](../reporting-services/pass-a-report-parameter-within-a-url.md)   
 [URL 액세스 매개 변수 참조](../reporting-services/url-access-parameter-reference.md)   
 [URL 액세스를 사용 하 여 Reporting Services 통합](../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [찾기, 보기 및 관리 보고서 &#40; 보고서 작성기 및 SSRS &#41;](../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
