---
title: 다양 한 Microsoft 환경에서 비즈니스 인텔리전스 기능 비교 | Microsoft Docs
ms.prod: sql-server-2014
ms.technology:
- reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 13ae9380cc3f034ace5f43d83640eea665cb3b02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267266"
---
# <a name="compare-business-intelligence-capabilities-in-different-microsoft-environments"></a>다양한 Microsoft 환경에서 비즈니스 인텔리전스 기능 비교

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence는 SharePoint Server 포함 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , SharePoint Online 및 Office 365용 Power BI 등을 망라한 다양한 환경에서 배포할 수 있습니다. 이 항목에서는 구성 요소 및 각 환경에서 지원되는 기능을 비교합니다.  
  
SharePoint Server 및 SharePoint Online 비교에 대한 자세한 내용은 [SharePoint 계획과 옵션 비교](http://products.office.com/SharePoint/compare-sharepoint-plans)(영문)를 참조하세요.  
  
## <a name="author-and-manage-bi-reports-and-dashboards"></a>BI 보고서 및 대시보드 작성 및 관리  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online 계획 2|Office 365용 Power BI|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|BI 사이트|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 갤러리|아니요|Power BI 사이트|  
|데이터 관리와 쿼리 공유 및 관리|아니요|아니요|예 **<sup>1</sup>**|  
|MDS(Master Data Services) 및 DQS(Data Quality Services)와의 통합|사용자 계정 컨트롤|아니오|아니요|  
|데이터 새로 고침 예약|예. 하지만 파워 쿼리 데이터가 들어 있는 통합 문서는 지원하지 않습니다.|아니요|사용자 계정 컨트롤|  
|자연어 쿼리 (Q & A)|아니요|아니요|예 **<sup>2</sup>**|  
|예측|아니요|아니요|예 **<sup>3</sup>**|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 통합|사용자 계정 컨트롤|아니오|아니요|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 통합(다차원 및 테이블 형식)|사용자 계정 컨트롤|아니오|아니요|  
|대화형 Power View 대시보드를 PowerPoint 프레젠테이션으로 내보내기|사용자 계정 컨트롤|아니오|아니요|  
|브라우저 내 대시보드 제작|사용자 계정 컨트롤|아니오|아니요|  
|사용 현황 모니터링|사용자 계정 컨트롤|아니요|사용자 계정 컨트롤|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 큐브의 행 기반 보안 활용|사용자 계정 컨트롤|아니오|아니요|  
  
 **<sup>1</sup>**[데이터 관리에서 데이터 관리자의 역할 이해](https://support.office.com/Article/Understanding-the-Role-of-Data-Stewards-in-Data-Management-ae3352f3-4389-45e8-a682-7fd6edb92524?ui=en-US&rs=en-US&ad=US) 고 [비디오: Power BI 정보 관리 및 데이터 관리](https://www.youtube.com/watch?v=8dHOj68ts7c)합니다.  
  
 **<sup>2</sup>**  [Power BI Q&A: Power BI 통합 문서 최적화 (클라우드 모델링)](https://powerbi.microsoft.com/nl-nl/blog/new-in-power-bi-cloud-modeling-for-q-and-a/)합니다.  
  
 **<sup>3</sup>**  [Office 365용 Power View에서 새로운 예측 기능 도입](https://blogs.msdn.com/b/powerbi/archive/2014/05/08/introducing-new-forecasting-capabilities-in-power-view-for-office-365.aspx)(영문).  
  
## <a name="view-and-browse-bi-data-reports-and-dashboards"></a>BI 데이터, 보고서 및 대시보드 보기 및 찾아보기  
  
||SQL Server 2014 & SharePoint Server 2013|SharePoint Online 계획 2|Office 365용 Power BI|  
|-|----------------------------------------------|------------------------------|-----------------------------|  
|브라우저에서 Microsoft Excel 통합 문서 보기|예(통합 문서 크기가 2GB 미만인 경우)|예(통합 문서 크기가 10MB 미만인 경우)|예(통합 문서 크기가 250MB 미만인 경우)|  
|HTML5에서 브라우저 내 데이터 탐색|아니요|아니요|사용자 계정 컨트롤|  
|보고서 및 대시보드에 원격으로 액세스하는 모바일 BI 앱|아니요|아니요|예 **<sup>1</sup>**|  
|데이터 소스로 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 를 사용하는 Excel 통합 문서 **<sup>2</sup>**|사용자 계정 컨트롤|아니오|아니요|  
|다른 브라우저 및 버전의 기능을 사용하는 기능|예(Power View가 아닌 시각화의 경우) **<sup>3</sup>**|예(크기 10MB 미만의 통합 문서 파일의 경우) **<sup>3</sup>**|예 **<sup>3</sup>**|  
  
 **<sup>1</sup>**  [Microsoft Power BI](http://apps.microsoft.com/windows/app/microsoft-power-bi/b7e7c94d-2ea3-4fa6-a277-9d19a1f697ba).  
  
 **<sup>2</sup>**  [데이터 원본으로 PowerPivot 통합 문서 사용](http://blogs.technet.com/b/excel_services__powerpivot_for_sharepoint_support_blog/archive/2013/02/15/powerpivot-workbook-as-a-data-source.aspx)  
  
 **<sup>3</sup>**  [BI(비즈니스 인텔리전스) 도구의 모바일 지원](https://msdn.microsoft.com/library/dn151146\(v=sql.110\).aspx) 및 [Reporting Services 및 Power View 브라우저 지원 계획(Reporting Services 2014)](https://msdn.microsoft.com/library/ms156511.aspx).  
  
## <a name="more-information"></a>자세한 정보  
  
- [Excel 및 Office 365의 BI 기능](https://support.office.com/article/BI-capabilities-in-Excel-and-Office-365-26c0548e-124c-4fd3-aab3-5f64568cb743)합니다.  
  
- 동의어 사용 요구 사항에 대 한 자세한 내용은 [최적화 Power BI q&a 동의어 및 관용구를 사용 하 여](https://blog.pragmaticworks.com/optimizing-power-bi-qa-with-synonyms-phrasing-using-cloud-modeling) pragmaticworks.com에서.  
  
- [Office Online, 기업 소셜 네트워크를 선택 합니다. Yammer 또는 뉴스 피드? ](https://support.office.com/article/Pick-your-enterprise-social-network-Yammer-or-Newsfeed-21954c85-4384-47d4-96c2-dfa1c9d56e66?ui=en-US&rs=en-US&ad=US).  
  
- [Office 365용 Power BI](https://www.microsoft.com/powerbi/default.aspx)(영문).  
  
- [Power BI 가격](https://www.microsoft.com/powerBI/pricing.aspx)(영문).  
  
- [분석 및 Microsoft 비즈니스 인텔리전스 (BI) 도구를 사용 하 여 보고](../reporting-services/choosing-microsoft-business-intelligence-bi-tools-for-analysis-and-reporting.md)  
  
## <a name="community-content"></a>커뮤니티 콘텐츠

[온-프레미스와 클라우드 Microsoft 셀프 서비스 BI 비교](http://businessintelligist.com/2014/02/07/microsoft-self-service-bi-on-premise-vs-could/)(영문).