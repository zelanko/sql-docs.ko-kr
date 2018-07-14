---
title: 예제 라이선스 토폴로지 및 SQL Server 2014 셀프 서비스 비즈니스 인텔리전스에 대 한 비용 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 682b8711-407a-48d1-9807-415d4c24dad6
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4672647d8e9caae94e3b64fc43c3b687aa010920
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185806"
---
# <a name="example-license-topologies-and-costs--for-sql-server-2014-self-service-business-intelligence"></a>SQL Server 2014 셀프 서비스 비즈니스 인텔리전스에 대한 예제 라이선스 토폴로지 및 비용
  이 항목에서는 선택에 대 한 고급 고려 사항 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Business Intelligence 버전 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition. 이 항목에는 몇 가지 샘플 온-프레미스 Microsoft 셀프 서비스 BI(Business Intelligence) 토폴로지가 포함되어 있습니다. 그 예에는 비용과 성능 간에 균형을 최적화하는 데 사용할 수 있는 버전과 라이선스가 포함됩니다. 토폴로지, 서버 수 및 라이선스 비용은 **예제로만**제공됩니다. Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 Microsoft SharePoint 2013은 라이선스 방식에 몇 가지 변경을 도입하여 서버, 사용자 및 장치를 라이선스 하는 방식에 더 많은 옵션을 제공합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 라이선스는 동일한 Business Intelligence 관련 시나리오를 지원합니다.  
  
-   
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]는 Business Intelligence 버전에서 사용 가능하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에 대한 코어 라이선스로 제공됩니다.  
  
-   SharePoint 2013은 엑스트라넷 및 인터넷 시나리오를 비롯하여 SharePoint Online 옵션에 대한 SharePoint Server 라이선스를 간소화했습니다.  
  
 구입 전에 각 제품에 대한 "구입 방법" 섹션을 방문하여 특정 라이선스 요구 사항에 대해 Microsoft 담당자 또는 지역 대리점에 문의하세요. 최신 라이선스 계획 및 비용에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [라이선스 정보 – SQL Server 2014](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx)  
  
-   [SharePoint 2013 라이선스](http://office.microsoft.com/sharepoint/sharepoint-licensing-overview-collaboration-software-FX103789438.aspx).  
  
 **항목 내용**  
  
-   [SQL Server Business Intelligence 구성 요소](#bkmk_bi_components)  
  
-   [SQL Server 2014 라이선스 요약](#bkmk_sql_server_license)  
  
-   [SharePoint 2013 라이선스 요약](#bkmk_sharepoint_license)  
  
-   [별도 PowerPivot 서버가 있는 3 계층 토폴로지](#bkmk_3tier_powerpivot)  
  
-   [3 계층 토폴로지](#bkmk_3tier)  
  
-   [2 계층 토폴로지](#bkmk_2tier)  
  
-   [참조 및 커뮤니티 콘텐츠](#bkmk_reference)  
  
##  <a name="bkmk_bi_components"></a> SQL Server Business Intelligence 구성 요소  
 이 항목은 SQL Server 및 SharePoint 서버 기술을 집중적으로 조명합니다. 관련 비용 및 예제는 전체 클라이언트 및 서버 솔루션이 필요한 Microsoft Windows Server 또는 Microsoft Office 구성 요소를 구체적으로 설명하지 않습니다. 이 항목에서 설명하는 SQL Server Business Intelligence 구성 요소는 SharePoint 모드 및 SharePoint용 PowerPivot에서 실행 중인 SQL Server Reporting Services입니다. 구성 요소에는 다음 기능이 포함됩니다.  
  
-   브라우저의 대화형 PowerPivot 통합 문서.  
  
-   대화형 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] SharePoint의 보고서입니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리, 데이터 새로 고침 예약, 관리 대시보드.  
  
-   데이터 경고를 비롯하여 SharePoint 모드의 Reporting Services.  
  
 자세한 내용은의 기능 테이블을 참조 하세요 [SharePoint 사용 하 여 SQL Server BI 기능 설치 &#40;PowerPivot 및 Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)합니다.  
  
## <a name="license-summary"></a>라이선스 요약  
 이 단원에서는 SQL Server 및 SharePoint에 대한 라이선스 요구 사항을 요약합니다. 이 정보는 대략적인 요약이므로 이 문서에서는 토폴로지 다이어그램과 비용 예제에서 사용된 시나리오만 다룹니다. 자세한 라이선스 세부 정보는 제시된 콘텐츠 링크를 검토하세요. 예제 가격은 MOLP(Microsoft Open License Program) 가격을 기준으로 합니다.  
  
 일반적인 사용법은 SQL Server Database Engine을 실행 중인 서버에서 **엔터프라이즈 버전** 을 사용하고 Reporting Services 또는 SharePoint용 PowerPivot을 실행 중인 서버에서 **Business Intelligence 버전** 을 사용하는 것입니다. 하지만 구현의 **사용자 수** 및 **서버 코어 수** 는 비용과 함께 어떤 버전을 사용할지에 대한 의사 결정에 영향을 미칩니다.  
  
###  <a name="bkmk_sql_server_license"></a> SQL Server 2014 라이선스 요약  
  
-   SQL Server 엔터프라이즈 버전은 코어 기반 라이선스를 사용합니다. 코어 기반 라이선스는 **2-core** 팩으로 판매됩니다.  
  
-   SQL Server BI 버전은 서버 라이선스와 CAL(클라이언트 액세스 라이선스)을 모두 사용합니다.  
  
-   CAL 라이선스는 연결된 서버 수에 관계없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결된 각 사용자 또는 장치를 기반으로 합니다.  
  
-   코어 라이선스에는 서버에서 라이선스에 의해 제공되는 모든 코어가 필요합니다. 서버에서 각 물리적 프로세스에는 최소 **4개** 의 코어 라이선스가 필요합니다.  
  
 다음 표에서는 배포 설계 및 라이선스 비용 예측에 사용되는 라이선스 세부 정보를 요약합니다. **참고:**  표시된 가격은 데모용입니다.  
  
|SQL Server 버전|SQL Server 라이선스 + CAL(클라이언트 액세스 라이선스)|SQL Server 코어 기반 라이선스|  
|-------------------------|---------------------------------------------------------|-----------------------------------|  
|Enterprise|해당 사항 없음|**(예)** $6874 X [코어 #개] X [코어 요소]|  
|Business Intelligence|**(예)** $8592 + CAL당 $199|해당 사항 없음|  
|표준|**(아니요)**|**(아니요)**|  
  
 샘플에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 라이선스 가격을 참조 하십시오.  
  
-   [가상 환경에 대 한 라이선싱](http://www.microsoft.com/licensing/about-licensing/virtualization.aspx) (http://www.microsoft.com/licensing/about-licensing/virtualization.aspx)합니다.  
  
-   [SQL Server 2014 라이선스 데이터 시트-Microsoft 홈 페이지](http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf)합니다.  
  
-   [SQL server 2014 버전 및 라이선스](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx#tab=2)  
  
1.  **SQL Server 가정 및 자세한 라이선스 정보:**  
  
2.  이 항목의 다이어그램은 데이터베이스 서버에 SQL Server의 엔터프라이즈 버전을 사용하여 AlwaysOn Availability Groups 등과 같은 고가용성 기능 전체를 지원합니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
3.  이 예의 서버는 2개의 Intel Xeon 6-코어 프로세스이며, 따라서 라이선스 비용 계산 시 **1** 개의 **SQL Server 코어 요소** 가 있습니다. 코어 요소 및 라이선스 비용에 대 한 자세한 내용은 참조 하세요. [SQL Server 코어 요소 표](http://download.microsoft.com/download/9/B/F/9BF63163-D8F9-4339-90AA-EBC9AAFC49AD/SQL2012_CoreFactorTable_Mar2012.pdf) (http://download.microsoft.com/download/0/C/8/0C85665B-11EA-4FF5-B37C-8CC21CF95AC4/BizTalk%202013_CoreFactorTable_**3.19.2013**. v4.pdf).  
  
###  <a name="bkmk_sharepoint_license"></a> SharePoint 2013 라이선스 요약  
 다음 목록에서는 배포 설계 및 라이선스 비용 예측에 사용되는 라이선스 모델 정보를 요약합니다. 표시된 가격은 데모용입니다.  
  
1.  SharePoint 서버 라이선스는 Microsoft SharePoint Server의 각 인스턴스에 필요합니다.  
  
2.  최종 사용자 또는 최종 장치별로 SharePoint Enterprise 라이선스를 받으려면 Microsoft SharePoint Server 2013 **표준 CAL 라이선스** 와 함께 Microsoft SharePoint Server 2013 **엔터프라이즈 CAL 라이선스**를 구입하세요.  
  
3.  SharePoint CAL 라이선스는 SharePoint 서버에 액세스하는 사용자 또는 장치별로 하나씩 구입합니다. CAL 라이선스는 서버별로 구입하지 않아도 됩니다.  
  
 예를 들어 100명의 사용자가 사용하는 2개의 인스턴스로 구성된 환경의 경우 견적 비용은 다음과 같습니다.  
  
-   Microsoft SharePoint Server 2013 표준 CAL 라이선스: **$107.99**  
  
-   Microsoft SharePoint Server 2013 엔터프라이즈 CAL 라이선스: **$94.99**  
  
-   Microsoft SharePoint Server 2013 라이선스: **$6,412.99**  
  
 비용은 **$33,123.98**이 됩니다.  
  
-   CAL 라이선스: ($107.99 +$94.99) X 100) =$20,298.00  
  
-   서버 라이선스: ($6,412.99 X 2) =$12,825.98  
  
 **SharePoint 가정 및 자세한 라이선스 정보:**  
  
 샘플 배포는 모두 인트라넷 환경이므로 SharePoint CAL 라이선스가 필요합니다.  
  
-   [SharePoint 라이선스 전체 목록](http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise) (http://technet.microsoft.com/en-in/library/jj819267.aspx#bkmk_FeaturesOnPremise)합니다.  
  
-   [SharePoint를 구입 하는 방법](http://sharepoint.microsoft.com/en-in/Pages/buy.aspx) (http://sharepoint.microsoft.com/en-in/Pages/buy.aspx)합니다.  
  
##  <a name="bkmk_3tier_powerpivot"></a> 3 계층 토폴로지 별도의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버  
 이 예제는 800명 이하의 사용자로 구성된 경우 SharePoint 응용 프로그램 서버 및 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에서 SQL Server BI 버전을 사용하는 것이 가장 저렴하다고 설명합니다. 하지만 사용자가 800명 이상인 경우에는 SQL Server 엔터프라이즈 버전이 보다 저렴합니다. 코어 라이선스는 사용자 수와 별개이므로 코어 및 CAL 라이선스 비용과 사용자 수 증가를 비교하는 경우 비용 임계값 지점이 발생합니다. 엔터프라이즈 버전 이상의 임계값 지점부터는 가장 저렴한 솔루션입니다. 비용 임계값을 결정하려면 라이선스를 부여할 코어 수와 라이선스를 부여할 최종 사용자 또는 최종 장치 CAL 수를 기반으로 비용을 비교합니다.  
  
-   이 예제는 인트라넷 배포이므로 SharePoint 2013에 SharePoint CAL 라이선스가 적용됩니다.  
  
-   응용 프로그램 역할(2)에는 SharePoint 모드에 설치된 SQL Server Reporting Services가 포함됩니다.  
  
     SharePoint 서비스 응용 프로그램 데이터베이스는 데이터베이스 역할(4) 서버에서 실행됩니다.  
  
-   SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]은 별도의 서버(3)에서 실행됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 2013 용 SharePoint 팜 외부의 실행 및 성능 향상 SharePoint 설치가 포함 되지 않은 서버에 설치할 수 있습니다.  
  
-   데이터베이스 역할(4)에서는 SQL Server 엔터프라이즈 버전을 사용하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]기능, AlwaysOn Availability Groups를 사용할 수 있습니다.  
  
 ![bi_license_3tiers_and_ASseparate](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseparate.gif "bi_license_3tiers_and_ASseparate")  
  
 사용자가 100명일 경우 SQL Server BI 버전이 보다 저렴합니다.  
  
 ![bi_license_3tiers_and_ASseperate_calcs](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs.gif "bi_license_3tiers_and_ASseperate_calcs")  
  
 하지만 사용자가 300명인 경우에는 SQL Server 엔터프라이즈 버전을 사용하는 것이 보다 저렴합니다.  
  
 ![bi_license_3tiers_and_ASseperate_calcs2](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs2.gif "bi_license_3tiers_and_ASseperate_calcs2")  
  
##  <a name="bkmk_3tier"></a> 3 계층 토폴로지  
 이 예제에서는 100명 이하의 사용자가 있는 경우 SQL Server BI 기능을 실행하는 서버에서 SQL Server BI 버전을 사용하는 것이 보다 저렴한 것으로 설명합니다. 하지만 사용자가 500명 이상인 경우에는 SQL Server 엔터프라이즈 버전이 보다 저렴합니다.  
  
-   이 예제는 인트라넷 배포이므로 SharePoint 2013에 SharePoint CAL 라이선스가 적용됩니다.  
  
-   팜 외부의 (2) 실행 PowerPivot 모드의 analysis Services 하지만 PowerPivot 중인지 **동일한 물리적** 다른 응용 프로그램 역할의 서버.  
  
-   데이터베이스 역할 (3) SQL Server Enterprise에서는 있도록는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능, AlwaysOn Availability Groups를 사용할 수 있습니다.  
  
 ![bi_license_3tiers](../../../2014/sql-server/install/media/bi-license-3tiers.gif "bi_license_3tiers")  
  
 사용자가 100명일 경우 SQL Server BI 버전이 보다 저렴합니다.  
  
 ![bi_license_3tiers_calcs1](../../../2014/sql-server/install/media/bi-license-3tiers-calcs1.gif "bi_license_3tiers_calcs1")  
  
 하지만 사용자가 500명인 경우에는 SQL Server 엔터프라이즈 버전이 보다 저렴합니다.  
  
 ![bi_license_3tiers_calcs3](../../../2014/sql-server/install/media/bi-license-3tiers-calcs3.gif "bi_license_3tiers_calcs3")  
  
##  <a name="bkmk_2tier"></a> 2 계층 토폴로지  
 2계층만 있는 SQL Server Enterprise Edition을 사용하면 SQL Server Database Engine에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능, AlwaysOn Availability Groups를 사용할 수 있습니다. 따라서 SQL Server 버전 간에 비교할 비용 차이가 없습니다. 유일한 변수는 사용자 수를 기반으로 하는 SharePoint CAL 가격입니다.  
  
-   이 예제는 인트라넷 배포이므로 SharePoint 2013에 SharePoint CAL 라이선스가 적용됩니다.  
  
-   PowerPivot 모드의 Analysis Services는 팜 외부에서 실행되지만 PowerPivot은 SQL server Database Engine 역할을 수행하는 동일한 물리적 서버(2)에서 실행됩니다.  
  
 ![bi_license_2tiers](../../../2014/sql-server/install/media/bi-license-2tiers.gif "bi_license_2tiers")  
  
 ![bi_license_2tiers_calcs1](../../../2014/sql-server/install/media/bi-license-2tiers-calcs1.gif "bi_license_2tiers_calcs1")  
  
##  <a name="bkmk_reference"></a> 참조 및 커뮤니티 콘텐츠  
  
### <a name="license-tools"></a>라이선스 도구  
  
-   [Microsoft 라이선스 관리자](http://mla.microsoft.com/default.aspx) (http://mla.microsoft.com/default.aspx)합니다.  
  
-   [클라이언트 액세스 라이선스 (CAL) 결정 도구](http://www.microsoft.com/licensing/CalTool/) (http://www.microsoft.com/licensing/CalTool/)합니다.  
  
-   [Microsoft Business Hub: 구입 방법](http://www.microsoftbusinesshub.com/How_To_Buy#) (http://www.microsoftbusinesshub.com/How_To_Buy#)합니다.  
  
### <a name="microsoft-license-information"></a>Microsoft 라이선스 정보  
  
-   [에 대 한 라이선스: 클라이언트 액세스 라이선스 및 라이선스 관리](http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx) (http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx)합니다.  
  
-   [에 대 한 라이선스: 제품 라이선스 검색](http://www.microsoftvolumelicensing.com/default.aspx) (http://www.microsoftvolumelicensing.com/default.aspx)합니다.  
  
-   [볼륨 라이선스: 가격 및 구입 방법](http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx) (http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx)합니다.  
  
### <a name="community-content"></a>커뮤니티 콘텐츠  
  
-   [SQL Server 2014 개발자 버전 라이선스](http://sqlmag.com/sql-server-2014/sql-server-2014-developer-edition-licensing).  
  
-   [SQL Server 2014 라이선스 변경](http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)(http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)합니다.  
  
-   [SQL Server 2014 라이선스 변경](https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)(https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)합니다.  
  
-   [SharePoint 2013 라이선스 비용 예측](http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/) (http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/)합니다.  
  
-   [Microsoft 볼륨 라이선스 고객 커뮤니티](http://www.microsoft.com/licensing/existing-customers/community.aspx) (http://www.microsoft.com/licensing/existing-customers/community.aspx)합니다.  
  
  
