---
title: PowerPivot 상태 규칙-구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a01e63e6-97dc-43e5-ad12-ae6580afc606
author: minewiskan
ms.author: owend
ms.openlocfilehash: 216721a187d86e56154d5d25c5e3174d231f7f36
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547545"
---
# <a name="powerpivot-health-rules---configure"></a>PowerPivot 상태 규칙 - 구성
  SharePoint용 PowerPivot에는 서버 가용성과 구성 문제를 모니터링하고 해결하는 데 유용한 SharePoint 상태 규칙이 포함되어 있습니다. SharePoint용 PowerPivot에 적용되는 상태 규칙은 규칙 정의 검토 페이지에 나타납니다.  
  
 상태 규칙을 통해 서비스가 중단될 수 있는 서버 문제를 조기에 감지할 수 있습니다. SharePoint용 PowerPivot에서는 사용자가 영향을 받기 전에 문제를 식별하고 수정할 수 있도록 도와 주는 여러 가지 규칙을 제공합니다. 사용자 배포 환경의 고유한 특징에 맞도록 이러한 규칙을 사용자 지정할 수 있습니다. 예를 들어, 디스크 공간에 대한 경고를 해결하는 데 시간이 더 필요한 경우 사용 가능한 디스크 공간 백분율을 5%에서 10%로 늘려 경고를 더 일찍 받을 수 있습니다.  
  
 사용자 지정할 수 있는 규칙은 리소스 소비 또는 서버 가용성에 대해 보고하는 규칙입니다. 기본 시스템 용량은 서버와 배포 토폴로지에 따라 매우 다양하기 때문에 이러한 영역에서는 사용자 지정이 도움이 될 수 있습니다. 반면 서버 구성 또는 보안 문제를 식별하는 규칙에 대해서는 사용자 지정을 사용할 수 없습니다. 이러한 규칙은 모든 설치에 일관되게 적용되어야 합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124; SharePoint 2010|  
  
 **참고:** 상태 규칙 설정은 SQL Server Analysis Services 인스턴스와 PowerPivot 서비스 애플리케이션에 대해 별도로 구성됩니다. 이 항목의 지침을 사용하여 각 서비스에 대한 상태 규칙을 구성할 수 있습니다. SharePoint 2013 배포의 경우 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 는 서비스 애플리케이션만 사용합니다. 따라서 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 에서는 다른 버전의 다른 SharePoint 상태 규칙 집합을 설치합니다. [상태 규칙 참조 &#40;SharePoint용 PowerPivot&#41;](health-rules-reference-power-pivot-for-sharepoint.md)항목에서 "버전" 열을 참조 하거나 다음 Windows PowerShell 명령을 실행 하 여 설치 된 규칙을 확인할 수 있습니다.  
  
```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default  
```  
  
 **항목 내용**  
  
 [PowerPivot 상태 규칙 보기](#bkmk_view)  
  
 [서버 안정성을 평가하는 데 사용되는 상태 규칙 구성(SQL Server Analysis Services)](#bkmk_HR_SSAS)  
  
 [애플리케이션 안정성을 평가하는 데 사용되는 상태 규칙 구성(PowerPivot 서비스 애플리케이션)](#bkmk_evaluate_application_stability)  
  
## <a name="prerequisites"></a>사전 요구 사항  
 Analysis Services 인스턴스 및 PowerPivot 서비스 애플리케이션의 구성 속성을 변경하려면 서비스 애플리케이션 관리자여야 합니다.  
  
##  <a name="view-powerpivot-health-rules"></a><a name="bkmk_view"></a>PowerPivot 상태 규칙 보기  
  
1.  SharePoint 중앙 관리에서 **모니터링**을 클릭하고 **상태 분석기** 섹션에서 **규칙 정의 검토**를 클릭합니다.  
  
2.  구성 섹션에서 **PowerPivot:** 접두사로 시작하는 규칙을 찾습니다. PowerPivot 관련 상태 규칙은 기본 제공 SharePoint 규칙과 구별할 수 있도록 모두 이 접두사로 시작됩니다.  
  
 문제가 감지되면 이러한 규칙은 **문제 및 솔루션 검토** 페이지에 나타납니다.  
  
 즉시 조사해야 할 문제가 의심되는 경우 규칙 확인을 수동으로 실행하여 문제가 있는지 확인할 수 있습니다.  
  
 이렇게 하려면 규칙을 클릭하여 해당 규칙 정의를 연 다음 리본에서 **지금 실행** 을 클릭합니다. **닫기** 를 클릭하여 **문제 및 솔루션 검토** 페이지로 돌아가 보고서를 확인합니다. 규칙에서 문제를 감지한 경우 경고 또는 오류가 페이지에 보고됩니다. 경우에 따라 오류나 경고가 표시되는 데 몇 분 정도 걸릴 수 있습니다.  
  
##  <a name="configure-health-rules-used-to-evaluate-server-stability-sql-server-analysis-services"></a><a name="bkmk_HR_SSAS"></a>서버 안정성을 평가 하는 데 사용 되는 상태 규칙 구성 (SQL Server Analysis Services)  
 Analysis Services 인스턴스에는 시스템 수준의 문제(캐시용 CPU, 메모리 및 디스크 공간)를 감지하는 상태 규칙이 포함되어 있습니다. 다음 지침을 사용하여 특정 상태 규칙을 트리거하는 임계값을 수정할 수 있습니다.  
  
1.  SharePoint 중앙 관리의 **시스템 설정** 섹션에서 **서버의 서비스 관리**를 클릭합니다.  
  
2.  페이지 맨 위에서 Analysis Services 인스턴스가 있는 SharePoint 팜의 서버(다음 그림의 경우 서버 이름은 AW-SRV033)를 선택합니다. **SQL Server Analysis Services** 가 서비스 목록에 나타납니다.  
  
     ![서버에서 서비스 관리 페이지의 스크린 샷](../media/ssas-centraladmin-servicesonserver.gif "서버에서 서비스 관리 페이지의 스크린 샷")  
  
3.  **SQL Server Analysis Services**를 클릭합니다.  
  
4.  서비스 속성 페이지의 상태 규칙 설정에서 다음 설정을 수정합니다.  
  
     CPU 리소스 할당 부족(기본값: 80%)  
     이 상태 규칙은 Analysis Services 서버 프로세스(msmdsrv.exe)에서 사용하는 CPU 리소스가 데이터 컬렉션 간격 설정을 통해 지정된 대로 4시간 이상 80% 또는 80% 위로 유지되는 경우에 트리거됩니다.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: Analysis Services에는 요청한 작업을 수행할 수 있는 충분한 CPU 리소스가 없습니다.** 규칙 정의에 해당합니다.  
  
     시스템의 CPU 리소스 부족(기본값: 90%)  
     이 상태 규칙은 서버의 CPU 리소스가 데이터 컬렉션 간격 설정을 통해 지정된 대로 4시간 이상 90% 또는 90% 위로 유지되는 경우에 트리거됩니다. 전체 CPU 사용률은 CPU 사용량을 서버 상태의 측정값으로 모니터링하는 상태 기반 부하 분산 알고리즘의 일부로 측정됩니다.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: 전체 CPU 사용량이 너무 많습니다.** 규칙 정의에 해당합니다.  
  
     메모리 임계값 부족(기본값: 5%)  
     SharePoint 애플리케이션 서버에서 SQL Server Analysis Services 인스턴스는 항상 소량의 사용되지 않는 메모리를 가지고 있어야 합니다. 서버 작업은 대부분 메모리 집중형이기 때문에 서버는 최대 한도까지 실행되지 않을 때 최상의 성능을 발휘합니다. 5%의 사용되지 않는 메모리는 Analysis  Services에 할당된 메모리의 백분율로 계산됩니다. 예를 들어 총 메모리가 200GB이고 Analysis  Services에 80%(160GB)가 할당된 경우 5%의 사용되지 않는 메모리는 160GB의 5%인 8GB입니다.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: Analysis Services에는 요청한 작업을 수행할 수 있는 충분한 메모리가 없습니다.** 규칙 정의에 해당합니다.  
  
     최대 연결 수(기본값: 100)  
     이 상태 규칙은 Analysis Services 인스턴스에 대한 연결 수가 데이터 컬렉션 간격 설정을 통해 지정된 대로 4시간 이상 100개 연결 또는 100개 연결 위로 유지되는 경우에 트리거됩니다. 이 기본값은 서버의 하드웨어 사양 또는 사용자 작업을 기반으로 하지 않고 임의로 지정되므로 사용자 환경의 서버 용량 및 사용자 작업에 따라 값을 높이거나 낮출 수 있습니다.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: 연결 수가 크므로 현재 로드를 처리하기 위해 서버를 더 많이 배포해야 합니다.** 규칙 정의에 해당합니다.  
  
     디스크 공간 부족(기본값: 5%)  
     디스크 공간은 데이터베이스가 요청될 때마다 PowerPivot 데이터를 캐시하는 데 사용됩니다. 이 규칙을 사용하여 디스크 공간이 부족한 때를 알 수 있습니다. 기본적으로 이 상태 규칙은 백업 폴더가 있는 디스크 드라이브의 디스크 공간이 5%  미만일 때 트리거됩니다. 디스크 사용에 대 한 자세한 내용은 [디스크 공간 사용 &#40;구성 SharePoint용 PowerPivot&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)을 참조 하십시오.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: PowerPivot 데이터가 캐시된 드라이브의 디스크 공간이 부족합니다.** 규칙 정의에 해당합니다.  
  
     데이터 컬렉션 간격(시간)  
     상태 규칙을 트리거하는 데 사용되는 숫자를 계산하는 데이터 컬렉션 기간을 지정할 수 있습니다. 시스템이 일관성 있게 모니터링되는 경우에도 상태 규칙 경고를 트리거하는 데 사용되는 임계값은 미리 정의된 간격으로 생성된 데이터를 사용하여 계산됩니다. 기본 간격은 4시간입니다. 서버에서는 이전 4시간 동안 수집된 시스템 및 사용량 현황 데이터를 검색하여 사용자 연결 수, 디스크 공간 사용, CPU 및 메모리 사용률을 평가합니다.  
  
##  <a name="configure-health-rules-used-to-evaluate-application-stability-powerpivot-service-application"></a><a name="bkmk_evaluate_application_stability"></a>응용 프로그램 안정성을 평가 하는 데 사용 되는 상태 규칙 구성 (PowerPivot 서비스 응용 프로그램)  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  서비스 애플리케이션 페이지에서 **기본 PowerPivot 서비스 애플리케이션**을 클릭합니다.  
  
     ![ManageService 응용 프로그램 페이지의 스크린 샷](../media/ssas-centraladmin-app.gif "ManageService 응용 프로그램 페이지의 스크린 샷")  
  
3.  PowerPivot 관리 대시보드가 나타납니다. **동작** 목록에서 **서비스 애플리케이션 설정 구성** 을 클릭하여 서비스 애플리케이션 설정 페이지를 엽니다.  
  
     ![동작 목록에 포커스가 있는 대시보드의 스크린 샷](../media/ssas-centraladmin-actionslist.gif "동작 목록에 포커스가 있는 대시보드의 스크린 샷")  
  
4.  상태 규칙 설정에서 다음 설정을 수정합니다.  
  
     로드 대 연결 비율(기본값: 20%)  
     이 상태 규칙은 로드 이벤트 수가 연결 이벤트 수보다 큰 경우 트리거됩니다. 이러한 경우는 서버가 데이터베이스를 너무 빠르게 언로드하거나 캐시 감소 설정이 너무 가파를 때 발생할 수 있습니다.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: 연결에 대한 로드 이벤트의 비율이 너무 높습니다.** 규칙 정의에 해당합니다.  
  
     데이터 컬렉션 간격(기본값: 4시간)  
     상태 규칙을 트리거하는 데 사용되는 숫자를 계산하는 데이터 컬렉션 기간을 지정할 수 있습니다. 시스템이 일관성 있게 모니터링되는 경우에도 상태 규칙 경고를 트리거하는 데 사용되는 임계값은 미리 정의된 간격으로 생성된 데이터를 사용하여 계산됩니다. 기본 간격은 4시간입니다. 서버에서는 이전 4시간 동안 수집된 시스템 및 사용량 현황 데이터를 검색하여 로드 대 수집 비율을 평가합니다.  
  
     PowerPivot Management Dashboard.xlsx에 대한 업데이트 확인(기본값: 5일)  
     PowerPivot Management Dashboard.xlsx 파일은 PowerPivot 관리 대시보드의 보고서에 사용되는 데이터 원본입니다. 기본 서버 구성에서 .xlsx 파일은 SharePoint 및 PowerPivot 시스템 서비스에 수집한 사용량 현황 데이터를 사용하여 매일 새로 고쳐집니다. 파일이 업데이트되지 않은 경우에는 상태 규칙에서 이를 문제로 보고합니다. 기본적으로 규칙은 파일의 타임스탬프가 5일 동안 변경되지 않은 경우에 트리거됩니다.  
  
     사용 현황 데이터 수집에 대 한 자세한 내용은 [&#40;SharePoint용 PowerPivot에 대 한 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 참조 하세요.  
  
     이 구성 설정은 **문제 및 솔루션 검토** 페이지의 **PowerPivot: 사용량 현황 데이터가 예상된 빈도로 업데이트되지 않습니다.** 규칙 정의에 해당합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint용 PowerPivot&#41;디스크 공간 사용 &#40;구성](configure-disk-space-usage-power-pivot-for-sharepoint.md)   
 [PowerPivot 관리 대시보드 및 사용량 현황 데이터](power-pivot-management-dashboard-and-usage-data.md)  
