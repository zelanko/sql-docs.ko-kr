---
title: SQL Server 2016 버전에서 지원하는 Reporting Services 기능 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 39f03d2d-6e48-4b34-a9d3-07f86313b937
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1a1b85b3e6e7bb782c9e384eabc25ed986a7138
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280102"
---
# <a name="reporting-services-features-supported-by-the-editions-of-sql-server-2016"></a>SQL Server 2016 버전에서 지원하는 Reporting Services 기능

이 항목은 다른 SQL Server 2016 버전에서 지원되는 기능의 세부 정보를 제공합니다.  
  
 SQL Server 평가 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
  
 최신 릴리스 정보는 [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md)를 참조하세요. 새로운 기능에 대한 최신 정보는 [Reporting Services(SSRS)의 새로운 기능](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)을 참조하세요.
    
 **SQL Server 2016을 사용해 보세요.**    
    
 > [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[평가 센터에서 SQL Server 2016 다운로드](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 가상 머신 소형](../analysis-services/media/azure-virtual-machine-small.png)**[이미 설치된 SQL Server 2016으로 가상 머신을 스핀업](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

Evaluation 및 Developer 버전에서 지원하는 기능은 SQL Server Enterprise Edition을 참조하세요.

SQL Server 기술에 대한 표로 이동하려면 해당 링크를 클릭합니다.  

-   [Reporting  Services](#SSRS)  
  
-   [Business Intelligence 클라이언트](#BIC)  

##  <a name="SSRS"></a> Reporting  Services  
  
|기능 이름|Enterprise|표준|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|모바일 보고서 및 KPI|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|지원되는 카탈로그 DB [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Standard 이상|Standard 이상|Web|Express|||Standard 이상|  
|지원되는 데이터 원본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Web|Express|||모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|  
|보고서 서버|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|보고서 디자이너|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|보고서 디자이너 웹 포털|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|역할 기반 보안|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|Excel, PowerPoint, Word, PDF 및 이미지로 내보내기|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|향상된 계기 및 차트|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]대시보드에 보고서 항목 고정|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|사용자 지정 인증|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|데이터 피드로 보고서 사용|사용자 계정 컨트롤|예|예|예|||사용자 계정 컨트롤|  
|모델 지원|사용자 계정 컨트롤|예|예||||사용자 계정 컨트롤|  
|역할 기반 보안을 위해 사용자 지정 역할 만들기|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|모델 항목 보안|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|무한 클릭 광고|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|공유 구성 요소 라이브러리|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|전자 메일 및 파일 공유 구독/일정 예약|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|보고서 기록, 스냅숏 실행 및 캐싱|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|SharePoint 통합|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|원격 및 비 SQL 데이터 원본 지원<sup>1</sup>|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|데이터 원본, 배달 및 렌더링, RDCE 확장성|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|사용자 지정 브랜딩|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|데이터 기반 보고서 구독|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|확장 배포(웹 팜)|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|경고<sup>2</sup>|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
  
 <sup>1</sup> SQL Server 2016 Reporting Services(SSRS)에서 지원하는 데이터 원본에 대한 자세한 내용은 [Reporting Services에서 지원하는 데이터 원본 &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)를 참조하세요.  
  
 <sup>2</sup> SharePoint 모드의 Reporting Services가 필요합니다. 자세한 내용은 [Reporting Services SharePoint 모드 설치](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)를 참조하세요.  
  
## <a name="report-server-database-server-edition-requirements"></a>보고서 서버 데이터베이스 서버 버전 요구 사항  
 보고서 서버 데이터베이스를 만들 때 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전은 데이터베이스 호스팅에 사용할 수 없습니다. 다음 표에서는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 특정 버전에 사용할 수 있는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]버전을 보여 줍니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services 버전|데이터베이스 호스팅에 사용할 데이터베이스 엔진 인스턴스 버전|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Standard 또는 Enterprise Edition(로컬 또는 원격)|  
|표준|Standard 또는 Enterprise Edition(로컬 또는 원격)|  
|Web|Web Edition(로컬 전용)|  
|Express with Advanced Services|Express with Advanced Services(로컬 전용)|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Business Intelligence 클라이언트  
 Microsoft 다운로드 센터에서 제공하는 다음 소프트웨어 클라이언트 응용 프로그램을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 실행되는 비즈니스 인텔리전스 문서를 손쉽게 만들 수 있습니다. 이러한 문서를 서버 환경에서 호스트하려는 경우 해당 문서 유형을 지원하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 사용하세요. 다음 표에서는 이러한 클라이언트 응용 프로그램에서 만든 문서를 호스팅하는 데 필요한 서버 기능이 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 보여 줍니다.  
  
|도구 이름|Enterprise|표준|Web|Express with Advanced Services|Express with Tools|Express|개발자|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] (.rdl 및.rds)|사용자 계정 컨트롤|예|||||사용자 계정 컨트롤|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] (.rsmobile)|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
|모바일 장치용 Power BI 앱(iOS, Windows 10, Android)(.rsmobile)|사용자 계정 컨트롤||||||사용자 계정 컨트롤|  
  
> [!NOTE]  
> 1.  위의 표는 이러한 클라이언트 도구를 활성화하는 데 필요한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전을 식별하지만 이러한 도구는 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서 호스트되는 데이터에 액세스할 수 있습니다.  
> 2.  [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 은 모바일 보고서를 만들기 위한 단일 지점입니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서버에 연결하여 데이터 원본에 액세스하고 보고서를 만듭니다. 그런 다음 조직의 다른 사용자가 서버 또는 모바일 장치에 액세스할 수 있도록 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서버에 게시합니다. 로컬 데이터 원본과 함께 독립적으로 [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)] 를 사용할 수도 있습니다.  
> 3.  클라우드에서  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 온-프레미스 또는 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 를 사용하든 보고서 배달 솔루션으로 둘 다를 사용하든 하나의 모바일 앱만 있으면 모바일 장치의 대시보드 및 모바일 보고서에 액세스할 수 있습니다. [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 앱은 Windows, iOS 또는 Android 앱 스토어에서 다운로드할 수 있습니다.  

## <a name="next-steps"></a>다음 단계

[SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[SQL Server 2016 제품 사양](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
[SQL Server 2016 설치](../database-engine/install-windows/installation-for-sql-server-2016.md) 

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
