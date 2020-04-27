---
title: PowerPivot 사용 현황 데이터 수집 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46504906b13323ac4881ca2289e87e31f1cea72f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071085"
---
# <a name="powerpivot-usage-data-collection"></a>PowerPivot 사용량 현황 데이터 컬렉션
  사용량 현황 데이터 컬렉션은 팜 수준의 SharePoint 기능입니다. SharePoint용 PowerPivot은 이 시스템을 사용하고 확장하여 PowerPivot 관리 대시보드에서 PowerPivot 데이터 및 서비스 사용 상태를 보여 주는 보고서를 제공합니다. SharePoint를 구성한 방법에 따라 팜에 대해 사용량 현황 데이터 컬렉션이 해제될 수 있습니다. 팜 관리자는 PowerPivot 관리 대시보드에 표시되는 사용량 현황 데이터를 만들기 위해 사용 현황 로깅을 설정해야 합니다. PowerPivot 이벤트에 대 한 사용 현황 데이터 수집을 사용 하도록 설정 하 고 구성 하는 방법에 대 한 자세한 내용은 [&#40;SharePoint용 PowerPivot 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 참조 하세요.  
  
 PowerPivot 관리 대시보드의 사용 데이터에 대한 자세한 내용을 [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)를 참조하십시오.  
  
 **항목 내용**  
  
 [사용 데이터 수집 및 보고 아키텍처](#usagearch)  
  
 [사용 현황 데이터의 원본](#sources)  
  
 [서비스 및 타이머 작업](#servicesjobs)  
  
 [사용 현황 데이터에 대 한 보고](#reporting)  
  
##  <a name="usage-data-collection-and-reporting-architecture"></a><a name="usagearch"></a> 사용량 현황 데이터 수집 및 보고 아키텍처  
 PowerPivot 사용량 현황 데이터는 SharePoint 인프라와 PowerPivot 서버 구성 요소의 기능 조합을 사용하여 수집, 저장 및 관리됩니다. SharePoint 인프라는 중앙 집중식 사용 서비스 및 기본 제공 타이머 작업을 제공합니다. SharePoint용 PowerPivot은 SharePoint 중앙 관리에 표시되는 PowerPivot 사용량 현황 데이터 및 보고서에 대한 장기 스토리지를 추가합니다.  
  
 사용량 현황 데이터 수집 시스템에서 이벤트 정보는 애플리케이션 서버나 웹 프런트 엔드의 사용 수집 시스템에 입력됩니다. 사용량 현황 데이터는 물리적 서버의 임시 데이터 파일에서 데이터베이스 서버의 영구 스토리지로 데이터를 이동하게 하는 타이머 작업에 응답하여 시스템을 통해 이동됩니다. 다음 다이어그램은 데이터 컬렉션 및 보고 시스템을 통해 사용량 현황 데이터를 이동하는 구성 요소와 프로세스를 보여 줍니다.  
  
 **참고:** 사용량 현황 데이터 컬렉션이 설정되었는지 확인합니다. 확인하려면 SharePoint 중앙 관리에서 **모니터링** 으로 이동합니다. 자세한 내용은 [&#40;SharePoint용 PowerPivot에 대 한 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 참조 하세요.  
  
 ![사용 데이터 컬렉션의 구성 요소 및 프로세스](../media/gmni-usagedata.gif "사용 데이터 컬렉션의 구성 요소 및 프로세스")  
  
|단계|설명|  
|-----------|-----------------|  
|1|사용량 현황 데이터 컬렉션은 SharePoint 배포의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 공급자와 PowerPivot 구성 요소가 생성하는 이벤트에 의해 트리거됩니다. 설정하거나 해제할 수 있는 구성 가능 이벤트에는 연결 요청, 로드 및 언로드 요청, 쿼리 응답 타이밍 이벤트가 포함되며 이들은 애플리케이션 서버에서 PowerPivot 서비스에 의해 모니터링됩니다. 다른 이벤트는 서버에서만 관리되며 해제할 수 없습니다. 여기에는 데이터 새로 고침 및 서버 상태 이벤트가 포함됩니다.<br /><br /> 처음에 사용량 현황 데이터는 SharePoint 시스템의 데이터 컬렉션 기능을 사용하여 논리 로그 파일에 수집되고 저장됩니다. 파일과 해당 위치는 SharePoint의 표준 사용량 현황 데이터 컬렉션 시스템의 일부입니다. 파일의 위치는 팜에 있는 모든 서버에서 동일합니다. 로깅 디렉터리의 위치를 보거나 변경하려면 SharePoint 중앙 관리에서 **모니터링** 으로 이동하고 **Usage and Health Data Collection 구성**을 클릭합니다.|  
|2|Microsoft SharePoint Foundation 사용량 현황 데이터 가져오기 타이머 작업은 예약된 간격(기본적으로 1시간 간격)으로 사용량 현황 데이터를 로컬 파일에서 PowerPivot 서비스 애플리케이션 데이터베이스로 이동합니다. 팜에 PowerPivot 서비스 애플리케이션이 여러 개 있을 경우 애플리케이션마다 고유한 데이터베이스가 있습니다. 이벤트에는 해당 이벤트를 생성한 PowerPivot 서비스 애플리케이션을 식별하는 내부 정보가 포함되어 있습니다. 애플리케이션 식별자를 통해 사용량 현황 데이터가 해당 데이터를 생성한 애플리케이션에 바인딩됩니다.|  
|3|중앙 관리의 PowerPivot 관리 대시보드에서 사용할 수 있는 내부 보고 데이터베이스에 데이터가 복사됩니다.|  
|4|데이터 원본은 Excel에서 사용자 지정 보고서를 만들기 위해 액세스할 수 있는 PowerPivot 통합 문서입니다. 원본 통합 문서의 인스턴스는 하나뿐입니다. 지역화된 보고서는 모두 동일한 원본 통합 문서를 기반으로 합니다.|  
|5|사용량 현황 데이터는 서버 성능 및 가용성을 담당하는 관리자를 위한 PowerPivot 서비스 애플리케이션의 보고서에 표시됩니다. 통합 문서의 지역화된 인스턴스는 지원되는 SharePoint 언어에 대해 생성됩니다.<br /><br /> 자세한 내용은 이 항목에서 [사용량 현황 데이터에 대한 보고](#reporting) 를 참조하십시오.|  
  
##  <a name="sources-of-usage-data"></a><a name="sources"></a> 사용량 현황 데이터의 원본  
 사용량 현황 데이터 수집이 사용되면 다음 서버 이벤트에 대한 데이터가 생성됩니다.  
  
|이벤트|설명|구성 가능 여부|  
|-----------|-----------------|------------------|  
|Connections|Excel 통합 문서에서 PowerPivot 데이터를 쿼리하는 사용자를 위해 서버 연결이 설정됩니다. 연결 이벤트는 PowerPivot 통합 문서에 대한 연결을 연 사용자를 식별합니다. 보고서에서 이 정보는 자주 사용하는 사용자, 동일한 사용자가 액세스하는 PowerPivot 데이터 원본 및 시간별 연결 추세를 식별하는 데 사용됩니다.|[&#40;SharePoint용 PowerPivot에 대해 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.|  
|쿼리 응답 시간|완료하는 데 걸리는 시간을 기준으로 쿼리를 범주화하는 쿼리 응답 통계입니다. 쿼리 응답 통계는 서버가 쿼리 요청에 응답하는 데 걸리는 시간의 패턴을 보여 줍니다.|[&#40;SharePoint용 PowerPivot에 대해 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.|  
|데이터 로드|[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]의 데이터 로드 작업입니다. 데이터 로드 이벤트는 가장 자주 사용되는 데이터 원본을 식별합니다.|[&#40;SharePoint용 PowerPivot에 대해 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.|  
|데이터 언로드|PowerPivot 서비스 애플리케이션의 데이터 언로드 작업입니다. [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 는 사용 중이 아니거나, 서버에 메모리가 부족하거나, 데이터 새로 고침 작업을 실행할 추가 메모리가 필요한 경우 비활성 PowerPivot 데이터 원본을 언로드합니다.|[&#40;SharePoint용 PowerPivot에 대해 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)을 사용 하거나 사용 하지 않도록 설정할 수 있습니다.|  
|서버 상태|CPU와 메모리 사용률로 측정한 서버 상태를 나타내는 서버 작업입니다. 이 데이터는 기록 데이터이며, 서버의 현재 처리 로드에 대한 실시간 정보를 제공하지 않습니다.|아니요. 이 이벤트에 대해 사용량 현황 데이터가 항상 수집됩니다.|  
|데이터 새로 고침|예약된 데이터 업데이트를 위해 PowerPivot 서비스에서 시작된 데이터 새로 고침 작업입니다. 데이터 새로 고침에 대한 사용 기록은 작업 보고서에 대해 애플리케이션 수준에서 수집되고, 개별 통합 문서에 대해 데이터 새로 고침 관리 페이지에 반영됩니다.<br /><br /> **참고:**[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 및 SharePoint 2013 배포의 경우 Analysis Services Server가 아닌 Excel Services로 데이터 새로 고침이 관리됩니다.|아니요. PowerPivot 서비스 애플리케이션에 대해 데이터 새로 고침을 사용하는 경우 데이터 새로 고침 사용량 현황 데이터가 항상 수집됩니다.|  
  
##  <a name="services-and-timer-jobs"></a><a name="servicesjobs"></a> 서비스 및 타이머 작업  
 다음 표에서는 사용량 현황 데이터 수집 시스템의 서비스 및 데이터 수집 저장소에 대해 설명합니다. PowerPivot 관리 대시보드 보고서에서 서버 상태 및 사용 현황 데이터의 데이터를 강제로 새로 고치는 타이머 작업 일정을 재정의 하는 방법에 대 한 지침은 [SharePoint 2010를 사용 하 여 Powerpivot 데이터 새로 고침](../powerpivot-data-refresh-with-sharepoint-2010.md)을 참조 하세요. SharePoint 중앙 관리에서 타이머 작업을 볼 수 있습니다. **모니터링**으로 이동하고 **작업 상태 확인**을 클릭합니다. **작업 정의 검토**를 클릭 합니다.  
  
|구성 요소|기본 일정|설명|  
|---------------|----------------------|-----------------|  
|SharePoint Timer Service(SPTimerV4)||Windows 서비스는 팜의 모든 멤버 컴퓨터에서 로컬로 실행되며 팜 수준에서 정의된 모든 타이머 작업을 처리합니다.|  
|Microsoft SharePoint Foundation 사용 데이터 가져오기(Microsoft SharePoint Foundation Usage Data Import)|SharePoint 2010에서 30분마다 SharePoint 2013에서 5분마다|이 타이머 작업은 팜 수준에서 전역적으로 구성되며, 로컬 사용 현황 로그 파일에서 중앙 사용량 현황 데이터 컬렉션 데이터베이스로 사용량 현황 데이터를 이동합니다. 데이터 가져오기 작업을 실행하기 위해 이 타이머 작업을 수동으로 실행할 수 있습니다.|  
|Microsoft SharePoint Foundation 사용량 현황 데이터 처리 타이머 작업|매일 오전 3시|**(\*)** SQL Server 2012 SharePoint용 PowerPivot부터이 시간 작업은 이전 사용 데이터가 아직 SharePoint 사용 데이터베이스에 있는 업그레이드 또는 마이그레이션 시나리오에 대해 지원 됩니다. SQL Server 2012 SharePoint용 PowerPivot부터 PowerPivot 사용 현황 컬렉션 및 관리 대시보드 워크플로에 SharePoint 사용 데이터베이스가 사용되지 않습니다. 타이머 작업을 수동으로 실행하여 SharePoint 사용 데이터베이스의 나머지 PowerPivot 관련 데이터를 PowerPivot 서비스 애플리케이션 데이터베이스로 이동할 수 있습니다.<br /><br /> 이 타이머 작업은 팜 수준에서 전역적으로 구성되며, 중앙의 사용량 현황 데이터 컬렉션 데이터베이스에서 만료된 사용량 현황 데이터(즉, 30일이 지난 모든 레코드)를 확인합니다. 팜에 있는 PowerPivot 서버에 대해 이 타이머 작업은 PowerPivot 사용량 현황 데이터에 대한 추가 확인을 수행합니다. PowerPivot 사용량 현황 데이터가 감지되면 타이머 작업은 애플리케이션 식별자를 사용하여 데이터를 서비스 애플리케이션 데이터베이스로 이동하여 올바른 데이터베이스를 찾습니다.<br /><br /> 만료된 데이터 확인 또는 PowerPivot 서비스 애플리케이션 데이터베이스로 PowerPivot 사용량 현황 데이터의 데이터 가져오기를 실행하기 위해 이 타이머 작업을 수동으로 실행할 수 있습니다.|  
|PowerPivot 관리 대시보드 처리 타이머 작업|매일 오전 3시|이 타이머 작업은 PowerPivot 관리 대시보드에 관리 데이터를 제공하는 내부 PowerPivot 통합 문서를 업데이트합니다. 이 타이머 작업은 대시보드 보고서나 웹 파트에 나타나는 서버 이름, 사용자 이름, 애플리케이션 이름 및 파일 이름을 포함하여 SharePoint에서 관리하는 업데이트된 정보를 가져옵니다.|  
  
##  <a name="reporting-on-usage-data"></a><a name="reporting"></a> 사용량 현황 데이터에 대한 보고  
 PowerPivot 데이터에 대한 사용량 현황 데이터를 보기 위해 PowerPivot 관리 대시보드에서 기본 제공 보고서를 볼 수 있습니다. 기본 제공 보고서는 서비스 애플리케이션 데이터베이스의 보고 데이터 구조에서 검색한 사용량 현황 데이터를 통합합니다. 기본 보고서 데이터는 매일 업데이트되므로 Microsoft SharePoint Foundation 사용량 현황 데이터 처리 타이머 작업이 데이터를 PowerPivot 서비스 애플리케이션 데이터베이스로 복사한 후에만 기본 제공 사용 보고서에 업데이트된 정보가 표시됩니다. 기본적으로 이 작업은 하루에 한 번 발생합니다.  
  
 보고서를 보는 방법은 [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [PowerPivot 관리 대시보드 및 사용 현황 데이터](power-pivot-management-dashboard-and-usage-data.md)   
 [구성 설정 참조 &#40;SharePoint용 PowerPivot&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [&#40;SharePoint용 PowerPivot에 대 한 사용 현황 데이터 수집 구성](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
