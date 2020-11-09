---
title: SSMS(SQL Server Management Studio)
description: SSMS(SQL Server Management Studio)의 자세한 내용과 Analysis Services 솔루션을 관리하는 방법을 비롯하여 SMMS에서 수행할 수 있는 작업에 대해 알아봅니다.
ms.prod: sql
ms.technology: ssms
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: ''
f1_keywords:
- sql13.ssms.viewhelp.f1
helpviewer_keywords:
- SQL Server Management Studio
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.custom: seo-lt-2019
ms.date: 09/11/2019
ms.openlocfilehash: 396df64c5c5be5d7ea9c5fc67d7cb1ff0a7d990f
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243852"
---
# <a name="what-is-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)란?

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)](SSMS)는 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Azure SQL Database, Azure Synapse Analytics의 모든 구성 요소에 액세스하고 구성, 관리, 개발할 수 있습니다. SSMS는 기술 수준에 상관없이 모든 개발자와 데이터베이스 관리자가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 액세스할 수 있도록 수많은 서식 있는 스크립트 편집기와 광범위한 그래픽 도구 그룹을 결합하는 포괄적인 단일 유틸리티를 제공합니다.

- [**SSMS(SQL Server Management Studio) 다운로드**](download-sql-server-management-studio-ssms.md)
- [**SQL Server Developer 다운로드**](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)
- [**Visual Studio 다운로드**](https://www.visualstudio.com/downloads/)

![SQL Server Management Studio의 스크린샷](media/sql-server-management-studio-ssms/ssms.png)

## <a name="sql-server-management-studio-components"></a>SQL Server Management Studio 구성 요소  
  
|Description|구성 요소|  
|---------------|---------|  
|**개체 탐색기** 를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에서 모든 개체를 보고 관리합니다.|[개체 탐색기](../ssms/object/object-explorer.md)|  
|**템플릿 탐색기** 를 사용하여 쿼리 및 스크립트 개발 속도를 높이는 데 사용하는 상용구 텍스트 파일을 작성 및 관리하는 방법입니다.|[템플릿 탐색기](../ssms/template/template-explorer.md)|  
|사용되지 않는 **솔루션 탐색기** 를 사용하여 쿼리 및 스크립트와 같은 관리 항목을 관리하는 데 사용되는 프로젝트를 작성하는 방법입니다.|[솔루션 탐색기](../ssms/solution/solution-explorer.md)|  
|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에 포함된 비주얼 디자인 도구를 사용하는 방법입니다.|[Visual Database Tools](../ssms/visual-db-tools/visual-database-tools.md)|  
|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 언어 편집기를 사용하여 쿼리와 스크립트를 대화식으로 작성 및 디버깅하는 방법입니다.|[쿼리 및 텍스트 편집기](./f1-help/database-engine-query-editor-sql-server-management-studio.md?view=sql-server-ver15)

## <a name="sql-server-management-studio-for-business-intelligence"></a>비즈니스 인텔리전스용 SQL Server Management Studio

[!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 액세스, 구성 및 관리하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용합니다. 3가지 비즈니스 인텔리전스 기술 모두 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에 의존하지만 각 기술과 관련된 관리 태스크는 약간씩 다릅니다.

> [!NOTE]
> [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 솔루션은 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)]가 아닌 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 만들고 수정합니다. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)][!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]기반의 개발 환경입니다.

### <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Analysis Services 솔루션 관리

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 개체를 관리할 수 있습니다. 예를 들어 백업을 수행하고 개체를 처리할 수 있습니다.

[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] MDX(Multidimensional Expressions), DMX(Data Mining Extensions) 및 XMLA(XML for Analysis)로 작성된 스크립트를 개발 및 저장할 수 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트를 제공합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 인스턴스에서 관리 태스크를 수행하거나 데이터베이스 및 큐브와 같은 개체를 다시 만들 수 있습니다. 예를 들어 기존 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 인스턴스에 직접 새 개체를 만드는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트에서 XMLA 스크립트를 개발할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] 스크립트 프로젝트는 솔루션의 일부로 저장되어 원본 코드 제어와 함께 통합될 수 있습니다.
  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하는 방법에 대한 자세한 내용은 [SQL Server Management Studio를 사용한 개발 및 구현](/analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio)을 참조하세요.
  
### <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Integration Services 솔루션 관리

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리하고 실행 중인 패키지를 모니터링할 수 있습니다. 또한 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 를 사용하여 패키지를 폴더로 구성하고 패키지를 실행하고 패키지를 가져오거나 내보내고 DTS(데이터 변환 서비스) 패키지를 마이그레이션하고 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 업그레이드할 수 있습니다.

### <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 Reporting Services 프로젝트 관리

SQL Server Management Studio를 사용하여 Reporting Services 기능을 활성화하고 서버 및 데이터베이스를 관리하고 역할 및 작업을 관리할 수 있습니다.

공유 일정 폴더를 사용하여 공유 일정을 관리하고 보고서 서버 데이터베이스(ReportServer, ReportServerTempdb)를 관리할 수 있습니다. 또한 보고서 서버 데이터베이스를 새로운 또는 다른 SQL Server 데이터베이스 엔진([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)])으로 이동할 때 Master 시스템 데이터베이스에서 RSExecRole을 만듭니다. 이러한 문서에 관한 자세한 내용은 다음 항목을 참조하세요.  

- [SSMS의 Reporting Services](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)
- [보고서 서버 데이터베이스 관리](../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)
- [RSExecRole 만들기](../reporting-services/security/create-the-rsexecrole.md)

다양한 기능을 설정 및 구성하고 서버 기본값을 설정하고 역할 및 작업을 관리함으로써 서버를 관리할 수도 있습니다. 이러한 문서에 관한 자세한 내용은 다음 항목을 참조하세요.

- [보고서 서버 속성 설정](../reporting-services/tools/set-report-server-properties-management-studio.md)
- [역할 만들기, 삭제 또는 수정](../reporting-services/security/role-definitions-create-delete-or-modify.md)
- [Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)

## <a name="non-english-language-versions-of-sql-server-management-studio-ssms"></a>영어가 아닌 언어 버전의 SSMS(SQL Server Management Studio)

혼합 언어 설정의 블록이 해제되었습니다. 프랑스어 Windows에 SSMS 독일어를 설치할 수 있습니다. OS 언어가 SSMS 언어와 일치하지 않는 경우 사용자는 도구 > 옵션 > 국가별 설정에서 언어를 변경해야 합니다. 그렇지 않으면 SSMS는 영어 UI를 표시합니다.

이전 버전의 다른 로캘에 대한 자세한 내용은 [SSMS의 영어 이외의 언어 버전 설치](install-other-languages.md)를 참조하세요.

## <a name="support-policy-for-ssms"></a>SSMS에 대한 지원 정책

- SSMS 17.0부터는 SQL 도구 팀이 [Microsoft 최신 수명 주기 정책](https://support.microsoft.com/help/30881/modern-lifecycle-policy)을 채택했습니다.
- 원래 [최신 수명 주기 정책 알림](https://support.microsoft.com/help/447912/announcing-microsoft-modern-lifecycle-policy)을 읽어 보세요. 자세한 내용은 [최신 정책 FAQ](https://support.microsoft.com/help/30882/modern-lifecycle-policy-faq)를 참조하세요.
- 진단 데이터 수집 및 기능 사용에 대한 자세한 내용은 [SQL Server 개인 정보 보완](../sql-server/sql-server-privacy.md)을 참조하세요.

## <a name="cross-platform-tool"></a>플랫폼 간 도구

[!INCLUDE[ssms-azure-data-studio-mention](../includes/ssms-azure-data-studio-mention.md)]

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>다음 단계

- [비영어 SSMS 버전 설치](install-other-languages.md)
- [SQL Server 인스턴스에 연결 및 쿼리](./quickstarts/connect-query-sql-server.md)
- [Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]