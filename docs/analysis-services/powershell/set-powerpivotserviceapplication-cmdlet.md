---
title: Set-powerpivotserviceapplication cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 16d10e2d-d7e1-40f1-bc9d-a4e10c61af95
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e1d1caae0c63d1ffdbbed07940b35a4a822787f5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="set-powerpivotserviceapplication-cmdlet"></a>Set-PowerPivotServiceApplication cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]속성을 설정 하는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램입니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
Set-PowerPivotServiceApplication [-Identity] <SPGeminiServiceApplicationPipeBind> [-AdministrationConnectionPoolSize <int>] [-AllowCustomWindowsCredentials] [-BusinessHoursEndTime <string>] [-BusinessHoursStartTime <string>] [-CachedDatabaseholdLimit <int>] [-Confirm <switch>] [-ConnectionPoolSize <int>] [-ConnectionPoolTimeout <int>] [-DataLoadTimeout <int>] [-DataRefreshFailureThreshold <int>] [-DataRefreshInactiveWorkbooksThreshold <int>] [-DataRefreshMaxHistory <int>] [-HealthBasedAllocation <switch>] [-LoadsToConnectionsRatioCollectionInterval <int>] [-LoadsToConnectionsRatioLimit <int>] [-MemoryDatabaseHoldLimit <int>] [-QueryReportingInterval <int>] [-RoundRobinAllocation <switch>] [-UnattendedAccount <string>] [-UsageDataRetentionPeriod <int>] [-UsageExpectedResponseUpperLimit <int>] [-UsageLongResponseUpperLimit <int>] [-UsageQuickResponseUpperLimit <int>] [-UsageTrivialResponseUpperLimit <int>] [-UsageUpdateDayLimit <int>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Set-PowerPivotServiceApplication cmdlet은 팜에 있는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램의 속성을 업데이트합니다. Identity 매개 변수는 필수입니다. 속성을 업데이트할 서비스 응용 프로그램의 GUID를 제공해야 합니다.  
  
 변경 내용을 확인 하려면 다음 cmdlet을 실행: Get-powerpivotserviceapplication-Identity \<GUID > | format-list 합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>Id \<SPGeminiServiceApplicationPipeBind >  
 업데이트할 서비스 응용 프로그램을 지정합니다. 유형은 유효한 GUID 또는 유효한 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 개체의 인스턴스여야 합니다. Get-PowerPivotServiceApplication을 사용하여 개체 인스턴스를 반환할 수 있습니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="-administrationconnectionpoolsize-int"></a>-AdministrationConnectionPoolSize \<int >  
 Analysis Services에 대한 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 연결용으로 생성된 연결 풀의 열린 연결 수를 지정합니다. 각 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 인스턴스는 같은 컴퓨터에 있는 Analysis Services 인스턴스에 대해 개별 관리 연결을 엽니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스는 별도의 풀을 만들어 유휴 연결을 확인하고 서버 상태를 모니터링하기 위해 관리 연결을 다시 사용합니다. 기본값은 연결 200개입니다. 유효한 값은 -1(제한 없음), 0(관리 연결 풀링 사용 안 함) 또는 1부터 10000까지입니다. 0을 선택하면 모든 연결이 새로 만들어집니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|200|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-allowcustomwindowscredentials-switchparameter"></a>-AllowCustomWindowsCredentials [\<SwitchParameter >]  
 일정 소유자가 데이터 새로 고침 일정을 실행하기 위해 임의의 Windows 자격 증명을 입력할 수 있는지 여부를 지정합니다. 이 확인란을 선택하면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램은 저장된 각 자격 증명 집합에 대해 대상 응용 프로그램을 만들고 관리합니다. 기본적으로 true로 설정됩니다. 이 기능을 해제하려면 AllowCustomWindowsCredentials:$false로 설정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-businesshoursendtime-string"></a>-BusinessHoursEndTime \<문자열 >  
 업무 시간을 정의하는 시간 범위에서 업무 시간이 종료되는 시간을 지정합니다. 데이터 새로 고침 일정은 업무 시간이 종료된 이후에 실행되어 정규 업무 시간 중에 생성된 트랜잭션 데이터를 가져올 수 있습니다. 기본값은 8:00 p.m입니다.  유효한 값은 따옴표로 묶어 a.m 또는 p.m 클럭 시간으로 지정합니다(예: "08:00PM"). 시간은 1에서 12 사이여야 합니다. 분은 1에서 59 사이여야 합니다.  
  
 업무 시간에 대한 전체 시간 범위를 지정하려면 BusinessHoursStartTime과 BusinessHoursEndTime을 모두 설정해야 합니다. 두 매개 변수는 업무 시간을 구성하는 시간의 구간을 정의합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|8 PM|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-businesshoursstarttime-string"></a>-BusinessHoursStartTime \<문자열 >  
 업무 시간을 정의하는 시간 범위에서 업무 시간이 시작되는 시간을 지정합니다. 데이터 새로 고침 일정은 업무 시간이 종료된 이후에 실행되어 정규 업무 시간 중에 생성된 트랜잭션 데이터를 가져올 수 있습니다. 기본값은 4:00 a.m입니다.  유효한 값은 따옴표로 묶어 a.m 또는 p.m 클럭 시간으로 지정합니다(예: "04:00AM"). 시간은 1에서 12 사이여야 합니다. 분은 1에서 59 사이여야 합니다.  
  
 업무 시간에 대한 전체 시간 범위를 지정하려면 BusinessHoursStartTime과 BusinessHoursEndTime을 모두 설정해야 합니다. 두 매개 변수는 업무 시간을 구성하는 시간의 구간을 정의합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|4 AM|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-cacheddatabaseholdlimit-int"></a>-CachedDatabaseholdLimit \<int >  
 비활성 데이터베이스가 메모리에서 언로드된 후 파일 시스템에 유지되는 시간을 지정합니다. 기본값은 120시간입니다. 정리 작업에서는 이 설정을 사용하여 삭제할 파일을 결정합니다. 168시간(메모리에서 48시간 및 캐시에서 120시간) 동안 비활성 상태인 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스는 정리 작업에 의해 디스크에서 삭제됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|120|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-confirm-switch"></a>-확인 \<전환 >  
 명령을 실행하기 전 확인 메시지를 표시합니다. 이 값은 기본적으로 설정되어 있습니다. 명령에서 확인 응답을 무시하려면 명령에 Confirm:$false를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-connectionpoolsize-int"></a>-ConnectionPoolSize \<int >  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스가 각 SharePoint 사용자, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 집합 및 버전 조합에 대해 개별 연결 풀에서 만들 최대 유휴 연결 수를 지정합니다. 기본 유휴 연결 수는 1000입니다. 유효한 값은 -1(제한 없음), 0(사용자 연결 풀링 비활성화) 또는 1부터 10000까지입니다. 이러한 연결 풀을 사용하면 서비스가 같은 사용자의 같은 읽기 전용 데이터에 대한 지속적인 연결을 보다 효율적으로 지원할 수 있습니다. 연결 풀링을 사용하지 않도록 설정하면 모든 연결이 새로 작성됩니다. 연결 풀 크기에서 이 한계를 변경(0으로 설정하는 경우 포함)해도 연결이 끊기지는 않습니다. 연결 풀은 데이터에 연결할 때 대기 시간을 줄이기 위한 것이며, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스는 연결 풀 설정을 기준으로 연결을 거부하지 않습니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|1000|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-connectionpooltimeout-int"></a>-ConnectionPoolTimeout \<int >  
 유휴 데이터 연결이 열린 상태로 유지되는 시간(분)을 지정합니다. 기본값은 1800초 또는 30분입니다. 이 기간 동안 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램은 같은 SharePoint 사용자가 같은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대해 보내는 읽기 전용 요청에 유휴 데이터 연결을 다시 사용합니다. 지정된 기간 동안 해당 데이터에 대해 추가 요청이 수신되지 않는 경우 풀에서 연결이 제거됩니다. 유효한 값은 1초에서 3600초까지입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|1800|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-dataloadtimeout-int"></a>-DataLoadTimeout \<int >  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램이 데이터 로드 요청을 전달한 SQL Server Analysis Services([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 인스턴스로부터의 응답을 기다리는 시간을 지정합니다. 데이터 집합이 크면 네트워크를 통해 이동하는 데 시간이 걸리므로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 인스턴스가 Excel 통합 문서를 검색하고 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 쿼리 처리를 위해 Analysis Services 인스턴스로 이동할 충분한 시간을 허용해야 합니다. 기본값은 1800초 또는 30분입니다. 유효한 값은 1초에서 3600초까지입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|1800|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-datarefreshfailurethreshold-int"></a>-DataRefreshFailureThreshold \<int >  
 일정을 사용하지 않도록 설정할 연속 실패 횟수를 지정합니다. 기본값은 10입니다. 새로 고침 실패가 발생하면 즉시 일정을 사용하지 않도록 설정하려는 경우 0을 입력하면 됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|10|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-datarefreshinactiveworkbooksthreshold-int"></a>-DataRefreshInactiveWorkbooksThreshold \<int >  
 일정을 사용하지 않도록 설정할 때까지의 데이터 새로 고침 주기 수를 지정하거나 비활성 상태인 경우 즉시 일정을 사용하지 않도록 설정하려면 0을 입력합니다. 기본값은 10입니다.  
  
 통합 문서 비활성 상태는 여러 데이터 새로 고침 주기에 대한 연결 이벤트가 없는 것으로 측정됩니다. 데이터 새로 고침 주기는 작업의 성공 여부에 관계없이 일정이나 지금 실행 작업에 의해 데이터 새로 고침 작업이 트리거될 때마다 계산됩니다. 통합 문서에 대한 연결 요청 없이 주기 수(기본적으로 10)가 초과하는 경우 비활성 상태로 인해 데이터 새로 고침 일정을 사용하지 않도록 설정됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|10|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-datarefreshmaxhistory-int"></a>-DataRefreshMaxHistory \<int >  
 데이터 새로 고침 기록을 보관할 기간을 지정합니다. 이 정보는 데이터 새로 고침을 사용하는 각 통합 문서에 대해 유지되는 데이터 새로 고침 기록 페이지에 표시되며 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드에도 표시됩니다. 기본값은 365일입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|365|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-healthbasedallocation-switch"></a>-HealthBasedAllocation \<전환 >  
 사용 가능한 CPU 및 메모리 리소스가 가장 많은 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버로 연결 요청을 전달하는 상태 기반 할당 알고리즘을 지정합니다. 기본 할당 알고리즘입니다. HealthBasedAllocation과 Roundrobinbasedallocation은 상호 배타적입니다. 따라서 둘 중 하나만 지정해야 합니다. 둘 모두 false로 설정하면 HealthBasedAllocation이 기본 설정이므로 HealthBasedAllocation이 사용됩니다. 둘 모두 true로 설정하면 유효성 검사 오류가 발생합니다. 이러한 매개 변수의 구문에는 매개 변수 이름만 입력하거나 parameter:$true 또는 parameter:$false만 입력합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-loadstoconnectionsratiocollectioninterval-int"></a>-LoadsToConnectionsRatioCollectionInterval \<int >  
 연결 로드 비율을 계산하기 위해 로드 및 연결 이벤트를 계산할 간격(시간)을 지정합니다. 기본적으로 4시간마다 새 비율이 계산됩니다. 유효한 값은 1에서 24까지입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|4|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-loadstoconnectionsratiolimit-int"></a>-LoadsToConnectionsRatioLimit \<int >  
 서버 상태 표시기로 사용되는 로드 이벤트 대 연결 이벤트의 비율을 지정합니다. 기본값은 20%입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|20|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-memorydatabaseholdlimit-int"></a>-MemoryDatabaseHoldLimit \<int >  
 비활성 데이터베이스가 해당 데이터에 대한 새 요청을 처리하기 위해 메모리에 유지되는 시간을 지정합니다. 활성 데이터베이스는 쿼리하고 있는 동안에는 항상 메모리에 유지되지만 더 이상 활성 상태가 아니면 해당 데이터에 대한 추가 요청이 있을 경우를 대비해 추가 기간 동안 메모리에 유지됩니다. 기본값은 48시간입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|48|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-queryreportinginterval-int"></a>-QueryReportingInterval \<int >  
 쿼리 응답 통계를 사용 이벤트로 보고하기 전에 수집하는 시간(초)을 지정합니다. 기본값은 300초입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|300|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-roundrobinallocation-switch"></a>-RoundRobinAllocation \<전환 >  
 다음 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버로 연결 요청을 전달하여 서버 부하에 관계없이 사용 가능한 서버 간에 요청을 번갈아 가며 균일하게 할당하는 라운드 로빈 할당 알고리즘을 지정합니다. HealthBasedAllocation과 Roundrobinbasedallocation은 상호 배타적입니다. 따라서 둘 중 하나만 지정해야 합니다. 둘 모두 false로 설정하면 HealthBasedAllocation이 기본 설정이므로 HealthBasedAllocation이 사용됩니다. 둘 모두 true로 설정하면 유효성 검사 오류가 발생합니다. 이러한 매개 변수의 구문에는 매개 변수 이름만 입력하거나 parameter:$true 또는 parameter:$false만 입력합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-unattendedaccount-string"></a>-UnattendedAccount \<문자열 >  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 새로 고침 작업을 실행하는 데 사용되는 미리 정의된 계정이 저장되는 보안 저장소 서비스 응용 프로그램의 대상 응용 프로그램 이름을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-usagedataretentionperiod-int"></a>-UsageDataRetentionPeriod \<int >  
 사용 데이터 및 서버 상태 통계에 대한 기록을 보관할 기간(일)을 지정합니다. 기본값은 365일입니다. 이 값을 0으로 설정하면 모든 기록이 무한정 보관됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|365|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-usageexpectedresponseupperlimit-int"></a>-UsageExpectedResponseUpperLimit \<int >  
 예상 요청-응답 교환을 정의하는 상한을 설정합니다. 기본값은 3000밀리초입니다. 1000밀리초에서 3000밀리초 사이에 완료되는 모든 요청은 보고에서 예상 응답으로 간주됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|3000|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-usagelongresponseupperlimit-int"></a>-UsageLongResponseUpperLimit \<int >  
 장기 실행 요청-응답 교환을 정의하는 상한을 설정합니다.  상한은 10000밀리초입니다. 이 상한을 초과하는 모든 요청은 상한 임계값이 없는 초과 범주에 속합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|10000|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-usagequickresponseupperlimit-int"></a>-UsageQuickResponseUpperLimit \<int >  
 빠른 요청-응답 교환을 정의하는 상한을 설정합니다. 기본값은 1000밀리초입니다. 500밀리초에서 1000밀리초 사이에 완료되는 모든 요청은 보고에서 빠른 응답으로 간주됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|1000|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-usagetrivialresponseupperlimit-int"></a>-UsageTrivialResponseUpperLimit \<int >  
 데이터 컬렉션에서 관련이 있다고 보기에는 너무 짧은 응답 시간 범주를 지정합니다. 이 범주에 속하는 대부분의 응답은 서버 대 서버 통신입니다. 기본적으로 이 값은 500밀리초입니다. 0밀리초에서 500밀리초 사이에 완료되는 모든 요청은 간단한 요청으로, 보고에서 무시됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|500|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-usageupdatedaylimit-int"></a>-UsageUpdateDayLimit \<int >  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드의 보고서에 사용되는 데이터 파일의 새로 고침 실패에 대해 경고를 트리거하는 임계값(일)을 지정합니다. 사용 데이터는 기본적으로 매일 업데이트됩니다. 관리 보고서의 데이터 원본인 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Management Dashboard.xlsx 파일도 매일 새로 고쳐집니다. 이 .xlsx 파일이 며칠 동안 업데이트되지 않으면 파일이 최신 상태가 아님을 나타내는 상태 규칙이 트리거됩니다. 기본값은 5일입니다. 유효한 값은 1에서 30까지입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|5|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## <a name="example-1"></a>예제 1  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -AllowCustomWindowsCredentials:$false -UnattendedAccount "MyTargetApp"  
```  
  
 이 예에서는 임의의 Windows 자격 증명을 저장하기 위한 Secure Store Service 대상 응용 프로그램을 자동으로 만들고 관리하는 데이터 새로 고침 기능을 해제합니다. 또한 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 무인 데이터 새로 고침 계정을 미리 정의된 대상 응용 프로그램으로 설정합니다.  
  
 유효한 ID를 가져오려면 Get-powerpivotserviceapplication을 사용합니다.  
  
## <a name="example-2"></a>예제 2  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -HealthBasedAllocation  
```  
  
 이 예에서는 사용 가능한 리소스가 가장 많은 서버로 연결 요청을 전달하는 상태 기반 할당 알고리즘을 지정합니다.  
  
 유효한 ID를 가져오려면 Get-powerpivotserviceapplication을 사용합니다.  
  
## <a name="example-3"></a>예 3  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklmn -BusinessHoursStartTime "07:15AM" -BusinessHoursEndTime "08:00PM"  
```  
  
 이 예에서는 업무 시간 시작 시간 및 종료 시간을 설정하는 방법을 보여 줍니다. 이 방법은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 새로 고침을 예약하는 일정 옵션으로 사용됩니다. 일정에 업무 시간 이후의 시간을 지정하여 업무 시간이 종료된 후에 데이터 새로 고침을 실행할 수 있습니다.  
  
 유효한 ID를 가져오려면 Get-powerpivotserviceapplication을 사용합니다.  
  
  
