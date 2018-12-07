---
title: Reporting Services 도구 | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b227ef4d93c5629305c711e46b4278428986ce0b
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712474"
---
# <a name="reporting-services-tools"></a>Reporting Services 도구
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 관리 환경에서 다양한 보고서의 개발 및 사용을 지원하는 그래픽 및 스크립팅 도구 집합이 포함되어 있습니다. 이 도구 집합에는 개발 도구, 구성 및 관리 도구, 보고서 보기 도구가 포함되어 있습니다. 이 항목은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 개별 툴 및 툴 액세스 방법에 대한 간략한 개요를 제공합니다.  
  
 도구를 바로 찾으려면 [자습서: Reporting Services 도구 찾기 및 시작 방법&#40;SSRS&#41;](../../reporting-services/tools/tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md)를 참조하세요.  
  
## <a name="tools-for-report-authoring"></a>보고서 작성 도구  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서 작성에 사용할 수 있는 도구를 보여 줍니다.  
  
|도구|설명|액세스 방법|  
|----------|-----------------|-------------------|  
|[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]|[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]을(를) 사용하면 화면 또는 브라우저 창에 맞도록 콘텐츠를 동적으로 조정하고 어떤 화면 크기에나 적합하도록 효율적으로 확장하는 모바일 보고서를 만들 수 있습니다.<br /><br /> 조정 가능한 표 행/열이 표시된 디자인 화면에서 유동적인 모바일 보고서 요소를 사용하여 모바일 보고서를 만듭니다.<br /><br /> 자세한 내용은 [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)를 참조하세요.|[SQL Server 모바일 보고서 게시자](https://go.microsoft.com/fwlink/?LinkId=733527)다운로드|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 모델을 기반으로 보고서를 만들고 보고서와 상호 작용할 수 있도록 디자인한 대화형 데이터 탐색 및 시각 표현 환경입니다.|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Silverlight 브라우저를 사용합니다.|  
|보고서 디자이너|이 도구를 사용하여 보고서를 디자인합니다. 다음과 같은 기능이 포함되어 있습니다.<br /><br /> 기본 모드 또는 SharePoint 모드 보고서 서버에 배포합니다.<br /><br /> 다음에서 호스트됨 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> 보고서에 사용되는 데이터를 구성하는 보고서 데이터 창<br /><br /> 대화형으로 보고서를 디자인할 수 있는 디자인 및 미리 보기 탭 뷰<br /><br /> 데이터 원본에서 검색할 데이터 및 [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)의 데이터 원본 유형과 연결되는 데이터를 지정하는 데 유용한 쿼리 디자이너<br /><br /> IntelliSense를 사용하여 보고서 내용 및 모양을 사용자 지정하는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 식을 작성하는 식 편집기<br /><br /> 사용자 지정 보고서 항목 및 사용자 지정 쿼리 디자이너 지원<br /><br /> <br /><br /> 자세한 내용은 [SQL Server Data Tools의 Reporting Services&#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)를 참조하세요.|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|보고서 작성기|이 도구를 사용하여 보고서를 디자인합니다. 다음과 같은 기능이 포함되어 있습니다.<br /><br /> 기본 모드 또는 SharePoint 모드 보고서 서버에 배포합니다.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office와 비슷한 제작 환경[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]<br /><br /> 보고서 항목을 보고서 파트로 저장하는 기능<br /><br /> 지도를 만들 수 있는 마법사<br /><br /> 집계의 집계<br /><br /> 향상된 식 지원<br /><br /> 선택한 기본 제공 데이터 원본 유형에서 검색할 데이터를 지정하는 데 유용한 쿼리 디자이너<br /><br /> 자세한 내용은 [SQL Server의 보고서 작성기](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)를 참조하세요.|[독립 실행형 버전의 보고서 작성기](https://go.microsoft.com/fwlink/?LinkID=219138)다운로드<br /><br /> 또는 보고서 관리자/SharePoint에서 열기|  
  
## <a name="tools-for-report-server-administration"></a>보고서 서버 관리를 위한 도구  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서 서버 관리에 사용할 수 있는 그래픽 및 스크립팅 도구 집합입니다. 사용하는 도구는 사용하는 보고서 서버의 배포 모드에 따라 다릅니다.  
  
### <a name="native-mode"></a>기본 모드  
 다음 표에서는 기본 모드에서 배포된 보고서 서버를 관리하는 데 사용할 수 있는 도구를 보여 줍니다.  
  
|도구|설명|액세스 방법|  
|----------|-----------------|-------------------|  
|Reporting Services 구성 관리자|이 도구를 사용하면 Reporting Services 설치를 구성할 수 있습니다. 사용 가능한 태스크는 다음과 같습니다.<br /><br /> 로컬 및 원격 보고서 서버 인스턴스 구성<br /><br /> 보고서 서버 서비스 계정 구성<br /><br /> 하나 이상의 웹 서비스 URL 만들기 및 구성<br /><br /> 보고서 관리자 URL 구성<br /><br /> 보고서 서버 데이터베이스 만들기 및 구성<br /><br /> 스케일 아웃 배포 구성<br /><br /> 저장된 연결 문자열과 자격 증명을 암호화하는 데 사용되는 대칭 키 백업, 복원 또는 교체<br /><br /> 무인 실행 계정 구성<br /><br /> 전자 메일 배달을 위한 SMTP 서버 구성<br /><br /> <br /><br /> 참고: Reporting Services 구성 관리자를 사용하여 보고서 서버 내용을 관리하거나 추가 기능을 활성화하거나 서버 액세스 권한을 부여할 수는 없습니다.<br /><br /> 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)을 참조하세요.|시작 메뉴|  
|SQL Server Management Studio|이 도구를 사용하면 단일 환경에서 하나 이상의 보고서 서버 인스턴스를 다음과 같이 관리합니다.<br /><br /> 로컬 및 원격 보고서 서버 인스턴스 관리<br /><br /> 보고서 서버 속성 설정<br /><br /> 역할 정의 수정<br /><br /> 사용하지 않을 보고서 서버 기능 해제<br /><br /> 작업 관리<br /><br /> 공유 일정 관리|시작 메뉴|  
|SQL Server 구성 관리자|이 도구를 사용하면 다음을 수행할 수 있습니다.<br /><br /> Reporting Services Windows 서비스 시작 및 중지<br /><br /> 고객 의견 보고, 덤프 디렉터리 위치 및 오류 보고 구성<br /><br /> <br /><br /> **\*\* 경고 \*\*** 서비스 계정을 구성할 때는 이 도구를 사용하지 마세요. 대신 Reporting Services 구성 도구를 사용합니다.<br /><br /> 자세한 내용은 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)을 참조하세요.|시작 메뉴|  
|Rsconfig 유틸리티|이 도구를 사용하면 보고서 서버 데이터베이스에 대한 보고서 서버 연결을 구성하고 관리할 수 있습니다. 또한 무인 보고서 처리에 사용할 사용자 계정을 지정할 때도 이 유틸리티를 사용할 수 있습니다.<br /><br /> 자세한 내용은 [보고서 서버 명령 프롬프트 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)를 참조하세요.|명령 프롬프트|  
|Rskeymgmt 유틸리티|이 도구를 사용하면 다음을 수행할 수 있습니다.<br /><br /> 보고서 서버 데이터를 암호화 하는 데 사용하는 대칭 키 추출, 복원, 만들기 및 삭제<br /><br /> 스케일 아웃 배포에서 보고서 서버 인스턴스 조인<br /><br /> <br /><br /> 자세한 내용은 [보고서 서버 명령 프롬프트 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)를 참조하세요.|명령 프롬프트|  
|WMI(Windows Management Instrumentation) 클래스|이 클래스를 사용하면 그래픽 사용자 인터페이스를 사용하지 않고도 Reporting Services 구성 관리자의 구성 태스크를 자동화할 수 있습니다.<br /><br /> 자세한 내용은 [Accessing the WMI Provider Programmatically](../../reporting-services/accessing-the-wmi-provider-programmatically.md)을 참조하세요.|Visual Basic 스크립트|  
  
### <a name="sharepoint-integrated-mode"></a>SharePoint 통합 모드  
 SharePoint 모드의 Reporting Services는 SharePoint 아키텍처의 서비스 응용 프로그램이며 SharePoint를 통해 직접 관리됩니다.  
  
|도구|설명|액세스 방법|  
|----------|-----------------|-------------------|  
|SharePoint 중앙 관리|SharePoint 중앙 관리를 사용하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 공유 서비스 응용 프로그램을 만들고 쿼리하며 관리할 수 있습니다.<br /><br /> 자세한 내용은 [보고서 서버의 구성 및 관리&#40;Reporting Services SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)를 참조하세요.|중앙 관리를 위한 SharePoint 사이트 URL 브라우저|  
|PowerShell Cmdlet|PowerShell cmdlet을 사용하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 공유 서비스 응용 프로그램을 만들고 쿼리하며 관리할 수 있습니다.<br /><br /> 자세한 내용은 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)을 참조하세요.|SharePoint 2010 관리 셸|  
  
## <a name="tools-for-report-content-management"></a>보고서 내용 관리를 위한 도구  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서 내용 관리에 사용할 수 있는 그래픽 및 스크립팅 도구 집합입니다. 사용하는 도구는 사용하는 보고서 서버의 배포 모드에 따라 다릅니다.  
  
|도구|설명|액세스 방법|  
|----------|-----------------|-------------------|  
|보고서 서버 웹 서비스 URL|이 도구를 사용하면 보고서 카탈로그 내용을 일반 항목 탐색 창에서 찾아볼 수 있습니다.<br /><br /> 자세한 내용은 [Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md)을 참조하세요.|브라우저|  
|웹 포털|**(기본 모드 전용)** 이 도구를 사용하면 HTTP 연결을 통해 원격 위치에서 단일 보고서 서버 인스턴스를 관리할 수 있습니다. 사용할 수 있는 기능은 다음과 같습니다.<br /><br /> 보고서 보기, 검색, 인쇄 및 구독<br /><br /> 서버의 항목을 체계적으로 구성하도록 폴더 계층 구조 생성, 보안 설정 및 유지 관리<br /><br /> 항목 및 작업에 대한 액세스 권한을 결정하는 역할 기반 보안 구성<br /><br /> 보고서 실행 속성, 보고서 기록 및 보고서 매개 변수 구성<br /><br /> 연결을 설정하고 Microsoft SQL Server Analysis Services 데이터 원본 또는 SQL Server 관계형 데이터 원본에서 데이터를 검색하는 보고서 모델 만들기<br /><br /> 모델의 특정 엔터티에 대한 액세스를 허용하도록 모델 항목 보안 설정 또는 미리 정의된 클릭 광고 보고서에 엔터티 매핑<br /><br /> 일정 및 데이터 원본 연결을 편리하게 관리하기 위해 공유 일정 및 공유 데이터 원본 만들기<br /><br /> 대규모 받는 사람 목록에 보고서를 전달하는 데이터 기반 구독 만들기<br /><br /> 기존 보고서를 다른 방식으로 다시 사용하고 용도를 변경하기 위해 링크된 보고서 만들기<br /><br /> 보고서 서버에서 저장하고 실행할 수 있는 보고서를 만들기 위해 보고서 작성기 시작 자세한 내용은 [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md)을 참조하세요.| 브라우저  
|RS 유틸리티|이 도구는 스크립팅된 작업을 수행하는 데 사용할 수 있는 스크립트 호스트입니다. 이 도구를 사용하면 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 스크립트를 실행하여 보고서 서버 데이터베이스 간의 데이터 복사, 보고서 게시, 보고서 서버 데이터베이스에 항목 만들기 등을 수행할 수 있습니다. 자세한 내용은 [보고서 서버 명령 프롬프트 유틸리티&#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)를 참조하세요.|명령 프롬프트|  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 보고서 서버](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Reporting Services 개념&#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Reporting Services&#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
