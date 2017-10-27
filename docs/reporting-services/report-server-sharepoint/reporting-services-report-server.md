---
title: "Reporting Services 보고서 서버 | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 51e3df193ddb01eaae45c559054ae93c98a55509
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---

# <a name="reporting-services-report-server"></a>Reporting Services 보고서 서버

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

중앙 부분에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services 설치 합니다. 처리 엔진과 기능 추가를 위한 확장과 함께 구성되어 있습니다.

> [!NOTE]
> SQL Server 2016 후 SharePoint와 reporting Services 통합을 사용할 수 없습니다.

Reporting Services 보고서 서버 배포 모드; 중 하나에서 실행 기본 모드 또는 SharePoint 모드입니다. 기능 비교는 [SharePoint와 기본 모드의 기능 비교](#bkmk_featuresupport) 섹션을 참조하세요.  
  
 **설치:** Reporting Services 설치 정보를 참조 하십시오. [Reporting Services 설치](../install-windows/install-reporting-services.md)합니다.

## <a name="overview-of-report-server-modes"></a>보고서 서버 모드의 개요

 처리 엔진(프로세서)는 보고서 서버의 핵심입니다. 프로세서는 보고 시스템의 무결성을 지원하며 수정 또는 확장될 수 없습니다. 확장 프로그램 또한 프로세서에 해당하지만 특정 기능을 수행합니다. Reporting Services 모든 유형의 지원 되는 확장에 대 한 하나 이상의 기본 확장 프로그램이 포함 되어 있습니다. 사용자 지정 확장 프로그램을 보고서 서버에 추가할 수 있는데 그럴 경우 기본적으로 지원되지 않는 지원 기능을 사용할 수 있도록 보고서 서버를 확장할 수 있습니다. Single Sign-on 기술 지원, 기본 렌더링 프로그램에서 지원하지 않는 응용 프로그램 형식의 보고서 출력, 프린터 또는 응용 프로그램으로의 보고서 배달 등이 사용자 지정 기능의 예입니다.  
  
 단일 보고서 서버 인스턴스는 초기 요청 처리부터 완성된 보고서 표시를 아우르는 종단 간 처리를 제공하는 프로세서 및 확장 프로그램의 전체 모음에 의해 정의됩니다. 보고서 서버는 하위 구성 요소를 통해 보고서 요청을 처리하고 요청 시 액세스 또는 예약된 배포에 보고서를 사용할 수 있도록 합니다.  
  
 보고서 서버를 사용하면 다양한 데이터 원본에 대한 보고서 제작 환경, 보고서 렌더링 및 보고서 배달 환경과 확장 가능한 인증 및 권한 부여 체계를 설정할 수 있습니다. 또한 보고서 서버에는 게시된 보고서, 공유 데이터 원본, 공유 데이터 집합, 보고서 파트, 공유 일정 및 구독, 보고서 정의 원본 파일, 모델 정의, 컴파일된 보고서, 스냅샷, 매개 변수 및 기타 리소스를 저장하는 보고서 서버 데이터베이스가 포함됩니다. 보고서 서버를 사용하면 보고서 요청 처리, 스냅숏 기록 유지 관리 외에도 보고서, 데이터 원본, 데이터 집합 및 구독에 대한 사용 권한을 관리하도록 보고서 서버를 구성하기 위한 관리 환경을 설정할 수 있습니다.  
  
 Reporting Services 보고서 서버에서는 보고서 서버 인스턴스에 대 한 배포의 두 가지 모드를 지원합니다.  
  
-   **기본 모드**: 기본 모드와 SharePoint 웹 파트를 보고서 서버 독점적으로 Reporting Services 구성 요소를 통해 모든 처리 및 관리 기능을 제공 하는 응용 프로그램 서버로 실행 되는 위치를 포함 합니다. Reporting Services 구성 관리자 및 SQL Server Management Studio 사용 하 여 기본 모드 보고서 서버를 구성합니다.  
  
-   **SharePoint 모드**: 보고서 서버가 SharePoint 서버 팜의 일부로 설치됩니다.  PowerShell 명령 또는 SharePoint 콘텐츠 관리 페이지를 사용하여 SharePoint 모드를 배포 및 구성합니다.  
  
 SQL Server Reporting Services에서 다른 보고서 서버를 한 모드를 전환할 수 없습니다. 환경에 사용되는 보고서 서버 유형을 변경하려면 원하는 보고서 서버 모드를 설치하고 이전 보고서 서버 버전의 보고서 항목 또는 보고서 서버 데이터베이스를 새 보고서 서버로 복사하거나 이동해야 합니다. 이러한 프로세스를 일반적으로 '마이그레이션'이라고 합니다. 마이그레이션하는 데 필요한 단계는 마이그레이션할 모드 및 원본 버전에 따라 달라집니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)를 참조하세요.  
  
## <a name="feature-comparison-of-sharepoint-and-native-mode"></a>SharePoint와 기본 모드의 기능 비교
  
|기능 또는 구성 요소|기본 모드|SharePoint 모드|  
|--------------------------|-----------------|---------------------|  
|**URL 주소 지정**|예|URL 주소 지정이 SharePoint 통합 모드에서 다르게 작동합니다. SharePoint URL은 보고서, 보고서 모델, 공유 데이터 원본 및 리소스를 참조하는 데 사용됩니다. 보고서 서버 폴더 계층은 사용되지 않습니다. 사용자 지정 응용 프로그램이 기본 모드 보고서 서버에서 지원되는 URL 액세스에 의존하는 경우 보고서 서버를 SharePoint 통합용으로 구성하면 해당 기능이 더 이상 작동하지 않습니다.<br /><br /> URL 액세스에 대한 자세한 내용은 [URL 액세스 매개 변수 참조](../../reporting-services/url-access-parameter-reference.md)를 참조하세요.|  
|**사용자 지정 보안 확장 프로그램**|예|Reporting Services 사용자 지정 보안 확장 프로그램 없습니다 배포 되거나 보고서 서버에 사용 합니다. 보고서 서버에는 SharePoint 통합 모드에서 실행되도록 보고서 서버를 구성할 때마다 사용되는 특수한 용도의 보안 확장 프로그램이 포함되어 있습니다. 이 보안 확장 프로그램은 내부 구성 요소로, 통합 작업에 필요합니다.|  
|**구성 관리자**|예|**\*\* 중요 \*\*** 구성 관리자를 사용하여 SharePoint 모드 보고서 서버를 관리할 수 없습니다. 대신 SharePoint 중앙 관리를 사용하세요.|  
|**보고서 관리자**|예|보고서 관리자를 사용하여 SharePoint 모드를 관리할 수 없습니다. SharePoint 응용 프로그램 페이지를 사용합니다. 자세한 내용은 [Reporting Services SharePoint Service 및 서비스 응용 프로그램](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)을 참조하세요.|  
|**링크된 보고서**|예|아니요.|  
|**내 보고서**|예|아니오|  
|**내 구독** 및 일괄 처리 방법|예|아니오|  
|**데이터 경고**|아니오|예|  
|**파워 뷰**|아니오|예<br /><br /> 클라이언트 브라우저에 Silverlight가 필요합니다. 브라우저 요구 사항에 대한 자세한 내용은 [Reporting Services 및 파워 뷰에 대한 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.|  
|**.RDL 보고서**|예|예<br /><br /> . RDL 보고서에서 실행할 수 Reporting Services 보고서 서버가 기본 모드 또는 SharePoint 모드.|  
|**.RDLX 보고서**|아니오|예<br /><br /> Power View 합니다. RDLX 보고서 수만 Reporting Services에서 보고서 서버 SharePoint 모드에서 실행 합니다.|  
|**SharePoint 목록 확장 프로그램을 위한 SharePoint 사용자 토큰 자격 증명**|아니오|예|  
|**인터넷 연결 배포를 위한 AAM 영역**|아니오|예|  
|**SharePoint 백업 및 복구**|아니오|예|  
|**ULS 로그 지원**|아니오|예|  
  
## <a name="native-mode"></a>기본 모드

 기본 모드에서 보고서 서버는 보고서 및 보고서 모델에 대한 모든 확인, 관리, 처리 및 배달 기능을 제공하는 독립 실행형 응용 프로그램 서버입니다. 이 모드는 보고서 서버 인스턴스의 기본 모드입니다. 설치 중 구성된 기본 모드 보고서 서버를 설치하거나 설치가 완료된 후 보고서 서버를 기본 모드 작업용으로 구성할 수 있습니다.  
  
 다음 다이어그램은 Reporting Services 기본 모드 배포의 3 계층 아키텍처를 보여 줍니다. 이 아키텍처에서는 데이터 계층의 보고서 서버 데이터베이스 및 데이터 원본, 중간 계층의 보고서 서버 구성 요소, 프레젠테이션 계층의 클라이언트 응용 프로그램 및 기본 제공 또는 사용자 지정 도구를 보여 주며, 서버 구성 요소 간 데이터 및 요청 흐름과 데이터 저장소에서 내용을 보내고 검색하는 구성 요소도 보여 줍니다.  
  
 ![Reporting Services 아키텍처](../../reporting-services/report-server-sharepoint/media/reporting-serv-arch.gif "Reporting Services 아키텍처")  
  
 보고서 서버는 웹 서비스, 백그라운드 처리 및 기타 작업을 호스팅하는 "보고서 서버 서비스"라고 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 서비스로 구현됩니다. 서비스 콘솔 응용 프로그램에서 이 서비스는 SQL Server Reporting Services(MSSQLSERVER)로 나열됩니다.  
  
 타사 개발자들은 보고서 서버의 처리 기능을 대체 또는 확장하기 위한 확장 프로그램을 추가로 만들 수 있습니다. 응용 프로그램 개발자가 사용할 수 있는 프로그래밍 인터페이스에 대한 자세한 내용은 [기술 참조](../../reporting-services/technical-reference-ssrs.md)를 참조하세요.  
  
### <a name="native-mode-with-sharepoint-web-parts"></a>기본 모드와 SharePoint 웹 파트

 Reporting Services 웹 파트를 설치 하 고 인스턴스의 등록을 제공 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0 이상 또는 [!INCLUDE[spPortalServ](../../includes/spportalserv-md.md)] 2003 이상. SharePoint 사이트에서 웹 파트를 찾고 기본 모드에서 실행 되는 보고서 서버에 저장 되 고 처리 하는 보고서를 볼 사용할 수 있습니다. 이러한 웹 파트는 이전 버전의 Reporting Services에서 도입 되었습니다.  
  
## <a name="sharepoint-mode"></a>SharePoint 모드

 SharePoint 모드에서는 보고서 서버가 SharePoint 서버 팜 내에서 실행되어야 합니다. 보고서 서버 처리, 렌더링 및 관리 기능 Reporting Services SharePoint 공유 서비스와 하나 이상의 Reporting Services 서비스 응용 프로그램을 실행 하는 SharePoint 응용 프로그램 서버로 표시 됩니다. SharePoint 사이트는 보고서 서버 내용 및 작업에 대한 프런트 엔드 액세스를 제공합니다.  
  
 SharePoint 모드에 필요한 사항은 다음과 같습니다.  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   SharePoint 2010 제품용 Reporting Services add-in의 적절 한 버전입니다.  
  
-   설치 하는 Reporting Services 공유 서비스 및 하나 이상의 Reporting Services 서비스 응용 프로그램 사용 하 여 SharePoint 응용 프로그램 서버.  
  
 다음 그림에는 SharePoint 모드 Reporting Services 환경을 보여 줍니다.  
  
 ![SSRS SharePoint 함수 아키텍처](../../reporting-services/report-server-sharepoint/media/rs-sharepoint-architecture.gif "SSRS SharePoint 함수 아키텍처")  
  
||Description|  
|-|-----------------|  
|**(1)**|웹 서버 또는 WFE(웹 프런트 엔드). Reporting Services 추가 기능을 보고서 또는 데이터 원본 또는 구독 관리와 같은 작업에 대 한 Reporting Services 관리 페이지 보기 등과 같은 웹 응용 프로그램 기능을 활용 하려는 각 웹 서버에 설치 되어야 합니다.|  
|**(2)**|추가 기능을 Reporting Services 서비스 프록시를 통해 응용 프로그램 서버와 통신 하는 클라이언트에 대 한 URL 및 SOAP 끝점을 설치 합니다.|  
|**(3)**|Reporting Services 공유 서비스를 실행 하는 응용 프로그램 서버. 보고서 처리의 확장 하 고 추가 응용 프로그램 서버에 Reporting Services 서비스를 추가 하 여 SharePoint 팜의 일부로 관리 됩니다.|  
|**(4)**|사용 권한, 전자 메일, 프록시 및 구독을 포함 하 여 각기 다른 구성으로 둘 이상의 Reporting Services 서비스 응용 프로그램을 만들 수 있습니다.|  
|**(5)**|보고서, 데이터 원본 및 기타 항목은 SharePoint 콘텐츠 데이터베이스에 저장됩니다.|  
|**(6)**|Reporting Services 서비스 응용 프로그램은 보고서 서버, 임시 및 데이터 경고 기능에 대 한 세 개의 데이터베이스를 만듭니다. 모든 SSRS 서비스 응용 프로그램에 적용되는 구성 설정은 **RSReportserver.config** 파일에 저장됩니다.|  
  
## <a name="report-process-and-schedule-and-delivery-process"></a>보고 프로세스 및 일정 예약 및 배달 프로세스

 보고서 서버에는 예비 및 중간 보고서 처리와 예약된 작업과 배달 작업을 수행하는 두 가지 처리 엔진이 있습니다. 보고서 처리기는 보고서 정의 또는 모델을 검색하고, 레이아웃 정보를 데이터 처리 확장 프로그램에서 가져온 데이터와 조합한 후 요청된 형식으로 렌더링합니다. 일정 예약 및 배달 프로세스는 일정에서 트리거된 보고서를 처리하고 대상으로 배달합니다.  
  
## <a name="report-server-database"></a>보고서 서버 데이터베이스

 보고서 서버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 모든 속성, 개체 및 메타데이터를 저장하는 상태 비저장 서버입니다. 저장되는 데이터로는 게시된 보고서, 컴파일된 보고서, 보고서 모델 및 보고서 서버가 관리하는 모든 항목에 대한 주소를 지정하는 폴더 계층 구조가 있습니다. 보고서 서버 데이터베이스는 확장 배포의 일부인 여러 보고서 서버 또는 단일 Reporting Services 설치에 대해 내부 저장소를 제공할 수 있습니다. SharePoint 제품 또는 기술의 대규모 배포에서 실행되도록 보고서 서버를 구성한 경우 보고서 서버는 보고서 서버 데이터베이스 이외에도 SharePoint 데이터베이스를 사용합니다. Reporting Services 설치에 사용되는 데이터 저장소에 대한 자세한 내용은 [보고서 서버 데이터베이스&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)를 참조하세요.  
  
## <a name="authentication-rendering-data-and-delivery-extensions"></a>인증, 렌더링, 데이터 및 배달 확장 프로그램

 보고서 서버에서 지원하는 확장 프로그램은 인증 확장 프로그램, 데이터 처리 확장 프로그램, 보고서 처리 확장 프로그램, 렌더링 확장 프로그램 및 배달 확장 프로그램입니다. 보고서 서버는 하나 이상의 인증 확장 프로그램, 데이터 처리 확장 프로그램 및 렌더링 확장 프로그램을 필요로 합니다. 배달 및 사용자 지정 보고서 처리 확장 프로그램은 선택적이지만 보고서 배포 또는 사용자 지정 컨트롤을 지원하려는 경우에는 반드시 필요합니다.  
  
 사용자 지정 구성 요소를 개발할 필요 없이 모든 서버 기능을 사용할 수 있도록 Reporting Services에서는 기본 확장 프로그램을 제공합니다. 다음 표에서는 즉시 사용 가능한 기능을 제공하는 전체 보고서 서버 인스턴스에 영향을 주는 기본 확장 프로그램에 대해 설명합니다.  
  
|형식|기본값|  
|----------|-------------|  
|인증|기본 보고서 서버 인스턴스는 가장 및 위임 기능(도메인에 설정된 경우)을 비롯한 Windows 인증을 지원합니다.|  
|데이터 처리|기본 보고서 서버 인스턴스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion Essbase, SAPBW, OLE DB, 병렬 데이터 웨어하우스 및 ODBC 데이터 원본용 데이터 처리 확장 프로그램이 있습니다.|  
|렌더링|기본 보고서 서버 인스턴스에는 HTML, Excel, CSV, XML, 이미지, Word, SharePoint 목록 및 PDF용 렌더링 확장 프로그램이 있습니다.|  
|배달|기본 보고서 서버 인스턴스에는 전자 메일 배달 확장 프로그램과 파일 공유 배달 확장 프로그램이 있습니다. 보고서 서버가 SharePoint 통합용으로 구성된 경우 보고서를 SharePoint 라이브러리에 저장하는 배달 확장 프로그램을 사용할 수 있습니다.|  
  
> [!NOTE]  
>  Reporting Services는 서버를 관리하고 콘텐츠를 작성하며 이 콘텐츠를 조직의 사용자가 사용할 수 있도록 설정하는 데 사용할 수 있는 모든 도구와 응용 프로그램을 포함합니다.  
  
## <a name="related-tasks"></a>관련 태스크

 다음 항목에서는 보고서 서버 설치, 사용 및 유지 관리에 대한 추가 정보를 제공합니다.  
  
|태스크|링크|  
|----------|----------|  
|하드웨어 및 소프트웨어 요구 사항을 검토합니다.|[Hardware and Software Requirements for Reporting Services in SharePoint Mode](http://msdn.microsoft.com/library/ed91877d-4f74-4266-a932-b824b4810c99)입니다.|  
|SharePoint 모드의 Reporting Services를 설치 합니다.|[SharePoint 2010 용 Reporting Services SharePoint 모드 설치](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)|  
|웹 개발자나 CSS 스타일시트 파일을 만드는 전문가인 경우 기본 스타일을 수정하여 도구 모음이나 보고서 관리자의 색, 글꼴 및 레이아웃을 변경할 수 있습니다. 단, 이로 인해 발생하는 모든 문제에 대한 책임은 자신에게 있습니다. 이 릴리스에서는 기본 스타일시트나 스타일시트 수정 지침을 다루지 않습니다.|[HTML 뷰어 및 보고서 관리자에 대한 스타일시트 사용자 지정](http://msdn.microsoft.com/library/df805cff-b1de-4062-b2ac-423f37390fbd)|  
|HTML 스타일 및 CSS 스타일시트에 익숙한 웹 개발자는 이 항목의 정보를 사용하여 보고서 관리자의 모양을 사용자 지정하기 위해 수정할 수 있는 파일을 확인할 수 있습니다.|[웹 포털에서 사용자 지정 인증 쿠키를 전달하도록 구성](assetid:///91aeb053-149e-4562-ae4c-a688d0e1b2ba)|  
|보고서 서버 웹 서비스 및 Windows 서비스에 대한 메모리 설정을 튜닝하는 방법에 대해 설명합니다.|[보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)|  
|원격 관리를 위해 보고서 서버를 구성하는 권장 단계에 대해 설명합니다.|[원격 관리를 위한 보고서 서버 구성](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)|  
|기본 보고서 서버 인스턴스에서 **내 보고서** 의 가용성을 구성하는 방법에 대한 지침을 제공합니다.|[내 보고서 설정 및 해제](../../reporting-services/report-server/enable-and-disable-my-reports.md)|  
|지원되는 브라우저 내에서 인쇄 기능을 제공하는 RSClientPrint 컨트롤을 설정하는 방법에 대한 지침을 제공합니다. 브라우저 요구 사항에 대한 자세한 내용은 [Reporting Services 및 파워 뷰에 대한 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.|[Reporting Services에 대한 클라이언트 쪽 인쇄 기능 사용 및 사용 안 함 설정](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)|  

## <a name="next-steps"></a>다음 단계

[Reporting Services 확장 프로그램](../../reporting-services/extensions/reporting-services-extensions.md)   
[Reporting Services 도구](../../reporting-services/tools/reporting-services-tools.md)   
[구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
[보고서 서버 데이터베이스&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[보안 확장 프로그램 구현](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
[데이터 처리 확장 프로그램 구현](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
[Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)

