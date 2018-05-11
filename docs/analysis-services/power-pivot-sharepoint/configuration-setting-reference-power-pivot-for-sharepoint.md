---
title: 구성 설정 참조 (SharePoint 용 파워 피벗) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d58ca9b3c3769a34164157f7297269f100ea8c1d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="configuration-setting-reference-power-pivot-for-sharepoint"></a>구성 설정 참조(SharePoint용 Power Pivot)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  이 항목에서는 SharePoint 팜에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램에 의해 사용되는 구성 설정에 대한 참조 설명서를 제공합니다. PowerShell 스크립트를 사용하여 서버를 구성하거나 특정 설정에 대한 정보를 찾아보려는 경우 이 항목의 정보가 자세한 설명을 제공합니다.  
  
 구성 설정은 각 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램에 대해 설정됩니다. 팜 내에서 동일한 물리적 서비스 인스턴스의 독립적 논리 인스턴스를 구성하는 방식으로 여러 서비스 응용 프로그램을 만들 수 있습니다. 구성 설정은 사용자가 구성하는 각 서비스 응용 프로그램에 대해 만들어지는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 응용 프로그램 데이터베이스에 저장됩니다.  
  
 구성 설정을 변경하는 경우 변경 내용이 즉시 선택되어 다음 요청 및 연결에 사용됩니다. 진행 중인 작업에는 작업이 시작될 때 유효했던 설정이 적용됩니다.  
  
 특정 구성 영역에 대해 알아보려면 다음 링크를 클릭하십시오.  
  
 [데이터 로드 제한 시간](#LoadingData)  
  
 [연결 풀](#ConnectionPool)  
  
 [부하 분산](#AllocationScheme)  
  
 [데이터 새로 고침](#DataRefresh)  
  
 [사용 데이터 수집](#UsageData)  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [중앙 관리에서 파워 피벗 서비스 응용 프로그램 만들기 및 구성](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)을 참조하세요.  
  
##  <a name="LoadingData"></a> 데이터 로드 제한 시간  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터는 팜에서 Analysis Services 서버 인스턴스에 의해 검색되고 로드됩니다. 마지막으로 데이터를 액세스한 방법과 시기에 따라 콘텐츠 라이브러리나 로컬 파일 캐시에서 데이터가 로드됩니다. 데이터는 쿼리나 처리 요청을 받을 때마다 메모리에 로드됩니다. 전체적인 서버 가용성을 최대화하기 위해 할당된 시간 내에 완료할 수 없을 경우 데이터 로드 요청을 중지하도록 서버에 지시하는 제한 시간 값을 설정할 수 있습니다.  
  
|이름|기본값|유효한 값|Description|  
|----------|-------------|------------------|-----------------|  
|데이터 로드 제한 시간|1800(초 단위)|1 ~ 3600|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램에서 특정 Analysis Services 서버 인스턴스의 응답을 기다릴 시간을 지정합니다.<br /><br /> 기본적으로 서비스 응용 프로그램은 특정 요청을 전달한 엔진 서비스 인스턴스로부터 데이터 페이로드를 30분 동안 기다립니다.<br /><br /> 이 기간 내에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본이 로드될 수 없는 경우 스레드가 중지되고 새로운 스레드가 시작됩니다.|  
  
##  <a name="ConnectionPool"></a> 연결 풀  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램은 연결 풀을 만들고 관리하여 연결을 다시 사용할 수 있도록 합니다. 연결 풀에는 읽기 전용 데이터에 대한 데이터 연결을 위한 풀과 서버 연결을 위한 풀의 두 가지 유형이 있습니다.  
  
 데이터 연결 풀에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본에 대한 캐시된 연결이 포함됩니다. 각 연결 풀은 데이터베이스가 로드될 때 설정된 컨텍스트를 기반으로 합니다. 이 컨텍스트에는 물리적 서비스 인스턴스의 ID, 데이터베이스 ID 및 데이터를 요청하는 SharePoint 사용자의 ID가 포함됩니다. 각 조합에 대해 별도의 연결 풀이 만들어집니다. 예를 들어 동일한 서버에서 동일한 데이터베이스를 실행 중인 다른 사용자로부터의 요청은 다른 풀의 연결을 사용합니다.  
  
 연결 풀의 용도는 동일한 SharePoint 사용자에 의한 동일한 Analysis Services 데이터베이스에 대한 읽기 전용 요청에 대해 캐시된 연결을 사용하기 위한 것입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 인스턴스는 메모리에 데이터가 로드된 서버입니다. 데이터베이스 ID는 데이터 모델의 메모리 내 데이터 구조에 대한 내부 식별자입니다. 모델은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브 데이터베이스로 인스턴스화됩니다. 버전 정보는 식별자에 암시적으로 통합됩니다.  
  
 서버 연결 풀에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 인스턴스에서 Analysis Services 서비스 인스턴스로의 캐시된 연결이 포함됩니다. 이때 서비스 응용 프로그램은 Analysis Services 서버에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Sysadmin 권한으로 연결됩니다. 이러한 연결은 데이터베이스 로드 요청을 실행하고 시스템 상태를 모니터링하기 위해 사용됩니다.  
  
 연결 풀의 각 유형에는 연결 관리를 위해 시스템 메모리를 최적으로 사용하기 위해 설정할 수 있는 상한값이 있습니다.  
  
|이름|기본값|유효한 값|Description|  
|----------|-------------|------------------|-----------------|  
|연결 풀 제한 시간|1800(초 단위)|1 ~ 3600|이 설정은 데이터 연결 풀에 적용됩니다.<br /><br /> 유휴 연결을 연결 풀에서 제거하기 전에 유지할 수 있는 시간을 지정합니다.<br /><br /> 기본적으로 서비스 응용 프로그램에서는 5분 넘게 연결이 비활성 상태인 경우 연결을 제거합니다.|  
|최대 사용자 연결 풀 크기|1000|-1, 0 또는 1 ~ 10000<br /><br /> -1은 유휴 연결 수에 제한이 없음을 의미합니다.<br /><br /> 0은 유휴 연결을 유지하지 않음을 의미합니다. 따라서 매번 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본에 대한 새로운 연결이 만들어져야 합니다.|이 설정은 특정 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 인스턴스에 대해 만들어진 모든 데이터 연결 풀의 유휴 연결에 적용됩니다.<br /><br /> SharePoint 사용자, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 및 서비스 인스턴스의 고유한 조합에 대해 개별 연결 풀이 만들어집니다. 많은 사용자가 다양한 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본에 액세스하는 경우 연결 풀 크기의 증가로 인해 서버 성능이 향상될 수 있습니다.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 인스턴스에 대해 100개가 넘는 유휴 연결이 있는 경우 새로 유휴 상태가 되는 연결은 풀로 반환되지 않고 연결이 해제됩니다.|  
|최대 관리 연결 풀 크기|200|-1, 0 또는 1 ~ 10000<br /><br /> -1은 유휴 연결 수에 제한이 없음을 의미합니다.|Analysis Services 서버 인스턴스에 대한 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 연결을 위해 만들어진 모든 관리 연결 풀의 최대 유휴 서버 연결 수. 서버 연결은 데이터베이스 로드 요청 및 변경 내용을 SharePoint 데이터베이스에 다시 저장하기 위해 사용됩니다.|  
  
##  <a name="AllocationScheme"></a> 부하 분산  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스에서 수행하는 기능 중 하나는 사용 가능한 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 인스턴스 중에서 Analysis Services 데이터가 로드될 위치를 결정하는 것입니다. **AllocationMethod** 설정은 서비스 인스턴스 선택 조건을 지정합니다.  
  
|이름|기본값|유효한 값|Description|  
|----------|-------------|------------------|-----------------|  
|할당 방법|RoundRobin|라운드 로빈<br /><br /> 상태 기반|둘 이상의 Analysis Services 서버 인스턴스에서 로드 요청을 할당하기 위한 체계.<br /><br /> 기본적으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스는 서버 상태를 기반으로 요청을 교대로 할당합니다. 상태 기반(Health Based)은 사용 가능한 메모리 및 CPU 사용률을 기반으로 가장 많은 시스템 리소스를 사용할 수 있는 서버에 요청을 할당합니다.<br /><br /> 라운드 로빈은 현재 부하 또는 서버 상태에 관계없이 사용 가능한 서버에 순차적으로 요청을 할당합니다.|  
  
##  <a name="DataRefresh"></a> 데이터 새로 고침  
 조직의 기본 또는 표준 업무 시간을 정의하는 시간 범위를 지정합니다. 이 구성 설정은 업무 시간 외에 데이터 새로 고침 작업을 위해 데이터 처리가 수행되는 시간을 결정합니다. 업무 시간 외 처리는 업무 시간이 종료되는 시간에 시작될 수 있습니다. 업무 시간 외 처리는 기본 업무 시간 중에 생성된 트랜잭션 데이터를 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본을 새로 고치려는 문서 소유자를 위한 일정 옵션입니다.  
  
|이름|기본값|유효한 값|Description|  
|----------|-------------|------------------|-----------------|  
|시작 시간|오전 4시|1 ~ 12시, 값은 이 범위 내의 유효한 정수<br /><br /> 유형은 Time|업무 시간 범위의 하한값을 설정합니다.|  
|종료 시간|오후 8시|1 ~ 12시, 값은 이 범위 내의 유효한 정수<br /><br /> 유형은 Time|업무 시간 범위의 상한값을 설정합니다.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 무인 데이터 새로 고침 계정|InclusionThresholdSetting|대상 응용 프로그램 ID|이 계정은 일정 소유자 대신 데이터 새로 고침 작업을 실행하는 데 사용됩니다.<br /><br /> 무인 데이터 새로 고침 계정을 서비스 응용 프로그램 구성 페이지에서 참조하려면 해당 계정을 미리 정의해야 합니다. 자세한 내용은 [파워 피벗 무인 데이터 새로 고침 계정 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)을 참조하세요.|  
|사용자가 사용자 지정 Windows 자격 증명을 입력할 수 있습니다.|설정|Boolean|예약된 데이터 새로 고침 구성 페이지에 예약 소유자가 데이터 새로 고침 작업을 실행하는 데 사용할 Windows 사용자 계정과 암호를 지정할 수 있는 옵션이 표시되는지 여부를 결정합니다.<br /><br /> 이 옵션을 사용하려면 Secure Store Service를 사용하도록 설정해야 합니다. 자세한 내용은 [파워 피벗 데이터 새로 고침을 위한 저장된 자격 증명 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)을 참조하세요.|  
|최대 처리 기록 길이|365|1~5000 일|데이터 새로 고침 기록이 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스에 보존되는 기간을 결정합니다. 자세한 내용은 [Power Pivot Usage Data Collection](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)을 참조하세요.|  
  
##  <a name="UsageData"></a> 사용 데이터 수집  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드에 표시되는 사용 보고서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]사용 통합 문서의 사용 방법에 대한 중요한 정보를 제공할 수 있습니다. 다음 구성 설정은 이후에 사용 또는 작업 보고서에 표시되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 이벤트에 대한 사용 데이터 컬렉션을 제어합니다.  
  
|이름|기본값|유효한 값|Description|  
|----------|-------------|------------------|-----------------|  
|쿼리 보고 간격|300(초)|1 ~ n초, 여기서 n은 임의의 유효한 정수|사용 데이터 컬렉션에서 팜의 데이터 전송 용량을 너무 많이 사용하지 않도록 하기 위해 쿼리 통계가 각 연결마다 수집되어 단일 이벤트로 보고됩니다. 쿼리 보고 간격은 이벤트 보고 빈도를 결정합니다. 기본적으로 쿼리 통계는 5분마다 보고됩니다.<br /><br /> 요청이 전송되면 즉시 연결이 종료되므로 시스템에서는 한 사용자가 하나의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본에 액세스하는 경우에도 매우 많은 수의 연결을 생성합니다. 따라서 각 사용자와 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 원본 조합에 대해 연결 풀이 만들어져 한 번 연결이 만들어지면 동일한 사용자가 동일한 데이터에 대해 이 연결을 다시 사용할 수 있습니다. 이 구성 설정을 통해 지정된 간격에 따라 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램에서 연결 풀의 각 연결에 대한 사용 데이터를 주기적으로 보고합니다.<br /><br /> 보고 시간 값을 늘리면 더 적은 수의 이벤트가 기록됩니다. 그러나 이 값을 너무 크게 설정하면 서버가 다시 시작되거나 연결이 종료될 경우 이벤트 데이터가 손실될 위험이 있습니다.<br /><br /> 값을 줄이면 더 많은 이벤트가 더 자주 기록되어 SharePoint 사용 데이터베이스의 데이터 컬렉션 시스템에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]관련 사용 데이터가 더 많이 추가됩니다.<br /><br /> 일반적으로 특정 문제를 해결하기 위한 경우(예: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 사용 데이터로 인해 사용 데이터베이스가 너무 빨리 커지는 경우)가 아니면 이 구성 설정을 변경하지 마세요.|  
|사용 데이터 기록|365(일)|0 또는 1 ~ n일, 여기서 n은 임의의 유효한 정수<br /><br /> 0은 기록이 항상 보존되며 삭제되지 않음을 의미합니다.|기본적으로 사용 데이터는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스에 1년 동안 유지됩니다. 1년이 넘은 레코드는 데이터베이스에서 삭제됩니다.<br /><br /> 매일 Microsoft SharePoint Foundation 사용 데이터 처리 작업이 실행될 때 만료된 기록 데이터에 대한 확인이 수행됩니다. 타이머 작업에서 이 설정을 읽고 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 데이터베이스의 만료된 기록에 대해 데이터 삭제 명령을 트리거합니다.|  
|간단한 응답 상한값|500(밀리초)|1 ~ n밀리초, 여기서 n은 임의의 유효한 정수|기본적으로 중요하지 않은 요청에 대한 임계값은 0.5초입니다.<br /><br /> 중요하지 않은 요청에는 서버 ping, 메타데이터 요청 및 세션 시작이 포함됩니다.|  
|빠른 응답 상한값|1000(밀리초)|1 ~ n밀리초, 여기서 n은 임의의 유효한 정수|기본적으로 빠른 요청에 대한 임계값은 1초입니다.<br /><br /> 빠른 요청은 데이터 집합이 매우 작거나 여러 큰 멤버 집합을 포함하는 메타데이터에 대한 요청입니다.|  
|예상 응답 상한값|3000(밀리초)|1 ~ n밀리초, 여기서 n은 임의의 유효한 정수|기본적으로 예상 요청에 대한 임계값은 3초입니다.<br /><br /> 이 임계값은 예상 쿼리 시간의 상한값을 설정합니다.|  
|긴 응답 상한값|10000(밀리초)|1 ~ n밀리초, 여기서 n은 임의의 유효한 정수|기본적으로 긴 요청에 대한 임계값은 10초입니다.<br /><br /> 예상보다 길게 실행되는 요청이나 여전히 허용 가능한 범위 내에 속하는 요청입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [중앙 관리에서 파워 피벗 서비스 응용 프로그램 만들기 및 구성](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [SharePoint 2010에서 Power Pivot 데이터 새로 고침](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [사용 현황 데이터 수집 구성&#40;SharePoint용 파워 피벗](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Power Pivot 서비스 계정 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Power Pivot 관리 대시보드 및 사용 데이터](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
  
