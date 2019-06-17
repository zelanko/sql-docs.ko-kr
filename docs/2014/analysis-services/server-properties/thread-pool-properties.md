---
title: 스레드 풀 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- PriorityRatio property
- threads [Analysis Services]
- MinThreads property
- NumThreads property
- MaxThreads property
- Concurrency property
ms.assetid: e2697bb6-6d3f-4621-b9fd-575ac39c2185
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fe324da14460d69d6930bf9d398a50e816f676f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068842"
---
# <a name="thread-pool-properties"></a>스레드 풀 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 여러 작업에 다중 스레드를 사용하여 여러 작업을 병렬로 실행함으로써 전반적인 서버 성능을 향상시킵니다. 스레드를 보다 효율적으로 관리하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 스레드 풀을 사용해서 스레드를 미리 할당하고 다음 작업에 스레드를 쉽게 사용할 수 있도록 지원합니다.  
  
 각 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 고유한 스레드 풀 집합을 유지 관리합니다. 테이블 형식과 다차원 인스턴스에서 스레드 풀이 사용되는 방법에는 중요한 차이점이 있습니다. 가장 중요 한 차이점은 다차원 솔루션만 사용 하 여 `IOProcess` 스레드 풀입니다. 따라서 테이블 형식 인스턴스의 경우에는 이 항목에서 설명하는 `PerNumaNode` 속성이 의미가 없습니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [Analysis Services의 스레드 관리](#bkmk_threadarch)  
  
-   [스레드 풀 속성 참조](#bkmk_propref)  
  
-   [GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정](#bkmk_groupaffinity)  
  
-   [NUMA 노드에서 프로세서에 대한 IO 스레드 선호도를 설정하기 위한 PerNumaNode 설정](#bkmk_pernumanode)  
  
-   [현재 스레드 풀 설정 확인](#bkmk_currentsettings)  
  
-   [종속되었거나 관련된 속성](#bkmk_related)  
  
-   [MSMDSRV.INI 정보](#bkmk_msmdrsrvini)  
  
> [!NOTE]  
>  NUMA 시스템의 테이블 형식 배포는 이 항목의 범위를 벗어납니다. 테이블 형식 솔루션을 NUMA 시스템에 성공적으로 배포할 수 있지만 테이블 형식 모델에 사용되는 메모리 내 데이터베이스 기술의 성능 특성으로 인해 고도로 확장된 아키텍처에서는 이에 대한 이점이 제한적일 수 있습니다. 자세한 내용은 참조 하세요. [Analysis Services 사례 연구: 대규모 상용 솔루션에서 테이블 형식 모델을 사용 하 여](https://msdn.microsoft.com/library/dn751533.aspx) 하 고 [테이블 형식 솔루션의 크기를 조정 하는 하드웨어](https://go.microsoft.com/fwlink/?LinkId=330359)합니다.  
  
##  <a name="bkmk_threadarch"></a> Analysis Services의 스레드 관리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 다중 스레드를 사용해서 병렬로 실행되는 작업 수를 늘림으로써 사용 가능한 CPU 리소스의 활용도를 높입니다. 스토리지 엔진은 다중 스레드로 지정됩니다. 스토리지 엔진 내에서 실행되는 다중 스레드 작업의 예로는 병렬 개체 처리 또는 스토리지 엔진에 밀어 넣은 불연속 쿼리 처리 또는 쿼리에서 요청된 데이터 값 반환이 포함됩니다. 수식 엔진은 수식이 평가하는 계산의 직렬 특성으로 인해 단일 스레드로 지정됩니다. 각 쿼리는 기본적으로 단일 스레드로 실행되며, 데이터를 요청하고 종종 스토리지 엔진에서 데이터가 반환될 때까지 기다립니다. 쿼리 스레드는 실행하는 데 더 오래 걸리며, 전체 쿼리가 완료된 다음에만 해제됩니다.  
  
 기본적으로 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 상위 버전의 Windows  및 SQL  Server를 실행하는 시스템에서 최대 640개까지 사용 가능한 모든 논리적 프로세서를 사용합니다. msmdsrv.exe 프로세스는 시작 시 특정 프로세스 그룹에 할당되지만 시간이 지남에 따라 임의 프로세서 그룹의 임의 논리적 프로세스에서 스레드를 예약할 수 있습니다.  
  
 많은 수의 프로세서 사용으로 인해 발생하는 한 가지 부작용은 많은 수의 프로세서에서 쿼리 및 처리 부하가 분산되고 공유 데이터 구조에 대한 경합이 증가함에 따라 성능 저하 문제가 발생할 수 있다는 것입니다. 이 문제는 특히 NUMA 아키텍처를 사용하는 고성능 시스템에서 발생할 수 있지만, 동일한 하드웨어에서 데이터 사용량이 많은 애플리케이션을 여러 개 실행하는 비NUMA 시스템에서도 이 문제가 발생할 수 있습니다.  
  
 이 문제를 줄이기 위해서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 작업 유형 간의 선호도를 설정하고 그에 따라 특정 논리적 프로세서 집합을 설정할 수 있습니다. `GroupAffinity` 속성을 사용하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 관리되는 각 스레드 풀 유형에 사용할 시스템 리소스를 지정하는 사용자 지정 선호도 마스크를 만들 수 있습니다.  
  
 사용자 지정 선호도는 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 작업 로드에 사용되는 5개 스레드 풀 중 어디에든 설정할 수 있습니다.  
  
-   **구문 분석 \ 짧은**  풀은 짧은 요청에 대한 구문 분석 풀입니다. 단일 네트워크 메시지 내에 포함되는 요청은 짧은 요청으로 간주됩니다.  
  
-   **구문 분석 \ 긴**  풀은 단일 네트워크 메시지 내에 포함되지 않는 다른 모든 요청에 대한 구문 분석 풀입니다.  
  
    > [!NOTE]  
    >  어느 구문 분석 풀의 스레드라도 쿼리를 실행하는 데 사용될 수 있습니다. 빠른 검색 또는 취소 요청과 같이 신속하게 실행되는 쿼리는 일부 경우, 쿼리 스레드 풀 큐에 저장되는 대신 즉시 실행될 수 있습니다.  
  
-   `Query` 구문 분석 스레드 풀에서 처리 되지 않은 모든 요청을 실행 하는 스레드 풀이입니다. 이 스레드 풀의 스레드는 검색, MDX, DAX, DMX 및 DDL 명령과 같은 모든 유형의 작업을 실행합니다.  
  
-   `IOProcess` 다차원 엔진에서 저장소 엔진 쿼리와 연관 된 IO 작업에 사용 됩니다. 이러한 스레드에서 수행되는 작업은 다른 스레드에 대한 종속성이 없는 것으로 고려됩니다. 이러한 스레드는 일반적으로 파티션의 단일 세그먼트를 검사하고 세그먼트 데이터에 대한 필터링 및 집계를 수행합니다. `IOProcess` 스레드는 특히 NUMA 하드웨어 구성에 민감합니다. 따라서이 스레드 풀에는 `PerNumaNode` 필요에 따라 성능을 조정에 사용할 수 있는 구성 속성입니다.  
  
-   `Process` 오래 걸리는 저장소 엔진 작업을 집계, 인덱싱 및 커밋 작업을 포함 하 여입니다. ROLAP 스토리지 모드에서도 처리 스레드 풀의 스레드가 사용됩니다.  
  
> [!NOTE]  
>  Msmdsrv.ini에서 스레드 풀 설정이 있지만 합니다 `VertiPaq` 섹션인 `VertiPaq` \\ `ThreadPool` \\ `GroupAffinity` 및 `ThreadPool` \\ `CPUs` 는 의도적으로 설명 합니다. 이러한 속성은 현재 작동 가능하지 않으며, 이후에 사용할 수 있도록 예약되어 있습니다.  
  
 작업 수행에 필요한 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 서비스 요청에 대해 최대 스레드 풀 한도를 초과하여 추가 스레드를 요청할 수 있습니다. 하지만 현재 스레드 수가 최대 한도보다 큰 경우, 스레드의 작업 수행이 완료되면 스레드가 스레드 풀로 반환되는 대신 단순히 종료됩니다.  
  
> [!NOTE]  
>  최대 스레드 풀 수를 초과하는 것은 특정 교착 상태 조건이 발생하는 경우에만 호출되는 보호 장치입니다. 런어웨이 스레드가 최대값을 넘어 만들어지지 않도록 하기 위해 최대 한도에 도달한 이후에는 짧은 지연 후 스레드가 점진적으로 만들어집니다. 최대 스레드 수를 초과하면 태스크 실행 속도가 느려질 수 있습니다. 성능 카운터를 통해 스레드 수가 스레드 풀의 최대 크기를 정기적으로 넘음을 나타내는 경우, 이 성능 카운터를 스레드 풀 크기가 시스템에서 요청되는 동시성 수준에 비해 너무 작음을 나타내는 지표로 사용할 수 있습니다.  
  
 기본적으로 스레드 풀 크기는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 결정되며,  코어 수를 기반으로 합니다. 선택된 기본값은 서비스 시작 후 msmdsrv.log를 조사하여 확인할 수 있습니다. 한 가지 성능 튜닝 방법으로, 다른 속성뿐만 아니라 스레드 풀 크기를 늘려서 쿼리 또는 처리 성능을 향상시킬 수 있습니다.  
  
##  <a name="bkmk_propref"></a> 스레드 풀 속성 참조  
 이 섹션에서는 각 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 msmdsrv.ini  파일에 있는 스레드 풀 속성에 대해 설명합니다. 이러한 속성의 하위 집합도 SQL Server Management Studio에 표시됩니다.  
  
 속성은 사전순으로 나열됩니다.  
  
|이름|형식|Description|기본값|지침|  
|----------|----------|-----------------|-------------|--------------|  
|`IOProcess` \ `Concurrency`|double|큐에 한 번에 넣을 수 있는 스레드 수의 목표치를 설정하는 알고리즘을 결정하는 배정밀도 부동 소수점 값입니다.|2.0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> Windows에서 IO 완료 포트를 사용해서 구현되는 동시성을 사용해서 스레드 풀이 초기화됩니다. 자세한 내용은 [I/O 완료 포트](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 를 참조하세요.<br /><br /> 다차원 모델에만 적용됩니다.|  
|`IOProcess` \ `GroupAffinity`|string|시스템의 프로세서 그룹에 해당하는 16진수 값 배열로, 각 프로세서 그룹의 논리적 프로세서에 대한 IOProcess 스레드 풀의 스레드 선호도를 설정하는 데 사용됩니다.|none|이 속성을 사용해서 사용자 지정 선호도를 만들 수 있습니다. 이 속성은 기본적으로 비어 있습니다.<br /><br /> 자세한 내용은 [GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정](#bkmk_groupaffinity) 를 참조하세요.<br /><br /> 다차원 모델에만 적용됩니다.|  
|`IOProcess` \ `MaxThreads`|ssNoversion|스레드 풀에 포함할 최대 스레드 수를 지정하는 부호 있는 32비트 정수입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본적으로 서버는 이 값을 64 또는 논리적 프로세서 수의 10배 중에서 큰 값으로 설정합니다. 예를 들어 하이퍼스레딩을 지원하는 4코어 시스템에서 스레드 풀 최대값은 80개 스레드입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다. 예를 들어 논리적 프로세서가 32개인 서버에서 -10으로 설정된 경우 최대값은 320개의 스레드입니다.<br /><br /> 최대값은 이전에 정의한 사용자 지정 선호도 마스크당 사용 가능한 프로세서 수의 영향을 받습니다. 예를 들어 32개의 프로세서 중에서 8개를 사용하도록 스레드 풀 선호도를 이미 설정한 경우 MaxThreads를 -10으로 설정하면 스레드 풀의 상한이 10에 8을 곱한 80개의 스레드가 됩니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.<br /><br /> 스레드 풀 설정 튜닝에 대한 자세한 내용은 [Analysis  Services  작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx)에서 찾을 수 있습니다.<br /><br /> 다차원 모델에만 적용됩니다.|  
|`IOProcess` \ `MinThreads`|ssNoversion|스레드 풀에 미리 할당할 최소 스레드 수를 지정하는 부호 있는 32비트 정수입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본적으로 최소값은 1입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.<br /><br /> 스레드 풀 설정 튜닝에 대한 자세한 내용은 [Analysis  Services  작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx)에서 찾을 수 있습니다.<br /><br /> 다차원 모델에만 적용됩니다.|  
|`IOProcess` \ `PerNumaNode`|ssNoversion|msmdsrv 프로세스에 대해 생성되는 스레드 풀 수를 결정하는 부호 있는 32비트 정수입니다.|-1|유효한 값은 -1, 0, 1, 2입니다.<br /><br /> -1 = NUMA 노드 수에 따라 서버가 다른 IO 스레드 풀 전략을 선택합니다. NUMA 노드가 4개 미만인 시스템에서 서버 동작은 0과 동일합니다(하나의 IOProcess 스레드 풀이 시스템에 대해 만들어짐). 노드가 4개 이상인 시스템에서 서버 동작은 1과 동일합니다(IOProcess 스레드 풀이 각 노드에 대해 만들어짐).<br /><br /> 0 = msmdsrv.exe 프로세스에서 IOProcess 스레드 풀이 1개만 사용되도록 NUMA 노드당 스레드 풀이 사용되지 않도록 설정합니다.<br /><br /> 1 = NUMA 노드당 IOProcess 스레드 풀이 1개 사용되도록 설정합니다.<br /><br /> 2 = 논리적 프로세서당 1개의 IOProcess 스레드 풀이 사용됩니다. 각 스레드 풀의 스레드는 논리적 프로세서의 NUMA 노드로 선호도가 설정되고 논리적 프로세서에 이상적인 프로세서가 설정됩니다.<br /><br /> 자세한 내용은 [NUMA 노드에서 프로세서에 대한 IO 스레드 선호도를 설정하기 위한 PerNumaNode 설정](#bkmk_pernumanode) 를 참조하세요.<br /><br /> 다차원 모델에만 적용됩니다.|  
|`IOProcess` \ `PriorityRatio`|ssNoversion|우선 순위가 더 높은 큐가 비어 있지 않을 경우에도 우선 순위가 낮은 스레드가 가끔 실행되도록 보장하기 위해 사용할 수 있는 부호 있는 32비트 정수입니다.|2|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> 다차원 모델에만 적용됩니다.|  
|`IOProcess` \ `StackSizeKB`|ssNoversion|스레드 실행 중 메모리 할당을 조정하는 데 사용할 수 있는 부호 있는 32비트 정수입니다.|0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> 다차원 모델에만 적용됩니다.|  
|**구문 분석**  \ `Long` \ `Concurrency`|double|큐에 한 번에 넣을 수 있는 스레드 수의 목표치를 설정하는 알고리즘을 결정하는 배정밀도 부동 소수점 값입니다.|2.0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> Windows에서 IO 완료 포트를 사용해서 구현되는 동시성을 사용해서 스레드 풀이 초기화됩니다. 자세한 내용은 [I/O 완료 포트](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 를 참조하세요.|  
|**구문 분석**  \ `Long` \ `GroupAffinity`|string|시스템의 프로세서 그룹에 해당하는 16진수 값 배열로, 각 프로세서 그룹의 논리적 프로세서에 대한 구문 분석 스레드의 선호도를 설정하는 데 사용됩니다.|none|이 속성을 사용해서 사용자 지정 선호도를 만들 수 있습니다. 이 속성은 기본적으로 비어 있습니다.<br /><br /> 자세한 내용은 [GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정](#bkmk_groupaffinity) 를 참조하세요.|  
|**구문 분석**  \ `Long` \ `NumThreads`|ssNoversion|긴 명령에 대해 만들 수 있는 스레드 수를 정의하는 부호 있는 32비트 정수 속성입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본 동작은 `NumThreads`를 절대값 4  또는 논리적 프로세서 수의 2배 중에서 큰 값으로 설정하는 것입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다. 예를 들어 논리적 프로세서가 32개인 서버에서 -10으로 설정된 경우 최대값은 320개의 스레드입니다.<br /><br /> 최대값은 이전에 정의한 사용자 지정 선호도 마스크당 사용 가능한 프로세서 수의 영향을 받습니다. 예를 들어 32개의 프로세서 중에서 8개를 사용하도록 스레드 풀 선호도를 이미 설정한 경우 NumThreads를 -10으로 설정하면 스레드 풀의 상한이 10에 8을 곱한 80개의 스레드가 됩니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.|  
|**구문 분석**  \ `Long` \ `PriorityRatio`|ssNoversion|우선 순위가 더 높은 큐가 비어 있지 않을 경우에도 우선 순위가 낮은 스레드가 가끔 실행되도록 보장하기 위해 사용할 수 있는 부호 있는 32비트 정수입니다.|0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|**구문 분석**  \ `Long` \ `StackSizeKB`|ssNoversion|스레드 실행 중 메모리 할당을 조정하는 데 사용할 수 있는 부호 있는 32비트 정수입니다.|0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|**구문 분석**  \ `Short` \ `Concurrency`|double|큐에 한 번에 넣을 수 있는 스레드 수의 목표치를 설정하는 알고리즘을 결정하는 배정밀도 부동 소수점 값입니다.|2.0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> Windows에서 IO 완료 포트를 사용해서 구현되는 동시성을 사용해서 스레드 풀이 초기화됩니다. 자세한 내용은 [I/O 완료 포트](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 를 참조하세요.|  
|**구문 분석**  \ `Short` \ `GroupAffinity`|string|시스템의 프로세서 그룹에 해당하는 16진수 값 배열로, 각 프로세서 그룹의 논리적 프로세서에 대한 구문 분석 스레드의 선호도를 설정하는 데 사용됩니다.|none|이 속성을 사용해서 사용자 지정 선호도를 만들 수 있습니다. 이 속성은 기본적으로 비어 있습니다.<br /><br /> 자세한 내용은 [GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정](#bkmk_groupaffinity) 를 참조하세요.|  
|**구문 분석**  \ `Short` \ `NumThreads`|ssNoversion|짧은 명령에 대해 만들 수 있는 스레드 수를 정의하는 부호 있는 32비트 정수 속성입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본 동작은 `NumThreads`를 절대값 4  또는 논리적 프로세서 수의 2배 중에서 큰 값으로 설정하는 것입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다. 예를 들어 논리적 프로세서가 32개인 서버에서 -10으로 설정된 경우 최대값은 320개의 스레드입니다.<br /><br /> 최대값은 이전에 정의한 사용자 지정 선호도 마스크당 사용 가능한 프로세서 수의 영향을 받습니다. 예를 들어 32개의 프로세서 중에서 8개를 사용하도록 스레드 풀 선호도를 이미 설정한 경우 NumThreads를 -10으로 설정하면 스레드 풀의 상한이 10에 8을 곱한 80개의 스레드가 됩니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.|  
|**구문 분석**  \ `Short` \ `PriorityRatio`|ssNoversion|우선 순위가 더 높은 큐가 비어 있지 않을 경우에도 우선 순위가 낮은 스레드가 가끔 실행되도록 보장하기 위해 사용할 수 있는 부호 있는 32비트 정수입니다.|0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|**구문 분석**  \ `Short` \ `StackSizeKB`|ssNoversion|스레드 실행 중 메모리 할당을 조정하는 데 사용할 수 있는 부호 있는 32비트 정수입니다.|64 * 논리적 프로세서|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|`Process` \ `Concurrency`|double|큐에 한 번에 넣을 수 있는 스레드 수의 목표치를 설정하는 알고리즘을 결정하는 배정밀도 부동 소수점 값입니다.|2.0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> Windows에서 IO 완료 포트를 사용해서 구현되는 동시성을 사용해서 스레드 풀이 초기화됩니다. 자세한 내용은 [I/O 완료 포트](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 를 참조하세요.|  
|`Process` \ `GroupAffinity`|string|시스템의 프로세서 그룹에 해당하는 16진수 값 배열로, 각 프로세서 그룹의 논리적 프로세서에 대한 처리 스레드의 선호도를 설정하는 데 사용됩니다.|none|이 속성을 사용해서 사용자 지정 선호도를 만들 수 있습니다. 이 속성은 기본적으로 비어 있습니다.<br /><br /> 자세한 내용은 [GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정](#bkmk_groupaffinity) 를 참조하세요.|  
|`Process` \ `MaxThreads`|ssNoversion|스레드 풀에 포함할 최대 스레드 수를 지정하는 부호 있는 32비트 정수입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본적으로 서버는 이 값을 절대값 64 또는 논리적 프로세서 수 중에서 큰 값으로 설정합니다. 예를 들어 하이퍼스레딩을 사용하는 64코어 시스템(논리적 프로세서가 128개 생성됨)에서 스레드 풀 최대값은 128개 스레드입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다. 예를 들어 논리적 프로세서가 32개인 서버에서 -10으로 설정된 경우 최대값은 320개의 스레드입니다.<br /><br /> 최대값은 이전에 정의한 사용자 지정 선호도 마스크당 사용 가능한 프로세서 수의 영향을 받습니다. 예를 들어 32개의 프로세서 중에서 8개를 사용하도록 스레드 풀 선호도를 이미 설정한 경우 MaxThreads를 -10으로 설정하면 스레드 풀의 상한이 10에 8을 곱한 80개의 스레드가 됩니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.<br /><br /> 스레드 풀 설정 튜닝에 대한 자세한 내용은 [Analysis  Services  작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx)에서 찾을 수 있습니다.|  
|`Process` \ `MinThreads`|ssNoversion|스레드 풀에 미리 할당할 최소 스레드 수를 지정하는 부호 있는 32비트 정수입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본적으로 최소값은 1입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.<br /><br /> 스레드 풀 설정 튜닝에 대한 자세한 내용은 [Analysis  Services  작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx)에서 찾을 수 있습니다.|  
|`Process` \ `PriorityRatio`|ssNoversion|우선 순위가 더 높은 큐가 비어 있지 않을 경우에도 우선 순위가 낮은 스레드가 가끔 실행되도록 보장하기 위해 사용할 수 있는 부호 있는 32비트 정수입니다.|2|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|`Process` \ `StackSizeKB`|ssNoversion|스레드 실행 중 메모리 할당을 조정하는 데 사용할 수 있는 부호 있는 32비트 정수입니다.|0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|`Query`  \ `Concurrency`|double|큐에 한 번에 넣을 수 있는 스레드 수의 목표치를 설정하는 알고리즘을 결정하는 배정밀도 부동 소수점 값입니다.|2.0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.<br /><br /> Windows에서 IO 완료 포트를 사용해서 구현되는 동시성을 사용해서 스레드 풀이 초기화됩니다. 자세한 내용은 [I/O 완료 포트](https://msdn.microsoft.com/library/windows/desktop/aa365198\(v=vs.85\).aspx) 를 참조하세요.|  
|`Query` \ `GroupAffinity`|string|시스템의 프로세서 그룹에 해당하는 16진수 값 배열로, 각 프로세서 그룹의 논리적 프로세서에 대한 처리 스레드의 선호도를 설정하는 데 사용됩니다.|none|이 속성을 사용해서 사용자 지정 선호도를 만들 수 있습니다. 이 속성은 기본적으로 비어 있습니다.<br /><br /> 자세한 내용은 [GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정](#bkmk_groupaffinity) 를 참조하세요.|  
|`Query`  \ `MaxThreads`|ssNoversion|스레드 풀에 포함할 최대 스레드 수를 지정하는 부호 있는 32비트 정수입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본적으로 서버는 이 값을 절대값 10 또는 논리적 프로세서 수의 2배 중에서 큰 값으로 설정합니다. 예를 들어 하이퍼스레딩을 지원하는 4코어 시스템에서 최대 스레드 수는 16입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다. 예를 들어 논리적 프로세서가 32개인 서버에서 -10으로 설정된 경우 최대값은 320개의 스레드입니다.<br /><br /> 최대값은 이전에 정의한 사용자 지정 선호도 마스크당 사용 가능한 프로세서 수의 영향을 받습니다. 예를 들어 32개의 프로세서 중에서 8개를 사용하도록 스레드 풀 선호도를 이미 설정한 경우 MaxThreads를 -10으로 설정하면 스레드 풀의 상한이 10에 8을 곱한 80개의 스레드가 됩니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.<br /><br /> 스레드 풀 설정 튜닝에 대한 자세한 내용은 [Analysis  Services  작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx)에서 찾을 수 있습니다.|  
|`Query` \ `MinThreads`|ssNoversion|스레드 풀에 미리 할당할 최소 스레드 수를 지정하는 부호 있는 32비트 정수입니다.|0|0은 서버에서 기본값이 결정됨을 나타냅니다. 기본적으로 최소값은 1입니다.<br /><br /> 이 값을 음수 값으로 설정하는 경우 서버는 해당 값을 논리적 프로세서 수와 곱합니다.<br /><br /> 이 스레드 풀 속성에 사용되는 실제 값은 서비스 시작 시 msmdsrv 로그 파일에 기록됩니다.<br /><br /> 스레드 풀 설정 튜닝에 대한 자세한 내용은 [Analysis  Services  작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx)에서 찾을 수 있습니다.|  
|`Query` \ `PriorityRatio`|ssNoversion|우선 순위가 더 높은 큐가 비어 있지 않을 경우에도 우선 순위가 낮은 스레드가 가끔 실행되도록 보장하기 위해 사용할 수 있는 부호 있는 32비트 정수입니다.|2|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
|`Query`  \ `StackSizeKB`|ssNoversion|스레드 실행 중 메모리 할당을 조정하는 데 사용할 수 있는 부호 있는 32비트 정수입니다.|0|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.|  
  
##  <a name="bkmk_groupaffinity"></a> GroupAffinity를 설정하여 프로세서 그룹의 프로세서에 대한 스레드 선호도 설정  
 `GroupAffinity`는 고급 튜닝 목적으로 제공됩니다. `GroupAffinity` 속성을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 스레드 풀과 특정 프로세서 사이의 선호도를 설정할 수 있습니다.  그러나 대부분의 설치에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 사용 가능한 논리적 프로세서를 모두 사용할 때 성능이 가장 뛰어납니다. 따라서 그룹 선호도는 기본적으로 지정되지 않습니다.  
  
 성능 테스트에서 CPU 최적화가 필요한 것으로 나타날 경우 Windows Server 리소스 관리자를 사용해서 논리적 프로세서와 서버 프로세스 사이의 선호도를 설정하는 등 조금 더 고급스러운 접근 방식을 고려해야 할 수 있습니다. 이러한 접근 방식은 개별 스레드 풀에 대해 사용자 지정 선호도를 정의하는 것보다 구현 및 관리가 간단할 수 있습니다.  
  
 이 방법으로 충분하지 않을 경우에는 스레드 풀에 대해 사용자 지정 선호도를 정의하여 정밀도를 높일 수 있습니다. 너무 넓은 프로세서 범위로 분산되는 스레드 풀로 인해 성능이 저하되는 대형 다중 코어 시스템 (NUMA 또는 비 NUMA)에서 선호도 설정을 사용자 지정하는 것이 좋습니다. 논리적 프로세서가 64개 미만인 시스템에서도 `GroupAffinity`를 설정할 수 있지만 이 경우 성능 이점이 저하되고 오히려 성능이 감소할 수도 있습니다.  
  
> [!NOTE]  
>  `GroupAffinity`는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 사용하는 코어 수를 제한하는 버전에 따라 제약을 받습니다. 시작 시 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 버전 정보와 `GroupAffinity` 속성을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 관리되는 5개의 스레드 풀 각각에 대한 선호도 마스크를 컴퓨팅합니다. Standard Edition에서는 최대 16개의 코어를 사용할 수 있습니다. 16개를 초과하는 코어가 포함된 대형 다중 코어 시스템에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Standard Edition을 설치하는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 16개의 코어만 사용됩니다. 이전 버전의 Enterprise 인스턴스를 업그레이드하는 경우 20개의 코어로 제한됩니다. 버전 및 라이선스에 대한 자세한 내용은 [SQL Server 2012 라이선스 개요](https://go.microsoft.com/fwlink/?LinkId=246061)를 참조하세요.  
  
### <a name="syntax"></a>구문  
 값은 각 프로세서 그룹에 대한 16진수 값이며,  16진수는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 지정된 스레드 풀에 대해 스레드를 할당할 때 처음 사용하도록 시도하는 논리적 프로세서를 나타냅니다.  
  
 **논리적 프로세서에 대한 비트 마스크**  
  
 단일 프로세서 그룹 내에 최대 64개의 논리적 프로세서를 포함할 수 있습니다. 비트 마스크는 스레드 풀에서 사용되는(또는 사용되지 않는) 그룹의 각 논리적 프로세서에 대해 1(또는 0)입니다. 비트 마스크를 계산 계산한 다음에 16 진수 값에 대 한 값으로 `GroupAffinity`입니다.  
  
 **다중 프로세서 그룹**  
  
 프로세서 그룹은 시스템 시작 시에 결정됩니다. `GroupAffinity` 쉼표로 구분 된 목록의 각 프로세서 그룹에 대 한 16 진수 값을 허용합니다. 다중 프로세서 그룹(고성능 시스템의 경우 최대 10개)이 지정된 경우, 0x0을 지정하여 개별 그룹을 무시할 수 있습니다. 예를 들어 4개의 프로세서 그룹(0, 1, 2, 3)이 포함된 시스템에서는 첫 번째 및 세 번째 값에 대해 0x0을 입력하여 그룹 0 및 2를 제외할 수 있습니다.  
  
 `<GroupAffinity>0x0, 0xFF, 0x0, 0xFF</GroupAffinity>`  
  
### <a name="steps-for-computing-the-processor-affinity-mask"></a>프로세서 선호도 마스크 계산 단계  
 설정할 수 있습니다 `GroupAffinity` msmdsrv.ini에서 또는 SQL Server Management Studio에서 서버 속성 페이지에서.  
  
1.  **프로세서 및 프로세서 그룹 수 결정**  
  
     [winsysinternals에서 Coreinfo  유틸리티](https://technet.microsoft.com/sysinternals/cc835722.aspx)를 다운로드할 수 있습니다.  
  
     논리적 프로세서에서 그룹 맵 섹션으로 이 정보를 가져오려면 **coreinfo** 를 실행합니다. 각 논리적 프로세서에 대해 별도의 행이 생성됩니다.  
  
2.  오른쪽에서 왼쪽으로의 프로세서 순서: `7654 3210`  
  
     예제에는 프로세서가 8개(0~7)만 표시되지만 프로세서 그룹은 최대 64개의 논리적 프로세서를 포함할 수 있으며, 엔터프라이즈급 Windows 서버에는 최대 10개의 프로세서 그룹이 포함될 수 있습니다.  
  
3.  **사용하려는 프로세서 그룹에 대한 비트 마스크 계산**  
  
     `7654 3210`  
  
     논리적 프로세서를 제외 또는 포함시키려는지 여부에 따라 숫자를 0 또는 1로 바꿉니다. 8개 프로세서가 포함된 시스템에서는 Analysis Services에 대해 프로세서 7, 6, 5, 4 및 1을 사용하려고 한 것처럼 계산이 표시될 수 있습니다.  
  
     `1111 0010`  
  
4.  **이진 숫자를 16진수 값으로 변환**  
  
     계산기 또는 변환 도구를 사용해서 이진 숫자를 16진수 값으로 변환합니다. 이 예에서 `1111 0010` 은 `0xF2`로 변환됩니다.  
  
5.  **GroupAffinity 속성에 16진수 값을 입력합니다.**  
  
     Msmdsrv.ini에서 또는 Management Studio에서 서버 속성 페이지의 설정 `GroupAffinity` 4 단계에서 계산 된 값입니다.  
  
> [!IMPORTANT]  
>  설정 `GroupAffinity` 설정은 여러 단계가 포함 된 수동 작업입니다. 계산할 때 `GroupAffinity`, 계산을 신중 하 게 확인 합니다. 전체 마스크가 잘못된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 오류를 반환하지만 올바른 설정과 잘못된 설정이 조합된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 속성이 무시됩니다. 예를 들어 비트 마스크에 추가 값이 포함된 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 설정을 무시하고,  시스템에서 모든 프로세서를 사용합니다. 이 동작이 발생할 때 오류나 경고가 발생하지 않지만, msmdsrv.log 파일을 확인하여 선호도가 실제로 어떻게 설정되었는지 알아볼 수 있습니다.  
  
##  <a name="bkmk_pernumanode"></a> NUMA 노드에서 프로세서에 대한 IO 스레드 선호도를 설정하기 위한 PerNumaNode 설정  
 다차원 Analysis Services 인스턴스에 대해 설정할 수 있습니다 `PerNumaNode` 에 `IOProcess` 스레드 풀 스레드 예약 및 실행을 추가로 최적화할 합니다. 반면 `GroupAffinity` 는 지정 된 스레드 풀에 사용할 논리적 프로세서 집합을 식별 `PerNumaNode` 더 나아갑니다 허용된 된 논리적 프로세서의 일부 하위 집합으로 다중 스레드 풀을 만들지 여부를 지정 하 여 한 단계 더 이동 합니다.  
  
> [!NOTE]  
>  Windows Server 2012에서 작업 관리자를 사용하여 컴퓨터의 NUMA 노드 수를 확인할 수 있습니다. 작업 관리자의 성능 탭에서 **CPU** 를 선택한 다음 그래프 영역을 마우스 오른쪽 단추로 클릭하면 NUMA 노드 수가 표시됩니다. 또는 Windows  Sysinternals에서 Coreinfo  유틸리티를 [다운로드](https://technet.microsoft.com/sysinternals/cc835722.aspx) 하고 `coreinfo -n` 을 실행하여 NUMA  노드 수와 각 노드의 논리적 프로세서 수를 반환합니다.  
  
 에 대 한 유효한 값 `PerNumaNode` 에 설명 된 대로-1, 0, 1, 2, 되는 [스레드 풀 속성 참조](#bkmk_propref) 섹션을이 참조 합니다.  
  
### <a name="default-recommended"></a>기본값(권장)  
 NUMA 노드가 포함된 시스템에서는 기본 설정 PerNumaNode=-1을 사용해서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 노드 수에 따라 스레드 풀의 수와 스레드 선호도를 조정하도록 허용하는 것이 좋습니다. 시스템에 4 개 미만의 노드가 있으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 설명 된 동작을 구현 `PerNumaNode`= 0 `PerNumaNode`= 1은 4 개 이상의 노드가 포함 된 시스템에서 사용 합니다.  
  
### <a name="choosing-a-value"></a>값 선택  
 다른 유효한 값을 사용하기 위해 기본값을 재정의할 수도 있습니다.  
  
 **PerNumaNode=0 설정**  
  
 NUMA 노드가 무시됩니다. IOProcess 스레드 풀이 하나만 있고 이 스레드 풀의 모든 스레드는 모든 논리적 프로세서로 선호도가 설정됩니다. 기본적으로(PerNumaNode=-1) 이 설정은 컴퓨터에 4개 미만의 NUMA 노드가 있는 경우 작동 가능한 설정입니다.  
  
 ![Numa, 프로세서 및 스레드 풀로 대응](../media/ssas-threadpool-numaex0.PNG "Numa, 프로세서 및 스레드 풀로 대응")  
  
 **PerNumaNode=1 설정**  
  
 IOProcess 스레드 풀이 각 NUMA 노드에 대해 만들어집니다. 스레드 풀을 별도로 지정하면 NUMA 노드의 로컬 캐시와 같이 로컬 리소스에 대한 액세스 조정 성능이 향상됩니다.  
  
 ![Numa, 프로세서 및 스레드 풀로 대응](../media/ssas-threadpool-numaex1.PNG "Numa, 프로세서 및 스레드 풀로 대응")  
  
 **PerNumaNode=2 설정**  
  
 이 설정은 많은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 작업을 실행하는 고성능 시스템을 위한 설정입니다. 이 속성은 IOProcess 스레드 풀 선호도를 가장 세분화된 수준으로 설정해서 논리적 프로세서 수준에서 개별 스레드 풀을 만들고 선호도를 설정합니다.  
  
 다음 예제에서는에 포함 된 시스템에서 NUMA 노드 4 개와 논리적 프로세서가 32 개, 설정 `PerNumaNode` IOProcess 스레드 풀이 32 2로 발생 합니다. 처음 8개 스레드 풀의 스레드는 NUMA 노드 0의 모든 논리적 프로세서로 선호도가 설정되지만 이상적인 프로세서 설정은 0, 1, 2부터 최대 7까지입니다. 다음 8개 스레드 풀은 NUMA 노드 1의 모든 논리적 프로세서로 선호도가 설정되며, 이상적인 프로세서 설정은 8, 9, 10부터 최대 15까지입니다.  
  
 ![Numa, 프로세서 및 스레드 풀로 대응](../media/ssas-threadpool-numaex2.PNG "Numa, 프로세서 및 스레드 풀로 대응")  
  
 이러한 선호도 수준에서 스케줄러는 항상 선호되는 NUMA 노드 내에서 이상적인 논리적 프로세서를 먼저 사용하도록 시도합니다. 논리적 프로세서를 사용할 수 없으면, 스케줄러가 동일한 노드 내에서 또는 동일한 프로세서 그룹 내에서(다른 스레드를 사용할 수 없는 경우) 다른 프로세서를 선택합니다. 자세한 내용 및 예제를 보려면 [Analysis Services 2012 구성 설정(Wordpress 블로그)](https://go.microsoft.com/fwlink/?LinkId=330387)을 참조하세요.  
  
###  <a name="bkmk_workdistrib"></a> IOProcess 스레드 간 작업 분산  
 설정할지 여부를 고려할 때 합니다 `PerNumaNode` 속성을 알고 있으면 어떻게 `IOProcess` 스레드가 사용 되 도움이 될 수 있습니다 더 합리적인된 결정을 내릴 합니다.  
  
 이전에 설명한 대로 `IOProcess` 은 다차원 엔진에서 저장소 엔진 쿼리와 연관 된 IO 작업에 사용 됩니다.  
  
 세그먼트가 검색될 때 엔진은 세그먼트가 속한 파티션을 식별하고 해당 파티션이 사용하는 스레드 풀에 세그먼트 작업을 대기시키려고 합니다. 일반적으로 파티션에 속한 모든 세그먼트가 동일한 스레드 풀에 작업을 대기시킵니다. NUMA 시스템에서는 파티션에 대한 모든 검색에 NUMA 노드에 로컬로 할당되는 파일 시스템 캐시의 메모리가 사용되기 때문에 이 동작이 특히 유용합니다.  
  
 다음 시나리오에서는 경우에 따라 NUMA 시스템에서 쿼리 성능을 향상시킬 수 있는 조정 방법을 제안합니다.  
  
-   분할되지 않은(예를 들어 파티션이 하나뿐인) 측정값 그룹의 경우 파티션 수를 늘립니다. 파티션을 하나만 사용하면 엔진이 항상 하나의 스레드 풀(스레드 풀 0)에 작업을 대기시킵니다. 파티션을 더 추가하면 엔진이 추가 스레드 풀을 사용할 수 있습니다.  
  
     또는 추가 파티션을 만들 수 없으면, 시도 설정을 `PerNumaNode`스레드 풀 0에서 사용 가능한 스레드 수가 증가 하는 방법으로 = 0.  
  
-   어느 세그먼트 검사 균등 하 게 설정 하는 여러 파티션 간에 분산 됩니다 데이터베이스용 `PerNumaNode` 1 또는 2로 쿼리 성능을 높일 수는 전체 수가 증가 하기 때문에 `IOProcess` 스레드 풀 시스템에서 사용 합니다.  
  
-   포함 하는 솔루션에 대 한 여러 파티션이 있지만 하나만 많이 검색 되, 설정을 시도 `PerNumaNode`= 0으로 하는 경우 성능이 향상 됩니다.  
  
 파티션 검색과 차원 검색 사용 하 여 모두 있지만 `IOProcess` 스레드 풀을 차원 검색만 사용 하 여 스레드 풀 0입니다. 이로 인해 이 스레드 풀에서 약간 균등하지 않은 부하가 발생할 수 있지만, 일반적으로 차원 검색이 매우 빠르고 자주 발생하지 않으므로 이러한 불균형은 일시적입니다.  
  
> [!NOTE]  
>  서버 속성을 변경하는 경우 구성 옵션이 현재 인스턴스에서 실행되는 모든 데이터베이스에 적용됩니다. 가장 중요한 데이터베이스나 대다수의 데이터베이스에 유용한 설정을 선택하세요. 데이터베이스 수준에서 프로세서 선호도를 설정할 수 없으며 개별 파티션과 특정 프로세서 사이의 선호도를 설정할 수 없습니다.  
  
 작업 아키텍처에 대한 자세한 내용은 [SQL Server 2008 Analysis Services 성능 가이드](https://www.microsoft.com/download/details.aspx?id=17303)의 2.2 섹션을 참조하세요.  
  
##  <a name="bkmk_related"></a> 종속되었거나 관련된 속성  
 2\.4 섹션에 설명 된 대로 합니다 [Analysis Services 작업 가이드](https://msdn.microsoft.com/library/hh226085.aspx), 처리 스레드 풀을 늘리면 확인 해야 하는 합니다 `CoordinatorExecutionMode` 설정을 뿐만 `CoordinatorQueryMaxThreads` 설정 값이 있는 사용 증가 한 스레드 풀 크기를 충분히 활용할 수 있습니다.  
  
 Analysis Services는 처리 또는 쿼리 요청을 완료하는 데 필요한 데이터 수집을 위해 코디네이터 스레드를 사용합니다. 코디네이터는 각 파티션에 대해 먼저 처리되어야 하는 최대 1개의 작업을 큐에 넣습니다. 이러한 각 작업은 파티션에서 검색되어야 하는 총 세그먼트 수에 따라 계속해서 추가 작업을 큐에 넣습니다.  
  
 `CoordinatorExecutionMode`는 기본값이 코어당 병렬 처리 작업이 4개로 제한됨을 의미하는 -4이며,  저장소 엔진의 하위 큐브 요청에 의해 병렬로 실행할 수 있는 총 코디네이터 작업 수를 제한합니다.  
  
 `CoordinatorQueryMaxThreads`는 기본값이 16이며,  각 파티션에서 병렬로 실행될 수 있는 세그먼트 작업 수를 제한합니다.  
  
##  <a name="bkmk_currentsettings"></a> 현재 스레드 풀 설정 확인  
 각 서비스 시작 시 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 최소 및 최대 스레드,  프로세서 선호도 마스크 및 동시성을 포함하여 현재 스레드 풀 설정을 msmdsrv.log  파일로 출력합니다.  
  
 다음 예는 로그 파일에서 하이퍼스레딩이 지원되는 4코어 시스템에서 쿼리 스레드 풀의 기본 설정(MinThread=0, MaxThread=0, Concurrency=2)을 보여주는 일부를 가져온 것입니다. 선호도 마스크는 8개 논리적 프로세서를 나타내는 0xFF입니다. 여기에서는 마스크에 선행 0이 있는 것을 알 수 있습니다. 선행 0은 무시할 수 있습니다.  
  
 `"10/28/2013 9:20:52 AM) Message: The Query thread pool now has 1 minimum threads, 16 maximum threads, and a concurrency of 16.  Its thread pool affinity mask is 0x00000000000000ff. (Source: \\?\C:\Program Files\Microsoft SQL Server\MSAS11.MSSQLSERVER\OLAP\Log\msmdsrv.log, Type: 1, Category: 289, Event ID: 0x4121000A)"`  
  
 **MinThread** 및 **MaxThread** 설정을 위한 알고리즘에는 시스템 구성,  특히 프로세서 수가 포함됩니다. 다음 블로그 게시물에서는 이러한 값이 계산되는 방법에 대해 자세히 설명합니다. [Analysis Services 2012 구성 설정 (Wordpress 블로그)](https://go.microsoft.com/fwlink/?LinkId=330387)합니다. 이러한 설정 및 동작은 이후 릴리스에서의 조정에 따라 변경될 수 있습니다.  
  
 다음 목록에서는 다양한 프로세서 조합에 대한 다른 선호도 마스크 설정의 예를 보여 줍니다.  
  
-   8코어 시스템에서 프로세서 3-2-1-0에 대한 선호도 설정은 비트 마스크: 00001111, 및 16 진수 값: 0xF를 지정합니다.  
  
-   8 코어 시스템에서 프로세서 7-6-5-4에 대 한 선호도 비트이 마스크 발생합니다. 11110000, 및 16 진수 값: 0xF0을 지정합니다.  
  
-   8 코어 시스템에서 프로세서 5-4-3-2에 대 한 선호도 비트이 마스크 발생합니다. 00111100, 및 16 진수 값: 0x3C를 지정합니다.  
  
-   8 코어 시스템에서 프로세서 7-6-1-0에 대 한 선호도 비트이 마스크 발생합니다. 11000011 및 16 진수 값: 0xC3을 지정합니다.  
  
 다중 프로세서 그룹을 포함하는 시스템에서는 쉼표로 구분된 목록의 각 그룹에 대해 별도의 선호도 마스크가 생성됩니다.  
  
##  <a name="bkmk_msmdrsrvini"></a> MSMDSRV.INI 정보  
 msmdsrv.ini  파일은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 구성 설정을 포함하므로 해당 인스턴스에서 실행되는 모든 데이터베이스에 영향을 미칩니다. 다른 모든 데이터베이스를 제외하고 한 데이터베이스의 성능만 최적화하기 위해 서버 구성 속성을 사용할 수는 없습니다. 그러나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스를 여러 개 설치하고 유사한 특성이나 작업을 공유하는 데이터베이스에 유용한 속성을 사용하도록 각 인스턴스를 구성할 수 있습니다.  
  
 모든 서버 구성 속성은 msmdsrv.ini 파일에 포함되어 있습니다. 수정 가능성이 높은 속성 하위 집합은 SSMS와 같은 관리 도구에도 표시됩니다.  
  
 msmdsrv.ini  내용은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 테이블 형식 및 다차원 인스턴스 모두 동일합니다. 하지만 일부 설정은 한 가지 모드에만 적용됩니다. 서버 모드에 따른 동작의 차이는 속성 참조 설명서에서 확인할 수 있습니다.  
  
> [!NOTE]  
>  속성 설정 방법은 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [프로세스 및 스레드 정보](/windows/desktop/ProcThread/about-processes-and-threads)   
 [다중 프로세서](/windows/desktop/ProcThread/multiple-processors)   
 [프로세서 그룹](/windows/desktop/ProcThread/processor-groups)   
 [SQL Server 2012에서 Analysis Services 스레드 풀 변경](https://blogs.msdn.com/b/psssql/archive/2012/01/31/analysis-services-thread-pool-changes-in-sql-server-2012.aspx)   
 [Analysis Services 2012 구성 설정(Wordpress 블로그)](https://go.microsoft.com/fwlink/?LinkId=330387)   
 [프로세서가 64개를 초과하는 시스템 지원](https://msdn.microsoft.com/library/windows/hardware/gg463349.aspx)   
 [SQL Server 2008 R2 Analysis Services 작업 가이드](https://go.microsoft.com/fwlink/?LinkID=225539)  
  
  
