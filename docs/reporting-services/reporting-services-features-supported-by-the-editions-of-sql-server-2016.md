---
title: 다른 버전에서 지원되는 기능 - SQL Server Reporting Services | Microsoft Docs
description: 이 항목은 다른 SQL Server 버전에서 지원하는 SSRS(SQL Server Reporting Services) 기능을 설명합니다. SQL Server 평가 버전은 180일 동안 시험용으로 사용할 수 있습니다.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 12/16/2019
ms.openlocfilehash: 96fe1480deed7dad420687b5b3b08a3ea8da2ffd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76516604"
---
# <a name="sql-server-reporting-services-features-supported-by-editions"></a>버전별로 지원되는 SQL Server Reporting Services 기능

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

이 항목은 다른 SQL Server 버전에서 지원하는 SSRS(SQL Server Reporting Services) 기능을 설명합니다. SQL Server 평가 버전은 180일 동안 시험용으로 사용할 수 있습니다.  

## <a name="related-links"></a>관련 링크
  
 - [SQL Server Reporting Services(SSRS) 릴리스 정보](release-notes-reporting-services.md). 
 - [SQL Server Reporting Services(SSRS)의 새로운 기능](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).
 - [SQL Server 버전에서 지원하는 기능](~/sql-server/editions-and-components-of-sql-server-version-15.md)

##  <a name="sql-server-reporting-services"></a><a name="SSRS"></a> SQL Server Reporting Services  

Evaluation 및 Developer 버전에서 지원하는 기능은 다음 표의 SQL Server Enterprise Edition 열을 참조하세요.

|기능 이름|Enterprise|Standard|웹|Express with Advanced Services|Developer|  
|------|---------|---------------|-----------|-------|---------|  
| Power BI 보고서 및 Excel 통합 문서 | yes, Software Assurance | | | | yes |
|모바일 보고서 및 분석|yes||||yes|  
|지원되는 카탈로그 데이터베이스 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Standard 이상|Standard 이상|웹|Express|Standard 이상|  
|지원되는 데이터 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|웹|Express|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|  
|보고서 서버|yes|yes|yes|yes|yes|  
|보고서 디자이너|yes|yes|yes|yes|yes|  
|보고서 디자이너 웹 포털|yes|yes|yes|yes|yes|  
|역할 기반 보안|yes|yes|yes|yes|yes|  
|Excel, PowerPoint, Word, PDF 및 이미지로 내보내기|yes|yes|yes|yes|yes|  
|향상된 계기 및 차트|yes|yes|yes|yes|yes|  
|[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 대시보드에 보고서 항목 고정|yes|yes|yes|yes|yes|  
|사용자 지정 인증|yes|yes|yes||yes|  
|데이터 피드로 보고서 사용|yes|yes|yes|yes|yes|  
|모델 지원|yes|yes|yes||yes|  
|역할 기반 보안을 위해 사용자 지정 역할 만들기|yes|yes|||yes|  
|모델 항목 보안|yes|yes|||yes|  
|무한 클릭 광고|yes|yes|||yes|  
|공유 구성 요소 라이브러리|yes|yes|||yes|  
|전자 메일 및 파일 공유 구독/일정 예약|yes|yes|||yes|  
|보고서 기록, 스냅샷 실행 및 캐싱|yes|yes|||yes|  
|SharePoint 통합<sup>2</sup>|yes|yes|||yes|  
|원격 및 비 SQL 데이터 원본 지원<sup>1</sup>|yes|yes|||yes|  
|데이터 원본, 배달, 렌더링 및 RDCE 확장성|yes|yes|||yes|  
|사용자 지정 브랜딩|yes||||yes|  
|데이터 기반 보고서 구독|yes||||yes|  
|스케일 아웃 배포(웹 팜)|yes||||yes|  
|경고<sup>2</sup>(SSRS 2016) |yes||||yes|  
|파워 뷰<sup>2</sup>(SSRS 2016) |yes||||yes| 
|주석<sup>3</sup> |yes|yes|yes|yes|yes|  

 <sup>1</sup> SSRS(SQL Server Reporting Services)에서 지원하는 데이터 원본에 대한 자세한 내용은 [Reporting Services에서 지원하는 데이터 원본 &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)를 참조하세요.  
  
 <sup>2</sup> SharePoint 모드의 SQL Server 2016 Reporting Services가 필요합니다. 자세한 내용은 [SharePoint 모드에서 SQL Server Reporting Services 설치](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)를 참조하세요. SQL Server 2017부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다. 

<sup>3</sup> Power BI Report Server 및 SQL Server 2017 Reporting Services 이상만 해당합니다.

> [!NOTE]
> SQL Server Express with Tools 및 SQL Server Express는 SQL Server Reporting Services를 지원하지 않습니다.
  
## <a name="edition-requirements-for-the-report-server-database"></a>보고서 서버 데이터베이스의 버전 요구 사항
 보고서 서버 데이터베이스를 만들 때 일부 SQL Server [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전은 데이터베이스 호스팅에 사용할 수 없습니다. 다음 표에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 특정 버전에 사용할 수 있는 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]버전을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 버전의 경우|이 데이터베이스 엔진 인스턴스 버전을 사용하여 이 데이터베이스를 호스팅합니다.|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Enterprise 또는 Standard Edition(로컬 또는 원격)|  
|Standard|Enterprise 또는 Standard Edition(로컬 또는 원격)|  
|웹|Web Edition(로컬 전용)|  
|Express with Advanced Services|Express with Advanced Services(로컬 전용)|  
|평가|평가|  
  
##  <a name="business-intelligence-clients"></a><a name="BIC"></a> 비즈니스 인텔리전스 클라이언트  
Microsoft 다운로드 센터에서 다음 소프트웨어 클라이언트 애플리케이션을 사용할 수 있습니다. 다음 애플리케이션을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행되는 비즈니스 인텔리전스 문서를 만들 수 있습니다. 이러한 문서를 서버 환경에서 호스트하려는 경우 해당 문서 유형을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 사용하세요. 다음 표에서는 이러한 클라이언트 애플리케이션에서 만든 문서를 호스팅하는 데 필요한 서버 기능이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 보여 줍니다.  
  
|도구 이름|Enterprise|Standard|웹|Express with Advanced Services|Developer|  
|---------------|----------------|--------------|------------------------|-------------|---------------| 
| Power BI Report Server에 최적화된 Power BI Desktop, **.pbix** | yes, Software Assurance | | | | yes |
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], **.rdl** 및 **.rds**|yes|yes|yes|yes|yes|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)], **.rsmobile**|yes||||yes|  
|모바일 디바이스용 Power BI 앱(iOS, Windows 10, Android), **.rsmobile**|yes||||yes|  
  
> [!NOTE]  
> * 앞의 표는 해당 클라이언트 도구를 사용하도록 설정하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전이 나와 있습니다. 그러나 이 도구를 사용하여 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에서 호스팅되는 데이터에 액세스할 수 있습니다.  
> * [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 은 모바일 보고서를 만들기 위한 단일 지점입니다. SSRS 서버에 연결하여 데이터 원본에 액세스하고 보고서를 만듭니다. 그런 다음 조직의 다른 사용자가 서버 또는 모바일 디바이스에 액세스할 수 있도록 SSRS 서버에 게시합니다. 로컬 데이터 원본과 함께 독립적으로 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 를 사용할 수도 있습니다.  
> * 클라우드에서 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 온-프레미스, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 또는 두 가지 모두를 사용하든 보고서 배달 솔루션으로 둘 다를 사용하든 하나의 모바일 앱만 있으면 모바일 디바이스의 대시보드 및 모바일 보고서에 액세스할 수 있습니다. [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 앱은 Windows, iOS 또는 Android 앱 스토어에서 다운로드할 수 있습니다.  

## <a name="next-steps"></a>다음 단계

* [SQL Server 2017 버전에서 지원하는 기능](~/sql-server/editions-and-components-of-sql-server-2017.md)에 관해 읽어보세요. 

* [SQL Server 설치 계획](../sql-server/install/planning-a-sql-server-installation.md).

* 추가 질문이 있으신가요? [SQL Server Reporting Services 포럼](https://go.microsoft.com/fwlink/?LinkId=620231)에 문의하세요.
