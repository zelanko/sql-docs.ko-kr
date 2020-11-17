---
title: 가용성 그룹이 포함된 Reporting Services
description: SQL Server에서 Always On 가용성 그룹에 사용하도록 Reporting Services를 구성하는 방법을 알아봅니다. 지원되는 기능은 시나리오마다 다릅니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: edeb5c75-fb13-467e-873a-ab3aad88ab72
author: cawrites
ms.author: chadam
manager: erikre
ms.openlocfilehash: 260af6fa8615969a895425aa3d2145071b78eb72
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583965"
---
# <a name="reporting-services-with-always-on-availability-groups-sql-server"></a>Always On 가용성 그룹이 포함된 Reporting Services(SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] (AG)과 함께 작동하도록 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 구성하는 방법에 대한 정보를 제공합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 및 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 사용에 관한 세 가지 시나리오는 보고서 데이터 원본에 대한 데이터베이스, 보고서 서버 데이터베이스 및 보고서 디자인이 있습니다. 세 가지 시나리오에서 지원되는 기능과 필요한 구성은 서로 다릅니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 데이터 원본에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 을 사용할 경우의 중요한 이점 중 하나는 읽기 가능한 보조 복제본을 보고 데이터 원본으로 사용하는 것과 동시에 보조 복제본이 주 데이터베이스에 대한 장애 조치(Failover) 기능을 제공할 수 있다는 점입니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 일반적인 내용은 [SQL Server 2012에 대한 Always On FAQ(../../../sql-server/index.yml)](../../../sql-server/index.yml)를 참조하세요.  

##  <a name="requirements-for-using-reporting-services-and-always-on-availability-groups"></a><a name="bkmk_requirements"></a> Reporting Services 및 Always On 가용성 그룹 사용을 위한 요구 사항  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 및 Power BI Report Server에서는 .NET Framework 4.0을 사용하며 데이터 원본과 함께 사용할 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 연결 문자열 속성을 지원합니다.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 2014 이전 버전에  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 을 사용하려면 .Net 3.5 SP1에 대한 핫픽스를 다운로드하고 설치해야 합니다. 이 핫픽스는 AG 기능을 위한 SQL 클라이언트에 대한 지원과 **ApplicationIntent** 및 **MultiSubnetFailover** 연결 문자열 속성 지원을 추가합니다. 보고서 서버를 호스팅하는 각 컴퓨터에 이 핫픽스가 설치되어 있지 않으면 사용자가 보고서를 미리 보려고 시도할 때 다음과 비슷한 오류 메시지가 표시되고 오류 메시지가 보고서 서버의 추적 로그에 기록됩니다.  
  
> **오류 메시지:** "키워드가 지원되는 'applicationintent'가 아닙니다."  
  
 이 메시지는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 연결 문자열에 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 속성 중 하나를 포함했지만 서버에서 이러한 속성이 인식되지 않는 경우에 발생합니다. 위에 언급한 오류 메시지는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 사용자 인터페이스에서 '연결 테스트' 단추를 클릭할 때 그리고 원격 오류가 보고서 서버에 설정된 경우 보고서를 미리 볼 때 표시됩니다.  
  
 필요한 핫픽스에 대한 자세한 내용은 [KB 2654347A – SQL Server 2012의 Always On 기능에 대한 지원을 .NET Framework 3.5 SP1에 도입하는 핫픽스](https://go.microsoft.com/fwlink/?LinkId=242896)를 참조하세요.  
  
 기타 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 요구 사항에 대한 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
> [!NOTE]  
>  **RSreportserver.config** 와 같은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 파일은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능의 일부로 지원되지 않습니다. 보고서 서버 중 하나에서 구성 파일을 수동으로 변경할 경우 복제본을 수동으로 업데이트해야 합니다.  
  
##  <a name="report-data-sources-and-availability-groups"></a><a name="bkmk_reportdatasources"></a> 보고서 데이터 원본 및 가용성 그룹  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 을 기반으로 하는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 데이터 원본의 동작은 관리자가 AG 환경을 구성한 방법에 따라 다를 수 있습니다.  
  
 보고서 데이터 원본 연결 문자열을 구성하는 데 필요한 보고서 데이터 원본에 대해 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 활용하려면 가용성 그룹 *리스너 DNS 이름* 을 사용합니다. 지원되는 데이터 원본은 다음과 같습니다.  
  
-   SQL 기본 클라이언트를 사용하는 ODBC 데이터 원본  
  
-   보고서 서버에 .Net 핫픽스가 적용된 SQL 클라이언트  
  
 또한 연결 문자열은 읽기 전용 보고를 위해 보조 복제본을 사용하도록 보고서 쿼리 요청을 구성하는 새 Always On 연결 속성을 포함합니다. 보고 요청을 위해 보조 복제본을 사용할 경우 읽기/쓰기 용도의 주 복제본에 대한 부하가 줄어듭니다. 다음 그림은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 원본 연결 문자열이 ApplicationIntent=ReadOnly로 구성된 세 개의 복제본 AG 구성 예입니다. 이 예에서 보고서 쿼리 요청은 주 복제본이 아니라 보조 복제본으로 전송됩니다.  
  
 
  
 다음은 [AvailabilityGroupListenerName]이 복제본을 만들 때 구성된 **리스너 DNS 이름** 인 연결 문자열의 예입니다.  
  
 `Data Source=[AvailabilityGroupListenerName];Initial Catalog = AdventureWorks2016; ApplicationIntent=ReadOnly`  
  
 **사용자 인터페이스에서** 연결 테스트 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 단추는 연결을 설정할 수 있는지에 대한 유효성을 검사하지만 AG 구성의 유효성은 검사하지 않습니다. 예를 들어 연결 문자열에 AG에 속하지 않는 서버에 대한 ApplicationIntent를 포함한 경우 추가 매개 변수가 무시되고 **연결 테스트** 단추를 클릭하면 지정된 서버에 대한 연결을 설정할 수 있는지에 대해서만 유효성을 검사합니다.  
  
 보고서를 만들고 게시하는 방법에 따라 연결 문자열을 편집할 위치가 결정됩니다.  
  
-   **기본 모드:** 기본 모드 보고서 서버에 이미 게시된 공유 데이터 원본 및 보고서에 대해 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../../includes/ssrswebportal-non-markdown-md.md)]를 사용합니다.  
  
-   **SharePoint 모드:** SharePoint 서버에 이미 게시된 보고서에 대한 문서 라이브러리 내에서 SharePoint 구성 페이지를 사용합니다.  
  
-   **보고서 디자인:** 새 보고서를 만들 때 [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]를 사용합니다. 이 항목의 '보고서 디자인' 섹션 또는 추가 정보를 참조하세요.  
  
 **추가 리소스:**  
  
-   [보고서 데이터 원본 관리](../../../reporting-services/report-data/manage-report-data-sources.md)  
  
-   사용 가능한 연결 문자열 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.  
  
-   가용성 그룹 수신기에 대한 자세한 내용은 [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)을 참조하세요.  
  
 **고려 사항:** 보조 복제본이 주 복제본에서 데이터 변경 내용을 수신할 때는 일반적으로 시간이 지연됩니다. 주 복제본과 보조 복제본 사이의 업데이트 시간 지연에 영향을 줄 수 있는 요소는 다음과 같습니다.  
  
-   보조 복제본의 수. 구성에 보조 복제본을 추가할수록 지연 시간이 늘어납니다.  
  
-   주 복제본과 보조 복제본 사이의 지리적 위치 및 거리. 예를 들어 보조 복제본이 다른 데이터 센터에 있을 경우에는 주 복제본과 같은 건물 안에 있을 때에 비해 지연 시간이 더 길어집니다.  
  
-   각 복제본의 가용성 모드 구성. 가용성 모드는 보조 복제본이 트랜잭션을 디스크에 쓸 때까지 주 복제본이 데이터베이스에서 트랜잭션을 커밋하기 위해 기다리는지 여부를 결정합니다. 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)의 '가용성 모드' 섹션을 참조하세요.  
  
 읽기 전용 보조 복제본을 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 원본으로 사용할 경우 데이터 업데이트 지연 시간이 보고서 사용자의 요구를 충족시킬 수 있는지 확인해야 합니다.  
  
##  <a name="report-design-and-availability-groups"></a><a name="bkmk_reportdesign"></a> 보고서 디자인 및 가용성 그룹  
 [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)] 에서 보고서를 디자인하거나 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 보고서 프로젝트를 디자인할 때 사용자는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 제공되는 새로운 연결 속성을 포함하도록 보고서 데이터 원본 연결 문자열을 구성할 수 있습니다. 새 연결 속성에 대한 지원은 사용자가 보고서를 미리 보는 위치에 따라 달라집니다.  
  
-   **로컬 미리 보기:** [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]는 .NET Framework 4.0을 사용하고 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 연결 문자열 속성을 지원합니다.  
  
-   **원격 또는 서버 모드 미리 보기:** 보고서를 보고서 서버에 게시한 후 또는 [!INCLUDE[ssRBnoversion](../../../includes/ssrbnoversion.md)]에서 미리 보기를 사용한 후 다음과 비슷한 오류가 표시되면 보고서를 미리 보려고 시도한 보고서 서버에 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 .Net Framework 3.5 SP1 핫픽스가 설치되지 않았기 때문입니다.  
  
> **오류 메시지:** "키워드가 지원되는 'applicationintent'가 아닙니다."  
  
##  <a name="report-server-databases-and-availability-groups"></a><a name="bkmk_reportserverdatabases"></a> 보고서 서버 데이터베이스 및 가용성 그룹  
 Reporting Services 및 Power BI Report Server는 보고서 서버 데이터베이스에 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 사용하는 데 있어서 제한적인 지원을 제공합니다. 보고서 서버 데이터베이스를 AG에서 복제본의 일부로 구성할 수 있지만 장애 조치(Failover)가 발생했을 때 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 가 보고서 서버 데이터베이스에 대해 다른 복제본을 자동으로 사용하지는 않습니다. 보고서 서버 데이터베이스와 함께 MultiSubnetFailover 사용은 지원되지 않습니다.  
  
 장애 조치(Failover) 및 복구를 완료하기 위해서는 작업을 수동으로 수행하거나 사용자 지정 자동화 스크립트를 사용해야 합니다. 이러한 작업을 완료할 때까지는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 장애 조치(Failover) 후 보고서 서버의 일부 기능이 올바르게 작동하지 않을 수 있습니다.  
  
> [!NOTE]  
>  보고서 서버 데이터베이스에 대해 장애 조치(Failover) 및 재해 복구를 계획할 때는 항상 보고서 서버 암호화 키의 복사본을 백업하는 것이 좋습니다.  
  
###  <a name="differences-between-sharepoint-native-mode"></a><a name="bkmk_differences_in_server_mode"></a> SharePoint 기본 모드 간 차이점  
 이 단원에서는 SharePoint 모드와 기본 모드의 보고서 서버가 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]과 상호 작용하는 방법상의 차이점에 대해 요약해서 보여 줍니다.  
  
 SharePoint 보고서 서버는 사용자가 만드는 각 **서비스 애플리케이션에 대해** 3 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 개의 데이터베이스를 만듭니다. SharePoint 모드에서 보고서 서버 데이터베이스에 대한 연결은 서비스 애플리케이션을 만들 때 SharePoint 중앙 관리에 구성됩니다. 데이터베이스의 기본 이름에는 서비스 애플리케이션과 연결된 GUID가 포함됩니다. 다음은 SharePoint 모드 보고서 서버에 대한 데이터베이스의 이름 예입니다.  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6TempDB  
  
-   ReportingService_85c08ac3c8e64d3cb400ad06ed5da5d6_Alerting  
  
 기본 모드 보고서 서버는 **2** 개의 데이터베이스를 사용합니다. 다음은 기본 모드 보고서 서버에 대한 데이터베이스의 이름 예입니다.  
  
-   ReportServer  
  
-   ReportServerTempDB  
  
 기본 모드에서는 경고 데이터베이스 및 관련 기능을 지원하거나 사용하지 않습니다. 기본 모드 보고서 서버는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 관리자에서 구성합니다. SharePoint 모드의 경우 서비스 애플리케이션 데이터베이스 이름을 SharePoint 구성 중에 만든 "클라이언트 액세스 지점"의 이름으로 구성합니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에서 SharePoint 구성에 대한 자세한 내용은 [SharePoint Server용 SQL Server 가용성 그룹 구성 및 관리(/previous-versions/office/sharepoint-server-2010/hh913923(v=office.14))](/previous-versions/office/sharepoint-server-2010/hh913923(v=office.14))를 참조하세요.  
  
> [!NOTE]
>  SharePoint 모드 보고서 서버는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서비스 애플리케이션 데이터베이스와 SharePoint 콘텐츠 데이터베이스 사이의 동기화 프로세스를 사용합니다. 보고서 서버 데이터베이스와 콘텐츠 데이터베이스를 함께 유지 관리하는 것이 중요합니다. 이를 하나의 집합으로 장애 조치(Failover)하고 복구할 수 있도록 동일한 가용성으로 구성해야 합니다. 다음과 같은 시나리오를 고려해 보세요.  
> 
>  -   보고서 서버 데이터베이스가 수신한 것과 동일한 최근 업데이트가 아직 수신되지 않은 콘텐츠 데이터베이스의 복사본을 복원 또는 장애 조치(Failover)해야 하는 경우  
> -   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 동기화 프로세스에서 콘텐츠 데이터베이스 및 보고서 서버 데이터베이스에 있는 항목 목록 간에 불일치가 발견된 경우  
> -   동기화 프로세스로 콘텐츠 데이터베이스에 있는 항목이 삭제되거나 업데이트되는 경우  
  
###  <a name="prepare-report-server-databases-for-availability-groups"></a><a name="bkmk_prepare_databases"></a> 가용성 그룹에 대한 보고서 서버 데이터베이스 준비  
 보고서 서버 데이터베이스를 준비하고 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 추가하는 기본 단계는 다음과 같습니다.  
  
-   가용성 그룹을 만들고 *리스너 DNS 이름* 을 구성합니다.  
  
-   **주 복제본:** 단일 가용성 그룹에 포함할 보고서 서버 데이터베이스를 구성하고 보고서 서버 데이터베이스를 모두 포함하는 주 복제본을 만듭니다.  
  
-   **보조 복제본:** 하나 이상의 보조 복제본을 만듭니다. 주 복제본의 데이터베이스를 보조 복제본으로 복사하는 일반적인 방법은 'RESTORE WITH NORECOVERY'를 사용하여 각 보조 복제본에 데이터베이스를 복원하는 것입니다. 보조 복제본을 만들고 데이터 동기화가 작동하는지 확인하는 방법은 [Always On 보조 데이터베이스에서 데이터 이동 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)을 참조하세요.  
  
-   **보고서 서버 자격 증명:** 주 복제본에 만든 적합한 보고서 서버 자격 증명을 보조 복제본에 만들어야 합니다. 정확한 단계는 Window [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 서비스 계정, Windows 사용자 계정 또는 SQL Server 인증 등 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 환경에서 사용 중인 인증 유형에 따라 달라집니다. 자세한 내용은 [보고서 서버 데이터베이스 연결 구성&#40;SSRS 구성 관리자&#41;](../../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)을 참조하세요.  
  
-   리스너 DNS 이름을 사용하도록 데이터베이스 연결을 업데이트합니다. 기본 모드 보고서 서버의 경우 **구성 관리자에서** 보고서 서버 데이터베이스 이름 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 을 변경합니다. SharePoint 모드의 경우에는 **서비스 애플리케이션에 대해** 데이터베이스 서버 이름 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 을 변경합니다.  
  
###  <a name="steps-to-complete-disaster-recovery-of-report-server-databases"></a><a name="bkmk_steps_to_complete_failover"></a> 보고서 서버 데이터베이스의 재해 복구 완료 단계  
 보조 복제본으로 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 장애 조치(Failover)한 후에는 다음과 같은 단계를 완료해야 합니다.  
  
1.  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터베이스를 호스팅하는 주 데이터베이스 엔진에서 사용 중이던 SQL 에이전트 서비스의 인스턴스를 중지합니다.  
  
2.  새 주 복제본인 컴퓨터에서 SQL 에이전트 서비스를 시작합니다.  
  
3.  보고서 서버 서비스를 중지합니다.  
  
     보고서 서버가 기본 모드인 경우 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버 Windows 서버를 중지합니다.  
  
     보고서 서버가 SharePoint 모드로 구성된 경우 SharePoint 중앙 관리에서 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 공유 서비스를 중지합니다.  
  
4.  보고서 서버 서비스 또는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 서비스를 시작합니다.  
  
5.  새 주 복제본에 대해 보고서를 실행할 수 있는지 확인합니다.  
  
###  <a name="report-server-behavior-when-a-failover-occurs"></a><a name="bkmk_failover_behavior"></a> 장애 조치(Failover) 발생 시 보고서 서버 동작  
 보고서 서버 데이터베이스가 장애 조치(Failover)될 때 그리고 새 주 복제본을 사용하도록 보고서 서버 환경을 업데이트한 경우 장애 조치(Failover) 및 복구 프로세스로 인해 몇 가지 운영상의 문제가 발생할 수 있습니다. 이러한 문제로 인한 영향은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 이 보조 복제본으로 장애 조치(Failover)를 수행하고 보고서 서버 관리자가 새 주 복제본을 사용하도록 보고 환경을 업데이트하는 데 걸리는 시간뿐만 아니라 장애 조치(Failover) 발생 시의 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 부하에 따라 달라집니다.  
  
-   재시도 논리로 인해 그리고 장애 조치(Failover) 기간 중 보고서 서버가 예약된 작업을 완료로 표시할 수 없어서 백그라운드 처리에 대한 실행이 두 번 이상 수행될 수도 있습니다.  
  
-   장애 조치(Failover) 기간 중에는 SQL Server 에이전트가 보고서 서버 데이터베이스에 데이터를 쓸 수 없고 이 데이터가 새 주 복제본과 동기화되지 않기 때문에 일반적으로 실행되도록 트리거되는 백그라운드 처리에 대한 실행이 수행되지 않습니다.  
  
-   데이터베이스 장애 조치(Failover)가 완료되고 보고서 서버 서비스를 다시 시작한 후 SQL Server 에이전트 작업이 자동으로 다시 만들어집니다. SQL 에이전트 작업을 다시 만들 때까지는 SQL Server 에이전트 작업과 연관된 모든 백그라운드 실행이 처리되지 않습니다. 여기에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구독, 예약 및 스냅샷이 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 시작&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)   
 [SQL Server Native Client에서 연결 문자열 키워드 사용](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)   
 [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)   
 [가용성 복제본에 대한 클라이언트 연결 액세스 정보&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
