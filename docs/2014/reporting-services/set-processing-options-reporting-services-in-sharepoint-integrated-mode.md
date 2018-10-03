---
title: 처리 옵션 (SharePoint 통합된 모드의 Reporting Services) 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- snapshots [Reporting Services], creating
ms.assetid: 453b19a1-739a-4b67-aeea-2069b52204e1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 72089aad9a38c488b36fdb65cc94060d70c6482c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104763"
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>처리 옵션 설정(SharePoint 통합 모드의 Reporting Services)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 처리 옵션을 설정하여 데이터 처리 시기를 결정할 수 있습니다. 현재 보고서에 대해 보고서 기록을 사용할지 여부를 결정하는 옵션과 보고서 처리의 제한 시간 값을 설정할 수도 있습니다.  
  
-   보고서를 보고서 스냅숏으로 실행하면 임의의 시간에(예: 예약된 백업 시간 동안) 보고서가 실행되지 않도록 할 수 있습니다. 보고서 스냅숏은 일반적으로 일정에 따라 생성되고 이후에 새로 고쳐지므로 보고서 및 데이터 처리 시간을 정확하게 예약할 수 있습니다. 실행하는 데 시간이 오래 걸리는 쿼리 또는 특정 시간 동안 누구도 액세스할 수 없는 데이터 원본의 데이터를 사용하는 쿼리를 기반으로 하는 보고서의 경우 보고서를 스냅숏으로 실행해야 합니다.  
  
-   보고서 서버는 처리된 보고서의 복사본을 캐시했다가 사용자가 보고서를 열면 해당 복사본을 반환할 수 있습니다. 캐싱은 성능을 향상시키는 기술입니다. 캐싱은 보고서가 크거나 자주 액세스되는 경우 보고서를 검색하는 데 필요한 시간을 단축시킬 수 있습니다.  
  
-   보고서 기록은 이전에 실행한 보고서 복사본의 모음입니다. 보고서 기록을 사용하여 시간에 따른 보고서 기록을 유지 관리할 수 있습니다. 보고서 기록은 기밀이나 개인 데이터가 포함된 보고서에 대해서는 사용할 수 없습니다. 따라서 보고서 기록에는 보고서를 실행하는 모든 사용자가 사용할 수 있는 단일 자격 증명 집합(저장된 자격 증명 또는 무인 모드의 보고서 실행에 사용되는 자격 증명)을 사용하여 데이터 원본을 쿼리하는 보고서만 포함될 수 있습니다.  
  
    > [!NOTE]  
    >  SharePoint와의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 통합에서는 SharePoint의 체크 아웃 및 체크인 콘텐츠 관리 기능을 사용하여 업데이트를 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 콘텐츠 형식에 저장합니다. 여기에는 보고서 스냅샷 만들기도 포함됩니다. 따라서 문서 라이브러리에 대한 버전 관리를 사용하는 경우 새 보고서 기록 스냅샷이 만들어질 때 보고서 버전이 업데이트되는 것을 볼 수 있습니다. 이것은 스냅샷 업데이트로 인해 파생되는 작업입니다. 스냅샷이 업데이트될 때 보고서의 LastExecution 속성이 변경되므로 보고서 버전이 변경되는 것입니다.  
  
-   제한 시간 값을 지정하여 시스템 리소스 사용 방식에 대해 제한을 설정할 수 있습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
 **항목 내용**  
  
-   [데이터 새로 고침 옵션을 설정하려면](#bkmk_set_data_refresh)  
  
-   [보고서 캐시 옵션을 설정하려면](#bkmk_set_report_caching)  
  
-   [처리 제한 시간 값을 설정하려면](#bkmk_set_processing)  
  
-   [보고서 기록 옵션 및 제한을 설정하려면](#bkmk_set_report_history)  
  
-   [데이터베이스 제한 시간 설정](#bkmk_set_database_timeout)  
  
##  <a name="bkmk_set_data_refresh"></a> 데이터 새로 고침 옵션을 설정하려면  
  
1.  라이브러리의 보고서를 가리킵니다.  
  
2.  아래쪽 화살표를 클릭하고 **처리 옵션 관리**를 선택합니다.  
  
3.  **데이터 새로 고침 옵션**에서 **스냅숏 데이터 사용**을 클릭합니다. "데이터 원본 자격 증명 중 하나 이상이 저장되어 있지 않으므로 스냅숏에서 이 보고서를 실행할 수 없습니다"가 표시되는 경우 보고서가 무인 모드로 실행되도록 구성되어 있지 않으며 이 옵션을 설정하기 전에 저장된 자격 증명을 사용하도록 데이터 원본을 수정해야 합니다.  
  
4.  **데이터 스냅숏 옵션**에서 **데이터 처리 예약**을 선택합니다.  
  
5.  사용할 기존 공유 일정이 있는 경우 **공유 일정** 을 선택하고, 없으면 **사용자 지정 일정**을 클릭한 다음 **구성**을 클릭합니다.  
  
6.  빈도, 일정, 시작 날짜 및 종료 날짜를 선택하고 **확인**을 클릭합니다.  
  
7.  예약된 데이터 처리가 수행될 때까지 기다리지 않고 보고서에 사용할 스냅숏 데이터를 즉시 만들려면 **데이터 스냅숏 옵션**에서 **이 페이지를 저장할 때 스냅숏 만들기 또는 업데이트** 를 선택합니다.  
  
##  <a name="bkmk_set_report_caching"></a> 보고서 캐시 옵션을 설정하려면  
  
1.  라이브러리의 보고서를 가리킵니다.  
  
2.  아래쪽 화살표를 클릭하고 **처리 옵션 관리**를 선택합니다.  
  
3.  **데이터 새로 고침 옵션**에서 **캐시된 데이터 사용**을 클릭합니다. "데이터 원본 자격 증명 중 하나 이상이 저장되어 있지 않으므로 이 보고서를 캐시할 수 없습니다"가 표시되는 경우 보고서가 무인 모드로 실행되도록 구성되어 있지 않으며 이 옵션을 설정하기 전에 저장된 자격 증명을 사용하도록 데이터 원본을 수정해야 합니다.  
  
4.  **캐시 옵션**에서 캐시 만료 방식을 지정합니다.  
  
    -   캐시가 만료되기까지의 시간(분)을 입력합니다.  
  
    -   일정에 지정된 시간에 캐시를 지우려면 공유 일정을 사용합니다.  
  
    -   사용자가 지정한 시간에 캐시를 지우려면 사용자 지정 일정을 만듭니다.  
  
##  <a name="bkmk_set_processing"></a> 처리 제한 시간 값을 설정하려면  
  
1.  라이브러리의 보고서를 가리킵니다.  
  
2.  아래쪽 화살표를 클릭하고 **처리 옵션 관리**를 선택합니다.  
  
3.  보고서 서버 수준에서 지정된 값을 사용하려면 **처리 제한 시간**에서 **사이트 기본 설정 사용** 을 선택합니다. 제한 시간 없음이나 다른 제한 시간 값으로 해당 값을 재정의하려면 **보고서 처리 시간 제한 없음** 또는 **보고서 처리 제한 시간(초)** 을 선택합니다.  
  
##  <a name="bkmk_set_report_history"></a> 보고서 기록 옵션 및 제한을 설정하려면  
  
1.  라이브러리의 보고서를 가리킵니다.  
  
2.  아래쪽 화살표를 클릭하고 **처리 옵션 관리**를 선택합니다.  
  
3.  **기록 스냅숏 옵션**에서 데이터 처리 및 저장 방법과 시기를 지정합니다.  
  
4.  보고서 서버 수준에서 지정된 값을 사용하려면 **기록 스냅숏 제한**에서 **사이트 기본 설정 사용** 을 선택합니다. 지정된 값을 사용하지 않으려면 **스냅숏 수를 제한하지 않음** 또는 **스냅숏 수 제한** 을 선택합니다.  
  
##  <a name="bkmk_set_database_timeout"></a> 데이터베이스 제한 시간 설정  
  
1.  Windows PowerShell을 사용하여 SharePoint 보고서 서버의 데이터베이스 제한 시간을 설정합니다. 자세한 내용은 가져오기 및 보고 서비스 응용 프로그램 데이터베이스의 속성 설정 "을 참조 하십시오. 부분 [Reporting Services SharePoint 모드용 PowerShell cmdlet](../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 처리 속성 설정](report-server/set-report-processing-properties.md)   
 [보고서 캐시&#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [보고서 및 공유 데이터 집합 처리에 대 한 제한 시간 값 설정 &#40;SSRS&#41;](report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
  
  
