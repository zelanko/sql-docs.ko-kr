---
title: PowerPivot 구성 및 솔루션 배포 (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23eaa3b9394822399618a99483dfb2b22fe13455
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079961"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>Configure PowerPivot and Deploy Solutions (SharePoint 2013)
  이 항목에서는 PowerPivot 갤러리, 데이터 새로 고침 예약, 관리 대시보드 및 데이터 공급자를 포함하여 [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)]의 PowerPivot 기능에 대한 중간 계층 향상 배포 및 구성에 대해 설명합니다. **SharePoint 2013용 PowerPivot 구성** 도구를 실행하여 다음을 수행합니다.  
  
-   SharePoint 솔루션 파일 배포  
  
-   PowerPivot 서비스 애플리케이션 만들기  
  
-   SharePoint 모드에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버를 사용하도록 Excel Services 애플리케이션을 구성합니다. 백 엔드 서비스 및 설치에 대 한 정보에 대 한는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 모드의 서버 참조 [SharePoint 용 PowerPivot 2013 설치](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)합니다.  
  
 PowerPivot for SharePoint 2013 구성 도구 설치에 대 한 내용은 참조 하세요 [를 설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot 제거 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [SharePoint 2013 구성에 대 한 PowerPivot을 실행 합니다.](#bkmk_run_configuration_tool)  
  
 [PowerPivot 구성 확인](#bkmk_verify_powerpivot)  
  
 [문제 해결](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a> SharePoint 2013 구성에 대 한 PowerPivot을 실행 합니다.  
 **참고:** 합니다 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 설치 마법사에 대 한 두 가지 구성 도구를 설치 [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]합니다. 구성 파일은 각각 SharePoint의 다른 버전을 지원합니다.  
  
|속성|Description|  
|----------|-----------------|  
|SharePoint 2013용 PowerPivot 구성|SharePoint 2013|  
|PowerPivot 구성 도구|SharePoint 2010 SP1(서비스 팩 1)|  
  
 **참고:** 다음 단계를 완료 하려면 팜 관리자 여야 합니다. 다음과 유사한 오류 메시지가 표시되는 경우  
  
-   "사용자가 팜 관리자가 없습니다. 유효성 검사 오류를 처리하고 다시 시도하십시오."  
  
 SharePoint를 설치한 계정으로 로그인하거나 설치 계정을 SharePoint 중앙 관리 사이트의 주 관리자로 구성합니다.  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **구성 도구**및 **SharePoint 2013용 PowerPivot 구성**을 차례로 클릭합니다. 도구는 SharePoint용 PowerPivot이 로컬 서버에 설치된 경우에만 표시됩니다.  
  
2.  **SharePoint용 PowerPivot 구성 또는 복구** 를 클릭한 다음 **확인**을 클릭합니다.  
  
3.  도구는 유효성 검사를 실행하여 PowerPivot의 현재 상태와 구성을 완료하는 데 필요한 단계를 확인합니다. 창을 전체 크기로 확장합니다. 창 아래쪽에 **유효성 검사**, **실행**및 **끝내기** 명령이 포함된 단추 모음이 표시됩니다.  
  
4.  **매개 변수** 탭에서  
  
    1.  **기본 계정 사용자 이름**: 기본 계정의 도메인 사용자 계정을 입력 합니다. 이 계정은 PowerPivot 서비스 애플리케이션 풀을 포함한 서비스를 프로비전하는 데 사용됩니다. 네트워크 서비스, 로컬 시스템 등의 기본 제공 계정을 지정하지 마세요. 이 도구는 기본 제공 계정을 지정하는 구성을 차단합니다.  
  
    2.  **데이터베이스 서버**: SharePoint 팜에 대해 지원 되는 SQL Server 데이터베이스 엔진을 사용할 수 있습니다.  
  
    3.  **Passphrase**: 암호를 입력 합니다. 새 SharePoint 팜을 만드는 경우 서버 또는 애플리케이션을 SharePoint 팜에 추가할 때마다 암호가 사용됩니다. 팜이 이미 있는 경우 서버 애플리케이션을 팜에 추가할 수 있는 암호를 입력합니다.  
  
    4.  **Excel Services 용 PowerPivot 서버**: 이름을 입력 한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 모드 서버. 단일 서버 배포에서 이는 데이터베이스 서버와 같습니다. `[ServerName]\powerpivot`  
  
    5.  왼쪽 창에서 **사이트 모음 만들기** 를 클릭합니다. 이후 단계에서 참조할 수 있도록 **사이트 URL** 을 기록해 둡니다. SharePoint 서버가 아직 구성되지 않은 경우 구성 마법사가 웹 애플리케이션 및 사이트 모음 URL을 `http://[ServerName]`의 루트로 기본 설정합니다. 기본값 수정 왼쪽된 창에서 다음 페이지를 검토 합니다. **기본 웹 응용 프로그램 만들기** 고 **웹 응용 프로그램 솔루션 배포**  
  
5.  필요에 따라 각 동작을 완료하는 데 사용되는 나머지 입력 값을 검토합니다. 동작의 세부 정보를 보고 검토하려면 왼쪽 창에서 각 동작을 클릭하세요. 각 동작에 대 한 자세한 내용은 섹션을 참조 하세요. "서버를 구성 하는 데 사용 되는 값 입력 [PowerPivot 구성 또는 복구 SharePoint 2010 &#40;PowerPivot 구성 도구&#41; ](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md) in this 항목.  
  
6.  선택적으로 지금 처리하지 않으려는 동작을 제거합니다. 예를 들어, Secure Store Service를 나중에 구성하려는 경우 **Secure Store Service 구성**을 클릭한 다음 **태스크 목록에 이 동작 포함**확인란의 선택을 취소합니다.  
  
7.  **유효성 검사** 를 클릭하여 목록에서 동작을 처리할 수 있는 충분한 정보가 도구에 있는지 여부를 확인합니다. 유효성 검사 오류가 표시되면 왼쪽 창에서 경고를 클릭하여 유효성 검사 오류에 대한 자세한 내용을 보세요. 유효성 검사 오류를 수정한 다음 **유효성 검사** 를 다시 클릭합니다.  
  
8.  **실행** 을 클릭하여 태스크 목록에 있는 모든 동작을 처리합니다. 동작의 유효성을 검사한 후에 **실행** 을 사용할 수 있습니다. **실행** 이 활성화되지 않으면 먼저 **유효성 검사** 를 클릭합니다.  
  
 자세한 내용은 [PowerPivot 구성 또는 복구 SharePoint 2010 용 &#40;PowerPivot 구성 도구&#41;](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a> PowerPivot 구성 확인  
 **서비스:**  
  
1.  중앙 관리의 시스템 설정에서 **서버의 서비스 관리**를 클릭합니다.  
  
2.  **SQL Server Analysis Services** 및 **SQL Server PowerPivot 시스템 서비스** 가 시작되었는지 확인합니다.  
  
 **팜 기능:**  
  
1.  중앙 관리의 시스템 설정에서 **팜 기능 관리**를 클릭합니다.  
  
2.  **PowerPivot 통합 기능** 이 **활성**인지 확인합니다.  
  
 **사이트 모음 기능:**  
  
1.  구성 도구로 만든 사이트 URL로 이동합니다.  
  
     클릭 **설정을**![SharePoint 설정](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 설정")를 클릭 하 고 **사이트 설정**합니다.  
  
     **사이트 모음 기능**을 클릭합니다.  
  
2.  **사이트 모음에 대한 PowerPivot 기능 통합** 이 **활성**상태인지 확인합니다.  
  
 **PowerPivot 서비스 응용 프로그램:**  
  
1.  중앙 관리의 **애플리케이션 관리**에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  서비스 애플리케이션 상태가 **시작**인지 확인합니다. 기본 이름은 **기본 PowerPivot 서비스 애플리케이션**입니다.  
  
     기본 서비스 애플리케이션의 이름을 클릭하여 서비스 애플리케이션에 대한 PowerPivot 관리 대시보드를 엽니다. 처음 사용하는 경우 대시보드는 로드하는 데 몇 분 정도 걸립니다.  
  
 자세한 내용은 [Verify a PowerPivot for SharePoint Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)을 참조하세요.  
  
##  <a name="bkmk_troubleshoot_issues"></a> 문제 해결  
 문제 해결을 돕기 위해 진단 로깅이 활성화되어 있는지 확인하는 것이 좋습니다.  
  
1.  SharePoint 중앙 관리에서 **모니터링** 을 클릭하고 **사용 현황 및 상태 데이터 수집 구성**을 클릭합니다.  
  
2.  **사용 현황 데이터 수집 사용** 이 선택되어 있는지 확인합니다.  
  
3.  다음 이벤트가 선택되어 있는지 확인합니다.  
  
    -   교육 원격 분석을 위한 사용 현황 필드 정의  
  
    -   PowerPivot 연결  
  
    -   PowerPivot 데이터 로드 사용  
  
    -   PowerPivot 쿼리 사용  
  
    -   PowerPivot 데이터 언로드 사용  
  
4.  **상태 데이터 수집 사용** 이 선택되어 있는지 확인합니다.  
  
5.  **확인**을 클릭합니다.  
  
 문제 해결 데이터 새로 고침에 대 한 자세한 내용은 참조 하세요. [PowerPivot 데이터 새로 고침 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx)합니다.  
  
 구성 도구에 대한 자세한 내용은 [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md)를 참조하세요.  
  
  
