---
title: SharePoint 2010에서 PowerPivot 데이터 새로 고침 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 01b54e6f-66e5-485c-acaa-3f9aa53119c9
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b92bb0b217ba9d6511bb4b5f26ae68a834bd6935
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312703"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2010"></a>SharePoint 2010에서 PowerPivot 데이터 새로 고침
  [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 데이터 새로 고침은 예약된 서버 쪽 작업으로서, 외부 데이터 원본을 쿼리하여 콘텐츠 라이브러리에 저장된 Excel 2010 통합 문서의 포함된 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 데이터를 업데이트합니다.  
  
 데이터 새로 고침은 SharePoint용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]의 기본 제공 기능이지만, 이 기능을 사용하려면 SharePoint 2010 팜에서 특정 서비스 및 타이머 작업을 실행해야 합니다. 데이터 새로 고침에 성공하기 위해서는 데이터 공급자 설치 및 데이터베이스 권한 검사와 같은 추가 관리 단계가 필요한 경우가 많습니다.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] SharePoint Server 2013 Excel Services 데이터 새로 고침에 다른 아키텍처를 사용 하 고 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 데이터 모델입니다. 새로운 아키텍처는 Excel Services를 기본 구성 요소로 사용하여 PowerPivot 데이터 모델을 로드합니다. 이전에 사용한 데이터 새로 고침 아키텍처는 PowerPivot 시스템 서비스와 SharePoint 모드의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 사용하여 데이터 모델을 로드했습니다. 자세한 내용은 [SharePoint 2013을 사용 하 여 PowerPivot 데이터 새로 고침](power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)합니다.  
  
 **항목 내용**  
  
 [1 단계: Secure Store Service 사용 및 마스터 키 생성](#bkmk_services)  
  
 [2 단계: 기능을 지원 하지 않으려는 경우 자격 증명 옵션 해제](#bkmk_creds)  
  
 [3 단계: 데이터 새로 고침에 사용 되는 자격 증명을 저장할 대상 응용 프로그램 만들기](#bkmk_stored)  
  
 [4 단계: 확장 가능한 데이터 새로 고침에 대 한 서버를 구성 합니다.](#bkmk_scale)  
  
 [5 단계: PowerPivot 데이터를 가져오는 데 사용 하는 데이터 공급자를 설치 합니다.](#bkmk_installdp)  
  
 [6 단계: 일정을 만들고 외부 데이터 원본에 액세스 하는 권한 부여](#bkmk_accounts)  
  
 [7 단계: 데이터 새로 고침에 대 한 통합 문서 업그레이드 사용](#bkmk_upgradewrkbk)  
  
 [8 단계: 데이터 새로 고침 구성 확인](#bkmk_verify)  
  
 [데이터 새로 고침에 대 한 구성 설정을 수정 합니다.](#bkmk_config)  
  
 [PowerPivot 데이터 새로 고침 타이머 작업 다시 예약](#configTimerJob)  
  
 [데이터 새로 고침 타이머 작업을 사용 하지 않도록 설정](#bkmk_disableDR)  
  
 서버 환경 및 권한이 구성되었는지 확인한 후에는 데이터 새로 고침을 바로 사용할 수 있습니다. 데이터 새로 고침을 사용하기 위해 SharePoint 사용자는 PowerPivot 통합 문서에서 데이터 새로 고침 발생 빈도를 지정하는 일정을 만듭니다. 주로 통합 문서 소유자 또는 파일을 SharePoint에 게시한 통합 문서 만든 이가 일정을 만듭니다. 이 사용자는 자신이 소유하는 통합 문서에 대한 데이터 새로 고침 일정을 만들어 관리합니다. 자세한 내용은 [데이터 새로 고침 예약 &#40;SharePoint 용 PowerPivot&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)합니다.  
  
##  <a name="bkmk_services"></a> 1 단계: Secure Store Service 사용 및 마스터 키 생성  
 PowerPivot 데이터 새로 고침은 데이터 새로 고침 작업을 실행하고 저장 프로시저를 사용하는 외부 데이터 원본에 연결하는 데 사용되는 자격 증명을 제공하는 Secure Store Service를 기반으로 합니다.  
  
 새 서버 옵션을 사용하여 SharePoint용 PowerPivot을 설치한 경우 Secure Store Service가 자동으로 구성됩니다. 모든 다른 설치 시나리오의 경우 Secure Store Service에 대한 서비스 응용 프로그램을 만들고 구성하고 마스터 암호화 키를 생성해야 합니다.  
  
> [!NOTE]  
>  Secure Store Service를 구성하거나 Secure Store Service 관리를 다른 사용자에게 위임하려면 팜 관리자여야 합니다. Secure Store Services를 활성화한 후 설정을 구성하거나 수정하려면 서비스 응용 프로그램 관리자여야 합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  서비스 응용 프로그램 리본에서 **새로 만들기**를 클릭합니다.  
  
3.  **보안 저장소 서비스**를 선택합니다.  
  
4.  **보안 저장소 응용 프로그램 만들기** 페이지에서 응용 프로그램 이름을 입력합니다.  
  
5.  **데이터베이스**에 이 서비스 응용 프로그램에 대한 데이터베이스를 호스팅할 SQL Server 인스턴스를 지정합니다. 기본값은 팜 구성 데이터베이스를 호스팅하는 SQL Server 데이터베이스 엔진 인스턴스입니다.  
  
6.  **데이터베이스 이름**에 서비스 응용 프로그램 데이터베이스의 이름을 입력합니다. 기본값은 Secure_Store_Service_DB_\<guid >. 기본 이름은 서비스 응용 프로그램의 기본 이름에 해당합니다. 고유한 서비스 응용 프로그램 이름을 입력한 경우 함께 관리할 수 있도록 데이터베이스 이름에 대해 비슷한 명명 규칙을 따릅니다.  
  
7.  **데이터베이스 인증**에서 기본값은 Windows  인증입니다. SQL 인증을 선택하는 경우 팜에서 이 인증 유형을 사용하는 방법에 대한 지침을 SharePoint 관리자 설명서에서 참조하십시오.  
  
8.  응용 프로그램 풀에서 **새 응용 프로그램 풀 만들기** 를 선택합니다. 다른 서버 관리자가 응용 프로그램 풀 사용 방법을 알 수 있도록 설명하는 이름을 지정합니다.  
  
9. 응용 프로그램 풀에 대한 보안 계정을 선택합니다. 도메인 사용자 계정을 사용할 관리 계정을 지정합니다.  
  
10. 나머지 기본값을 적용 하 고 클릭 **확인 합니다.** 을 클릭합니다. 서비스 응용 프로그램이 다른 관리 서비스와 함께 팜의 서비스 응용 프로그램 목록에 표시됩니다.  
  
11. 목록에서 보안 저장소 서비스 응용 프로그램을 클릭합니다.  
  
12. 서비스 응용 프로그램 리본에서 **관리**를 클릭합니다.  
  
13. 키 관리에서 **새 키 생성**을 클릭합니다.  
  
14. 전달 구를 입력한 다음 확인합니다. 이 전달 구는 추가 보안 저장소 공유 서비스 응용 프로그램을 추가하는 데 사용됩니다.  
  
15. **확인**을 클릭합니다.  
  
 문제 해결에 유용한 Store Service 작업의 감사 로깅을 사용하려면 이 기능을 사용하도록 설정해야 합니다. 로깅을 사용하도록 설정하는 방법은 [Secure Store Service 구성(SharePoint 2010)](http://go.microsoft.com/fwlink/p/?LinkID=223294)을 참조하십시오.  
  
##  <a name="bkmk_creds"></a> 2 단계: 기능을 지원 하지 않으려는 경우 자격 증명 옵션 해제  
 PowerPivot 데이터 새로 고침은 데이터 새로 고침 일정에 세 가지 자격 증명 옵션을 제공합니다. 통합 문서 소유자는 데이터 새로 고침을 예약할 때 이러한 옵션 중 하나를 선택하여 데이터 새로 고침 작업을 실행할 계정을 결정할 수 있습니다. 관리자는 일정 소유자가 사용할 수 있는 자격 증명 옵션을 결정할 수 있습니다.  
  
 데이터 새로 고침이 작동하려면 사용 가능한 옵션이 하나 이상 있어야 합니다.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 옵션 1 **관리자가 구성한 데이터 새로 고침 계정 사용**은 일정 정의 페이지에 항상 표시되지만 무인 데이터 새로 고침 계정을 구성한 경우에만 작동합니다. 계정을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [PowerPivot 무인 데이터 새로 고침 계정 구성 &#40;SharePoint 용 PowerPivot&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)합니다.  
  
 옵션 2 **다음 Windows 사용자 자격 증명을 사용하여 연결**은 페이지에 항상 표시되지만 서비스 응용 프로그램 구성 페이지에서 **사용자가 사용자 지정 Windows 자격 증명을 입력할 수 있습니다.** 옵션을 사용하도록 설정한 경우에만 작동합니다. 이 옵션은 기본적으로 사용되지만 사용 시 장점보다 단점이 많은 경우에는 사용하지 않도록 설정할 수 있습니다(아래 참조).  
  
 옵션 3 **Secure Store Service에 저장된 자격 증명을 사용하여 연결**은 페이지에 항상 표시되지만 일정 소유자가 유효한 대상 응용 프로그램을 제공한 경우에만 작동합니다. 관리자는 이러한 대상 응용 프로그램을 미리 만든 다음 데이터 새로 고침 일정을 만드는 사용자에게 응용 프로그램 이름을 제공해야 합니다. 새로 고침 작업 데이터에 대 한 대상 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 참조 하십시오 [PowerPivot 데이터 새로 고침을 위한 저장 된 자격 증명 구성 &#40;SharePoint 용 PowerPivot&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)합니다.  
  
 **자격 증명 옵션 2, "다음 Windows 사용자 자격 증명을 사용 하 여 연결" 구성**  
  
 PowerPivot 서비스 응용 프로그램에는 일정 소유자가 데이터 새로 고침 작업을 실행하기 위해 임의 Windows 사용자 이름 및 암호를 입력할 수 있는 자격 증명 옵션이 포함되어 있습니다. 이는 일정 정의 페이지의 두 번째 자격 증명 옵션입니다.  
  
 ![SSAS_PPS_ScheduleDataRefreshCreds](media/ssas-pps-scheduledatarefreshcreds.gif "SSAS_PPS_ScheduleDataRefreshCreds")  
  
 이 자격 증명 옵션은 기본적으로 사용하도록 설정되어 있습니다. 이 자격 증명 옵션을 사용하도록 설정하면 PowerPivot System Service에서 Secure Store Service에 일정 소유자가 입력한 사용자 이름 및 암호를 저장하는 대상 응용 프로그램을 생성합니다. 이 명명 규칙을 사용 하 여 생성 된 대상 응용 프로그램이 만들어집니다: PowerPivotDataRefresh_\<guid >. 각 Windows 자격 증명 집합에 대해 하나의 대상 응용 프로그램이 만들어집니다. PowerPivot System Service에서 소유하고 일정을 정의하는 사용자가 입력한 사용자 이름 및 암호를 저장하는 대상 응용 프로그램이 이미 있는 경우에는 PowerPivot System Service에서 대상 응용 프로그램을 만들지 않고 해당 대상 응용 프로그램을 사용합니다.  
  
 이 자격 증명 옵션을 사용할 경우의 가장 큰 이점은 사용 편의성과 단순성입니다. 대상 응용 프로그램이 자동으로 만들어지므로 추가 작업이 최소화됩니다. 또한 일정 소유자(통합 문서를 만든 사람과 거의 동일함)의 자격 증명으로 데이터 새로 고침을 실행하면 권한 요구 사항 다운스트림이 간소화됩니다. 대부분 이 사용자에게는 대상 데이터베이스에 대한 권한이 이미 있습니다. 이 사람의 Windows 사용자 ID로 데이터 새로 고침을 실행하면 '현재 사용자'를 지정하는 모든 데이터 연결이 자동으로 작동합니다.  
  
 반면, 단점은 관리 기능이 제한된다는 것입니다. 대상 응용 프로그램은 자동으로 만들어지지만 계정 정보가 변경될 때 자동으로 업데이트되거나 삭제되지 않습니다. 또한 암호 만료 정책으로 인해 이러한 대상 응용 프로그램이 더 이상 사용되지 않게 될 수도 있습니다. 만료된 자격 증명을 사용하는 데이터 새로 고침 작업은 시작할 수 없습니다. 이 경우 일정 소유자는 데이터 새로 고침 일정에서 현재 사용자 이름 및 암호 값을 제공하여 자격 증명을 업데이트해야 합니다. 그러면 새 대상 응용 프로그램이 만들어집니다. 시간이 지나면서 사용자가 데이터 새로 고침 일정에서 자격 증명 정보를 추가하고 수정함에 따라 시스템에서 유지되는 자동 생성된 대상 응용 프로그램이 증가할 수 있습니다.  
  
 현재 이러한 대상 응용 프로그램이 활성 상태인지, 비활성 상태인지 확인할 방법은 없으며 특정 대상 응용 프로그램을 해당 데이터 새로 고침 일정에 따라 역추적할 방법도 없습니다. 일반적으로 대상 응용 프로그램은 독립적으로 유지해야 합니다. 대상 응용 프로그램을 삭제하면 기존 데이터 새로 고침 일정이 중단될 수 있기 때문입니다. 현재 사용 중인 대상 응용 프로그램을 삭제하면 데이터 새로 고침이 실패하고 통합 문서의 데이터 새로 고침 기록 페이지에 "대상 응용 프로그램이 없습니다."라는 메시지가 나타납니다.  
  
 이 자격 증명 옵션을 사용하지 않도록 선택한 경우 PowerPivot 데이터 새로 고침을 위해 생성된 모든 대상 응용 프로그램을 안전하게 삭제할 수 있습니다.  
  
 **데이터 새로 고침 일정에서 임의 Windows 자격 증명 사용 안 함**  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  PowerPivot 서비스 응용 프로그램 이름을 클릭합니다. PowerPivot 관리 대시보드가 나타납니다.  
  
3.  동작에서 **서비스 응용 프로그램 설정 구성** 을 클릭하여 PowerPivot 서비스 응용 프로그램 설정 페이지를 엽니다.  
  
4.  데이터 새로 고침 섹션에서 **사용자가 사용자 지정 Windows 자격 증명을 입력할 수 있습니다.** 확인란의 선택을 취소합니다.  
  
     ![SSAS_PowerPivotDatarefreshOptions_AllowUser](media/ssas-powerpivotdatarefreshoptions-allowuser.gif "SSAS_PowerPivotDatarefreshOptions_AllowUser")  
  
##  <a name="bkmk_stored"></a> 3 단계: 데이터 새로 고침에 사용 되는 자격 증명을 저장할 대상 응용 프로그램 만들기  
 Secure Store Service가 구성되면 SharePoint 관리자는 대상 응용 프로그램을 만들어 PowerPivot 무인 데이터 새로 고침 계정 또는 데이터 새로 고침 작업을 실행하거나 외부 데이터 원본에 연결하는 데 사용할 다른 계정의 자격 증명을 비롯하여 저장된 자격 증명을 데이터 새로 고침 작업에 사용할 수 있게 설정할 수 있습니다.  
  
 이전 섹션에서 특정 자격 증명 옵션을 다시 사용하려면 대상 응용 프로그램을 만들어야 한다는 점을 설명했습니다. 특히, PowerPivot 무인 데이터 새로 고침 계정에 대한 대상 응용 프로그램을 만들고 이후 데이터 새로 고침 작업에서 사용할 수 있도록 저장해야 할 추가 자격 증명을 만들어야 합니다.  
  
 저장 된 자격 증명을 포함 하는 대상 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [PowerPivot 무인 데이터 새로 고침 계정 구성 &#40;SharePoint 용 PowerPivot&#41; ](configure-unattended-data-refresh-account-powerpivot-sharepoint.md) 하 고 [ PowerPivot 데이터 새로 고침에 대 한 저장 된 자격 증명 구성 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)합니다.  
  
##  <a name="bkmk_scale"></a> 4 단계: 확장 가능한 데이터 새로 고침에 대 한 서버를 구성 합니다.  
 기본적으로 각 SharePoint용 PowerPivot 설치에서는 요청 시 쿼리와 예약된 데이터 새로 고침을 둘 다 지원합니다.  
  
 각 설치에 대해 Analysis Services 서버 인스턴스에서 쿼리와 예약된 데이터 새로 고침을 둘 다 지원할지, 아니면 인스턴스가 특정 유형의 작업에만 사용되도록 할지 지정할 수 있습니다. 팜에 설치된 SharePoint용 PowerPivot이 여러 개인 경우 데이터 새로 고침 작업이 지연되거나 실패할 때를 대비하여 데이터 새로 고침 작업 전용 서버를 두는 것이 좋을 수 있습니다.  
  
 또한 기본 하드웨어에서 지원 가능한 경우 병렬로 실행되는 데이터 새로 고침 작업 수를 늘릴 수 있습니다. 기본적으로 병렬로 실행할 수 있는 작업 수는 시스템 메모리를 기준으로 계산되지만 작업을 지원할 수 있는 추가 CPU 용량이 있는 경우 이 수를 늘릴 수 있습니다.  
  
 자세한 내용은 [Query-Only 처리 또는 구성 전용 데이터 새로 고침 &#40;SharePoint 용 PowerPivot&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)합니다.  
  
##  <a name="bkmk_installdp"></a> 5 단계: PowerPivot 데이터를 가져오는 데 사용 하는 데이터 공급자를 설치 합니다.  
 데이터 새로 고침 작업은 기본적으로 원래 데이터를 검색하는, 반복되는 가져오기 작업입니다. 즉, PowerPivot 클라이언트 응용 프로그램에서 데이터를 가져오는 데 사용되는 것과 동일한 데이터 공급자가 PowerPivot 서버에도 설치되어 있어야 합니다.  
  
 Windows 서버에 데이터 공급자를 설치하려면 로컬 관리자여야 합니다. 추가 드라이버를 설치하려는 경우 SharePoint용 PowerPivot이 설치되어 있는 SharePoint 팜의 각 컴퓨터에 설치해야 합니다. 팜에 PowerPivot 서버가 여러 대 있는 경우 각 서버에 공급자를 설치해야 합니다.  
  
 SharePoint 서버는 64비트 응용 프로그램입니다. 데이터 새로 고침 작업을 지원하려면 사용 중인 데이터 공급자의 64비트 버전을 설치해야 합니다.  
  
##  <a name="bkmk_accounts"></a> 6 단계: 일정을 만들고 외부 데이터 원본에 액세스 하는 권한 부여  
 통합 문서 소유자 또는 만든 이가 통합 문서에서 데이터 새로 고침을 예약하려면 **참가** 권한이 있어야 합니다. 이 권한 수준이 제공되면 통합 문서의 데이터 새로 고침 구성 페이지를 열고 편집하여 데이터 새로 고침에 사용되는 자격 증명 및 일정 정보를 지정할 수 있습니다.  
  
 SharePoint 사용 권한 외에 외부 데이터 원본에 대한 데이터베이스 권한도 검토하여 데이터 새로 고침 중에 사용되는 계정에 데이터에 대한 액세스 권한이 있는지 확인해야 합니다. 부여해야 하는 권한은 통합 문서의 연결 문자열 및 데이터 새로 고침 작업을 실행하는 사용자 ID에 따라 다르므로 권한 요구 사항을 결정할 때는 신중하게 평가해야 합니다.  
  
 **PowerPivot 데이터 새로 고침 작업에 PowerPivot 통합 문서에서 기존 연결 문자열을 중요 하는 이유**  
  
 데이터 새로 고침이 실행되면 서버에서 데이터를 처음 가져올 때 만든 연결 문자열을 사용하여 외부 데이터 원본에 연결 요청을 보냅니다. 그런 다음 데이터 새로 고침 중에 이 연결 문자열에 지정된 서버 위치, 데이터베이스 이름 및 인증 매개 변수를 다시 사용하여 동일한 데이터 원본에 액세스합니다. 연결 문자열과 해당 전체 구성은 데이터 새로 고침을 위해 수정할 수 없습니다. 연결 문자열은 데이터 새로 고침 중에 있는 그대로 재사용됩니다. 경우에 따라 Windows 인증 이외의 인증을 사용하여 데이터 원본에 연결한 경우 연결 문자열에서 사용자 이름과 암호를 재정의할 수 있습니다. 여기에 대한 자세한 내용은 이 항목의 뒷부분에 제공되어 있습니다.  
  
 대부분의 통합 문서에서는 연결에 대한 기본 인증 옵션으로 트러스트된 연결 또는 Windows 통합 보안을 사용하므로 연결 문자열에 `SSPI=IntegratedSecurity` 또는 `SSPI=TrustedConnection`이 포함됩니다. 이 연결 문자열이 데이터 새로 고침 중에 사용된 경우 데이터 새로 고침 작업을 실행하는 데 사용되는 계정이 '현재 사용자'가 됩니다. 따라서 이 계정에는 트러스트된 연결을 통해 액세스되는 모든 외부 데이터 원본에 대한 읽기 권한이 있어야 합니다.  
  
 **PowerPivot 사용 하면 무인된 데이터 새로 고침 계정?**  
  
 그렇다면 해당 계정에 데이터를 새로 고치는 동안 액세스할 수 있는 데이터 원본에 대한 읽기 권한을 부여해야 합니다. 이 계정에 읽기 권한이 필요한 이유는 기본 인증 옵션을 사용하는 통합 문서에서는 무인 계정이 데이터를 새로 고치는 동안 '현재 사용자'가 되기 때문입니다. 일정 소유자가 연결 문자열에서 자격 증명을 재정의하지 않는 한 이 계정에는 조직에서 자주 사용되는 모든 데이터 원본에 대한 읽기 권한이 필요합니다.  
  
 **자격 증명 옵션 2: Windows 사용자 이름 및 암호를 입력할 경우 일정 소유자?**  
  
 일반적으로 PowerPivot 통합 문서를 만든 사용자는 처음에 데이터를 가져왔기 때문에 이미 충분한 권한이 있습니다. 이러한 사용자가 이후에 자신의 Windows 사용자 ID로 실행하도록 데이터 새로 고침을 구성한 경우에는 데이터베이스에 대한 권한이 이미 있는 해당 Windows 사용자 계정이 데이터를 새로 고치는 동안 데이터를 검색하는 데 사용됩니다. 따라서 기존 사용 권한이 충분해야 합니다.  
  
 **자격 증명 옵션 3을 사용 하 고: Secure Store Service 대상 응용 프로그램을 사용 하 여 데이터 새로 고침 작업을 실행 하기 위한 사용자 id를 제공 하 시겠습니까?**  
  
 데이터 새로 고침 작업을 실행하는 데 사용되는 모든 계정에는 읽기 권한이 있어야 합니다. 그 이유는 PowerPivot 무인 데이터 새로 고침 계정에 대해 설명된 이유와 같습니다.  
  
 **데이터 새로 고침 중에 사용 되는 자격 증명을 재정의할 수 있는지 여부를 확인 하려면 연결 문자열을 확인 하는 방법**  
  
 앞서 설명한 바와 같이 Windows 인증 이외의 인증(예: SQL Server 인증)이 연결에 사용되는 경우 데이터 새로 고침 작업 수준에서 다른 사용자 이름 및 암호를 대체할 수 있습니다. 비-Windows 자격 증명은 사용자 ID 및 암호 매개 변수를 통해 연결 문자열에 전달됩니다. 통합 문서에 이러한 매개 변수가 포함된 연결 문자열이 있는 경우 데이터 새로 고침에 사용되는 사용자 이름 및 암호를 해당 데이터 원본과 다르게 지정할 수 있습니다.  
  
 다음 단계에서는 사용자 이름 및 암호 재정의를 허용하는 연결 문자열이 있는지 여부를 확인하는 방법에 대해 설명합니다.  
  
1.  Excel에서 통합 문서를 엽니다.  
  
2.  Excel의 PowerPivot 리본에서 PowerPivot 창을 클릭하여 PowerPivot 창을 엽니다.  
  
3.  **디자인**을 클릭합니다.  
  
4.  **기존 연결**을 클릭합니다.  
  
     통합 문서에 사용된 모든 연결이 **PowerPivot 데이터 연결**아래에 나열됩니다.  
  
5.  연결을 선택하고 **편집**을 클릭한 다음 **고급**을 클릭합니다. 연결 문자열은 페이지의 맨 아래에 있습니다.  
  
 연결 문자열에 **Integrated Security=SSPI** 가 있으면 연결 문자열에서 자격 증명을 재정의할 수 없습니다. 이 경우 연결에서는 항상 현재 사용자를 사용하며, 사용자가 제공한 자격 증명은 모두 무시됩니다.  
  
 표시 되 면 **Persist Security Info = False, Password =\* \* \* \* \* \* \* \* \* \* \*, UserID =\<userlogin >** 은 자격 증명 재정의 허용 하는 연결 문자열을 사용 해야 합니다. 연결 문자열에 표시된 자격 증명(예: UserID 및 Password)은 Windows 자격 증명이 아니라 데이터베이스 로그인 또는 기타 대상 데이터 원본에 유효한 로그인 계정입니다.  
  
 **연결 문자열에서 자격 증명을 재정의 하는 방법**  
  
 자격 증명을 재정의하려면 데이터 새로 고침 일정에서 데이터 원본 자격 증명을 지정하면 됩니다. 관리자는 Secure Store Service에서 외부 데이터에 액세스하기 위해 사용되는 자격 증명에 매핑되는 대상 응용 프로그램을 제공할 수 있습니다. 그런 다음 일정 소유자가 자신이 정의하는 데이터 새로 고침 일정에 대상 응용 프로그램 ID를 입력할 수 있습니다. 이 대상 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [PowerPivot 데이터 새로 고침을 위한 저장 된 자격 증명 구성 &#40;SharePoint 용 PowerPivot&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)합니다.  
  
 또는 일정 소유자가 데이터를 새로 고치는 동안 데이터 원본에 연결하는 데 사용되는 자격 증명 집합을 입력할 수 있습니다. 다음 그림에서는 일정 정의 페이지의 이러한 데이터 원본 옵션을 보여 줍니다.  
  
 ![SSAS_PowerPivotKJ_DataRefreshDSOptions](media/ssas-powerpivotkj-datarefreshdsoptions.gif "SSAS_PowerPivotKJ_DataRefreshDSOptions")  
  
 **식별 데이터 액세스 요구 사항**  
  
 이전 섹션에서 설명한 대로, 데이터 새로 고침을 실행하는 데 사용되는 계정과 외부 데이터 원본에 연결하는 데 사용되는 계정은 하나이며 동일한 경우가 많습니다. 따라서 외부 데이터 원본에 액세스하는 데 사용되는 계정은 데이터 새로 고침 일정 페이지의 이 부분에 설정된 옵션에 의해 결정됩니다. 이는 PowerPivot 무인 데이터 새로 고침 계정, 개별 사용자의 Windows 계정 또는 미리 정의된 대상 응용 프로그램에 저장된 계정일 수 있습니다.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 데이터 새로 고침을 실행하는 데 사용된 계정이 데이터를 가져오는 데 사용된 계정과 다른 경우(예: PowerPivot 무인 데이터 새로 고침 계정과 자격 증명 옵션 1 또는 다른 저장된 자격 증명 집합과 자격 증명 옵션 3) 해당 계정에 대한 새 데이터베이스 로그인을 만들고 외부 데이터 원본에 대한 읽기 권한을 부여해야 합니다.  
  
 데이터에 액세스해야 하는 계정을 이해한 후에는 PowerPivot 통합 문서에서 가장 자주 사용되는 데이터 원본에 대한 사용 권한을 확인할 수 있습니다. 자주 사용되는 데이터 웨어하우스 또는 보고 데이터베이스부터 시작하되, 활성 PowerPivot 사용자의 입력을 요청하여 이들이 사용 중인 데이터 원본도 확인합니다. 데이터 원본 목록이 확보되면 하나씩 검사하여 사용 권한이 올바르게 설정되었는지 확인할 수 있습니다.  
  
##  <a name="bkmk_upgradewrkbk"></a> 7 단계: 데이터 새로 고침에 대 한 통합 문서 업그레이드 사용  
 기본적으로 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 버전의 PowerPivot for Excel을 사용하여 만든 통합 문서는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 버전의 SharePoint용 PowerPivot에서 예약된 데이터 새로 고침에 맞게 구성할 수 없습니다. SharePoint 환경에서 이후 버전 또는 이전 버전의 PowerPivot 통합 문서를 호스팅하는 경우 서버에서 자동 데이터 새로 고침을 위해 예약하려면 먼저 모든 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 통합 문서를 업그레이드해야 합니다.  
  
##  <a name="bkmk_verify"></a> 8 단계: 데이터 새로 고침 구성 확인  
 데이터 새로 고침을 확인하려면 SharePoint 사이트에 게시된 PowerPivot 통합 문서가 있어야 합니다. 또한 통합 문서에 대한 참가 권한과 데이터 새로 고침 일정에 포함된 모든 데이터 원본에 대한 액세스 권한이 있어야 합니다.  
  
 일정을 만들 때 **가능한 빨리 새로 고치십시오.** 확인란을 선택하면 데이터 새로 고침을 즉시 실행할 수 있습니다. 그런 다음 해당 통합 문서의 데이터 새로 고침 기록 페이지에서 성공적으로 실행되었는지 확인할 수 있습니다. 이전에 설명한 대로 PowerPivot 데이터 새로 고침 타이머 작업은 1분마다 실행됩니다. 이는 데이터 새로 고침이 성공했는지 확인하는 데 걸리는 최소한의 시간입니다.  
  
 지원하려는 모든 자격 증명 옵션을 시도해야 합니다. 예를 들어 PowerPivot 무인 데이터 새로 고침 계정을 구성한 경우 해당 옵션을 사용하여 데이터 새로 고침을 성공적으로 완료할 수 있는지 확인합니다. 일정 및 상태 정보를 확인 하는 방법에 대 한 자세한 내용은 참조 하세요. [데이터 새로 고침 예약 &#40;SharePoint 용 PowerPivot&#41; ](schedule-a-data-refresh-powerpivot-for-sharepoint.md) 하 고 [데이터 새로 고침 기록 보기 &#40;SharePoint 용 PowerPivot &#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 데이터 새로 고침에 실패한 경우 가능한 해결 방안에 대한 자세한 내용은 TechNet Wiki에서 [PowerPivot 데이터 새로 고침 문제 해결](http://go.microsoft.com/fwlink/?LinkID=223279) 페이지를 참조하십시오.  
  
##  <a name="bkmk_config"></a> 데이터 새로 고침에 대 한 구성 설정을 수정 합니다.  
 각 PowerPivot 서비스 응용 프로그램에는 데이터 새로 고침 작업에 영향을 주는 구성 설정이 포함됩니다. 이 섹션에서는 이러한 설정을 수정하는 방법에 대해 설명합니다.  
  
###  <a name="procIntervals"></a> 설정된 ' 업무 시간 ' 업무 시간 이후 처리를 확인 하려면  
 데이터 새로 고침 작업을 예약하는 SharePoint 사용자는 "업무 시간 이후"의 가장 빠른 시작 시간을 지정할 수 있습니다. 이렇게 하면 업무 시간에 누적되는 비즈니스 트랜잭션 데이터를 검색하려는 경우에 유용합니다. 팜 관리자는 조직의 업무 시간을 가장 정확하게 정의하는 시간 범위를 지정할 수 있습니다. 업무 시간을 오전 4시부터 오후 8시까지로 정의할 경우 "업무 시간 이후" 시작 시간을 기반으로 하는 데이터 새로 고침 처리는 오후 8시 1분에 시작됩니다.  
  
 업무 시간 이후에 실행되는 데이터 새로 고침 요청은 수신되는 순서대로 큐에 추가됩니다. 개별 요청은 서버 리소스를 사용할 수 있을 때 처리됩니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  PowerPivot 서비스 응용 프로그램 이름을 클릭합니다. PowerPivot 관리 대시보드가 나타납니다.  
  
3.  동작에서 **서비스 응용 프로그램 설정 구성** 을 클릭하여 PowerPivot 서비스 응용 프로그램 설정 페이지를 엽니다.  
  
4.  데이터 새로 고침 섹션의 업무 시간에 업무 시간 이후 처리 기간을 정의하는 시작 시간과 종료 시간을 입력합니다.  
  
     업무 시간 이후 처리 기간을 정의하지 않으려면 시작 시간과 종료 시간에 동일한 값을 입력할 수 있습니다. 예를 들어 시작 시간과 종료 시간에 모두 12:00을 입력합니다. 이 경우에도 SharePoint 사이트의 일정 정의 페이지에는 "업무 시간 이후"가 옵션으로 제공됩니다. 업무 시간 이후 처리 범위가 정의되어 있지 않은 팜에서 업무 시간 이후 옵션을 선택하면 처리 작업이 시작되지 않고 데이터 새로 고침 오류가 발생합니다.  
  
5.  **확인**을 클릭합니다.  
  
###  <a name="usagehist"></a> 데이터 새로 고침 기록이 보존 되는 기간 제한  
 데이터 새로 고침 기록은 시간에 따라 데이터 새로 고침 작업에 대해 생성되는 성공 및 실패 메시지의 세부 레코드입니다. 기록 정보는 팜에서 사용 데이터 컬렉션 시스템을 통해 수집되어 관리됩니다. 따라서 사용 데이터 기록에 대해 설정하는 제한이 데이터 새로 고침 기록에도 적용됩니다. 사용 작업 보고서는 PowerPivot 시스템 전체에서 데이터를 가져오기 때문에 수집되어 저장되는 데이터 새로 고침 기록과 모든 다른 사용 데이터에 대해 단일 기록 설정을 사용하여 데이터 보존을 제어합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  PowerPivot 서비스 응용 프로그램 이름을 클릭합니다. PowerPivot 관리 대시보드가 나타납니다.  
  
3.  동작에서 **서비스 응용 프로그램 설정 구성** 을 클릭하여 PowerPivot 서비스 응용 프로그램 설정 페이지를 엽니다.  
  
4.  사용 데이터 컬렉션 섹션의 사용 데이터 기록에 각 통합 문서에 대한 데이터 새로 고침 작업 기록을 보관할 일 수를 입력합니다.  
  
     기본값은 365일입니다. 최소값은 1일이고 최대값은 5000일입니다. 0은 보존 기간에 제한이 없음을 의미합니다. 즉, 데이터가 삭제되지 않습니다. 기록을 해제하는 설정은 없습니다.  
  
5.  **확인**을 클릭합니다.  
  
 SharePoint 사용자가 데이터 새로 고침 기록이 있는 통합 문서에서 데이터 새로 고침 관리 옵션을 선택하면 기록 정보가 제공됩니다. 팜 관리자가 PowerPivot 서비스 작업을 관리하는 데 사용되는 PowerPivot 관리 대시보드에서도 이 정보가 사용됩니다. 자세한 내용은 [데이터 새로 고침 기록 보기 &#40;SharePoint 용 PowerPivot&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)합니다.  
  
 기록 데이터의 장기적인 실제 저장소는 PowerPivot 서비스 응용 프로그램의 PowerPivot 서비스 응용 프로그램 데이터베이스에 있습니다. 사용 현황 데이터 수집 및 저장 하는 방법에 대 한 자세한 내용은 참조 하세요. [PowerPivot 사용 현황 데이터 수집](power-pivot-sharepoint/power-pivot-usage-data-collection.md)합니다.  
  
##  <a name="configTimerJob"></a> PowerPivot 데이터 새로 고침 타이머 작업 다시 예약  
 예약된 데이터 새로 고침은 PowerPivot 서비스 응용 프로그램 데이터베이스에서 1분 간격으로 예약 정보를 검사하는 PowerPivot 데이터 새로 고침 타이머 작업에 의해 트리거됩니다. 데이터 새로 고침을 시작하도록 예약된 시간에 타이머 작업은 사용 가능한 PowerPivot 서버의 처리 큐에 요청을 추가합니다.  
  
 성능 튜닝을 위해 검사 간격을 늘릴 수 있습니다. 또한 문제를 해결하는 동안 데이터 새로 고침 작업을 일시적으로 중지하도록 타이머 작업을 해제할 수 있습니다.  
  
 기본 설정은 1분이며, 지정할 수 있는 최소값입니다. 이 값은 임의의 시간에 실행되는 일정에 대해 가장 예측 가능한 결과를 제공하므로 이 값을 사용하는 것이 좋습니다. 예를 들어 사용자가 오후 4시 15분에 데이터 새로 고침을 예약하고 타이머 작업에서 1분 간격으로 일정을 검색한다면, 예약된 데이터 새로 고침 요청이 4시 15분에 검색되고 4시 15분부터 몇 분 이내에 처리가 시작됩니다.  
  
 아주 가끔씩 실행하도록 검색 간격을 늘릴 경우(예: 자정에 한 번) 해당 간격에 실행하도록 예약된 모든 데이터 새로 고침 작업이 처리 큐에 한 번에 추가되어 서버 성능이 저하되고 다른 응용 프로그램이 시스템 리소스를 사용하지 못하게 될 수도 있습니다. 예약된 새로 고침 작업 수에 따라 데이터 새로 고침 작업에 대한 처리 큐가 그만큼 커져 일부 작업을 완료하지 못할 수도 있습니다. 큐의 끝에 있는 데이터 새로 고침 요청은 다음 처리 간격으로 넘어가는 경우 삭제될 수 있습니다.  
  
 하드웨어에서 지원 가능한 경우 더 많은 데이터 새로 고침 작업을 병렬로 실행할 수 있도록 추가 프로세서를 지정하여 이 문제를 줄일 수 있습니다. 자세한 내용은 [Query-Only 처리 또는 구성 전용 데이터 새로 고침 &#40;SharePoint 용 PowerPivot&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)합니다. 데이터 새로 고침 요청은 검색, 큐에 추가 및 처리 하는 방법에 대 한 자세한 내용은 참조 하세요. [PowerPivot 데이터 새로 고침](power-pivot-sharepoint/power-pivot-data-refresh.md)합니다.  
  
1.  중앙 관리에서 **모니터링**을 클릭합니다.  
  
2.  **작업 정의 검토**를 클릭합니다.  
  
3.  **PowerPivot 데이터 새로 고침 타이머 작업**을 선택합니다.  
  
4.  일정 빈도를 수정하여 타이머 작업에서 데이터 새로 고침 일정 정보를 검색하는 빈도를 변경할 수 있습니다.  
  
##  <a name="bkmk_disableDR"></a> 데이터 새로 고침 타이머 작업을 사용 하지 않도록 설정  
 PowerPivot 데이터 새로 고침 타이머 작업은 팜의 모든 PowerPivot 서버 인스턴스에 대해 설정되거나 해제되는 팜 수준 타이머 작업입니다. 이 작업은 특정 웹 응용 프로그램이나 PowerPivot 서비스 응용 프로그램에 연결되지 않습니다. 팜의 일부 서버에서만 데이터 새로 고침을 강제로 처리하기 위해 일부 서버에서 작업을 해제할 수 없습니다.  
  
 PowerPivot 데이터 새로 고침 타이머 작업을 해제하는 경우 큐에 이미 있던 요청은 처리되지만 새 요청은 작업을 사용하도록 다시 설정할 때까지 추가되지 않습니다. 과거 시간에 발생하도록 예약된 요청은 처리되지 않습니다.  
  
 타이머 작업을 해제해도 응용 프로그램 페이지의 기능 가용성에는 영향을 주지 않습니다. 웹 응용 프로그램에서 데이터 새로 고침 기능을 제거하거나 숨길 수 없습니다. 참가 권한 이상의 권한이 있는 사용자는 타이머 작업을 영구히 해제하더라도 데이터 새로 고침 작업에 대한 새 일정을 계속해서 만들 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 새로 고침 예약 &#40;SharePoint 용 PowerPivot&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [전용된 데이터 새로 고침 또는 쿼리만 처리 구성 &#40;SharePoint 용 PowerPivot&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)   
 [구성 PowerPivot 무인된 데이터 새로 고침 계정 &#40;SharePoint 용 PowerPivot&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [PowerPivot 데이터 새로 고침에 대 한 저장 된 자격 증명 구성 &#40;SharePoint 용 PowerPivot&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
