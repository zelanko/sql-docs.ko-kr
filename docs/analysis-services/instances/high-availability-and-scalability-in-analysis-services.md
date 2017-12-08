---
title: "고가용성 및 Analysis Services의 확장성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7040a55-1e4d-4c24-9333-689c1b9e2db8
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7d6b6f6fa02735de056b83a3ec0216cd95c84926
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="high-availability-and-scalability-in-analysis-services"></a>Analysis Services의 고가용성 및 확장성
  이 문서에서는 Analysis Services 데이터베이스를 항상 사용 가능하고 확장 가능하도록 만드는 가장 일반적으로 사용되는 기술을 설명합니다. 각 목표를 개별적으로 다룰 수 있지만 실제로는 연관된 경우가 많습니다. 대규모 쿼리 또는 처리 워크로드에 대한 확장 가능한 배포는 일반적으로 고가용성에 대한 기대와 함께 제공됩니다.  
  
 그러나 반대의 경우는 그렇지 않을 때도 있습니다. 업무에 중요하지만 적절한 규모의 쿼리 워크로드에 대해 엄격한 서비스 수준 계약이 존재하는 경우에는 확장 없이 고가용성이 단독 목표일 수 있습니다.  
  
 Analysis Services를 항상 사용 가능하고 확장 가능하게 만드는 기술은 모든 서버 모드(다차원, 테이블 형식 및 SharePoint 통합 모드)에 대해 동일한 경향이 있습니다. 다른 설명이 없는 경우, 이 문서의 정보는 모든 모드에 적용되는 것으로 가정해야 합니다.  
  
## <a name="key-points"></a>요점  
 가용성 및 확장 기술은 관계형 데이터베이스 엔진에 대한 기술과 다르기 때문에 Analysis Services에서 사용되는 기술을 소개하는 데 다음과 같은 요점이 유용합니다.  
  
-   Analysis Services에서는 Windows server 플랫폼에 기본 제공되는 고가용성 및 확장성 메커니즘(NLB(네트워크 부하 분산), Window Server 장애 조치(failover) 클러스터링 또는 둘 다)을 활용합니다.  
  
    > [!NOTE]  
    >  관계형 데이터베이스 엔진의 AlwaysOn 기능은 Analysis Services로 확장되지 않습니다.  Analysis Services 인스턴스는 AlwaysOn 가용성 그룹에서 실행되도록 구성할 수 없습니다.  
    >   
    >  Analysis Services는 AlwaysOn 가용성 그룹에서 실행되지 않더라도 AlwaysOn 관계형 데이터베이스에서 데이터를 검색하고 처리할 수 있습니다. Analysis Services에서 사용할 수 있도록 항상 사용 가능한 관계형 데이터베이스를 구성하는 방법은 [Always On 가용성 그룹이 포함된 Analysis Services](../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)를 참조하세요.  
  
-   단독 목표로서의 고가용성은 장애 조치(failover) 클러스터의 서버 중복성을 통해 달성할 수 있습니다. 대체 노드는 하드웨어 및 소프트웨어 구성이 활성 노드와 동일한 것으로 간주됩니다.  WSFC는 자체적으로 확장 없이 고가용성을 제공합니다.  
  
-   가용성을 포함하거나 포함하지 않는 확장성은 읽기 전용 데이터베이스에 대한 NLB를 통해 달성됩니다.  확장성은 일반적으로 쿼리 볼륨이 크거나 급증할 수 있는 경우에 문제가 됩니다.  
  
     여러 읽기 전용 데이터베이스와 결합된 부하 분산은 확장성과 고가용성을 둘 다 제공합니다. 모든 노드가 활성 상태이므로 서버가 중단된 경우 나머지 노드로 요청이 자동으로 재배포됩니다. 확장성과 가용성이 둘 다 필요한 경우 NLB 클러스터를 사용하는 것이 좋습니다.  
  
 처리의 경우에는 고가용성 및 확장성 목표가 문제가 되지 않습니다. 작업의 일정 및 범위를 사용자가 제어하기 때문입니다. 처리는 모델의 일부분에 걸쳐 부분적이고 증분적일 수 있습니다. 다만, 일부 시점에서는 모든 인덱스와 집계에서 데이터 일관성을 유지하기 위해 단일 서버에서 모델을 전체적으로 처리해야 합니다. 확장 가능한 강력한 아키텍처는 어떤 흐름에서든 전체 처리를 수용할 수 있는 하드웨어에 의존합니다. 대규모 솔루션의 경우 이 작업은 자체 하드웨어 리소스를 통해 독립된 작업으로 구조화됩니다.  
  
##  <a name="bkmk_serverconfig"></a> 단일 및 다중 서버 구성  
 일반적인 단일 서버 배포에서는 시스템 리소스가 두 활동 모두에 충분한 것으로 가정하여 처리 및 쿼리 워크로드가 동시에 실행됩니다. Analysis Services는 업데이트된 버전이 백그라운드에서 처리되는 동안 쿼리 지원을 위해 기존 데이터 구조를 그대로 유지합니다. 임시 데이터 구조를 처리할 수 있는 충분한 메모리 및 디스크 공간을 유지하는 것은 모든 서버 모드의 하드웨어 요구 사항입니다. 다만, 모드마다 시스템 리소스 수요는 서로 다르며, 각 모드는 서로 다른 NUMA 인식 수준으로 제공됩니다.  
  
 **단일 서버 및 확장성**  
  
 고사양의 단일 다중 코어 서버는 자체적으로 충분한 확장성을 제공할 수 있습니다. 코어 수, RAM 및 디스크 공간이 많은 고사양 시스템에서는 잠재적으로 단일 시스템 내에서 확장할 수 있습니다.  
  
 다차원 데이터베이스의 경우 서버 구성 속성을 조정하여 프로세스와 프로세서 간의 선호도 만들 수 있습니다. 자세한 내용은 [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) 을 참조하세요.  
  
 **다중 서버 배포**  
  
 운영상, 여러 서버를 사용해야 하는 경우가 있습니다. 예를 들어 장애 조치(failover) 클러스터는 각 노드가 동일한 하드웨어 및 소프트웨어 구성에서 실행되는 다중 서버로 정의됩니다.  
  
 마찬가지로, 쿼리 워크로드의 고가용성에 대한 요구 사항이 중요한 경우에도 일반적으로 여러 서버가 필요합니다. 이 시나리오에서 Analysis Services에 권장되는 구성은 전용 하드웨어에서 별도 Analysis Services 인스턴스에서 실행되는 읽기 전용 및 읽기/쓰기 데이터베이스를 사용하는 것입니다. 읽기 전용 데이터베이스는 쿼리 요청을 처리합니다. 읽기/쓰기 데이터베이스는 처리에 사용됩니다. 이 자주 사용되는 기술에 대한 확장된 설명은 다음 섹션에 나와 있습니다.  
  
 **가상 컴퓨터 및 고가용성**  
  
 고가용성 요구 사항을 충족하기 위한 또 다른 전략에는 가상 컴퓨터의 사용이 포함될 수 있습니다. 가용성을 충족하기 위해 대체 서버를 설치하는 데 몇 분이 아니라 몇 시간이 걸리는 경우 요청 시 시작하고 중앙 위치에서 검색되는 업데이트된 데이터베이스와 함께 로드할 수 있는 가상 컴퓨터를 사용할 수 있습니다.  
  
## <a name="scalability-using-read-only-and-read-write-databases"></a>읽기 전용 및 읽기/쓰기 데이터베이스를 통한 확장성  
 네트워크 부하 분산은 쿼리 및 처리 워크로드가 높거나 상승하는 경우에 권장됩니다. NLB 솔루션의 Analysis Services 데이터베이스는 쿼리 간의 일관성을 위해 읽기 전용 데이터베이스로 정의됩니다.  
  
 [읽기 전용 데이터베이스를 사용하여 Analysis Services에 대한 쿼리 확장](https://technet.microsoft.com/library/ff795582\(v=sql.100\).aspx) (2008에 게시)의 참고 자료는 오래되었지만 여전히 일반적으로 유효합니다. 서버 운영 체제 및 컴퓨터 하드웨어가 진화하여 특정 플랫폼에 대한 참조 및 CPU 제한이 더 이상 사용되지 않지만 읽기 전용 및 읽기/쓰기 데이터베이스를 대용량 쿼리에 사용하는 기본 기술은 변경되지 않습니다.  
  
 이 접근 방식은 다음과 같이 요약될 수 있습니다.  
  
-   전용 하드웨어 및 Analysis Services의 인스턴스를 사용하여 데이터베이스를 처리합니다. 처리가 완료된 후 데이터베이스를 읽기 전용으로 설정합니다. 방법을 보려면 [Switch an Analysis Services database between ReadOnly and ReadWrite modes](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) 을 참조하세요.  
  
-   동일한 여러 쿼리 서버를 사용하여 동일한 읽기 전용 Analysis Services 데이터베이스의 복사본을 실행합니다. 서버는 클러스터의 단일 진입점 역할을 하는 하나의 가상 서버 이름을 통해 액세스할 수 있는 NLB 클러스터에 배포됩니다.  
  
-   Robocopy를 사용하여 처리 서버에서 각 쿼리 서버로 전체 데이터 디렉터리를 복사하고 읽기 전용 모드의 동일한 데이터베이스를 모든 쿼리 서버에 연결합니다. 또한 SAN 스냅숏, 동기화 또는 프로덕션 데이터베이스를 이동하는 데 사용되는 기타 모든 도구 또는 방법을 사용할 수 있습니다.  
  
## <a name="resource-demands-for-tabular-and-multidimensional-workloads"></a>테이블 형식 및 다차원 워크로드에 대한 리소스 요구  
 다음 표에는 Analysis Services에서 쿼리 및 처리에 시스템 리소스를 사용하는 방법이 서버 모드 및 저장소별로 요약되어 있습니다. 이 요약을 통해 분산 워크로드를 처리하는 다중 서버 배포에서 강조할 항목을 이해할 수 있습니다.  
  
|||  
|-|-|  
|**서버 및 저장소 모드**|**시스템 리소스에 미치는 영향**|  
|메모리 내 테이블 형식(기본값) - 메모리 내 데이터 구조의 테이블 검색으로 쿼리가 실행됩니다.|RAM 및 CPU의 빠른 클럭 속도를 강조합니다.|  
|DirectQuery 모드의 테이블 형식 - 쿼리가 백 엔드 관계형 데이터베이스 서버에 오프로드되고 처리가 모델에서 메타데이터를 생성하는 것으로 제한됩니다.|관계형 데이터베이스 성능, 네트워크 대기 시간 단축 및 처리량 극대화에 중점을 둡니다. CPU 속도가 빠르면 Analysis Services 쿼리 프로세서의 성능도 향상됩니다.|  
|MOLAP 저장소를 사용하는 다차원 모델|신속한 데이터 로드를 위한 디스크 IO및 캐시된 데이터에 충분한 RAM을 수용하는 부하 분산된 구성을 선택합니다.|  
|ROLAP 저장소를 사용하는 다차원 모델|디스크 IO를 최대화하고 네트워크 대기 시간을 최소화합니다.|  
  
## <a name="highly-availability-and-redundancy-through-wsfc"></a>WSFC를 통한 고가용성 및 중복성  
 Analysis Services를 기존 WSFC(Windows Server 장애 조치(failover) 클러스터)에 설치하여 가장 짧은 시간 내에 서비스를 복원하는 고가용성을 달성할 수 있습니다.  
  
 장애 조치(failover) 클러스터는 데이터베이스에 대한 모든 액세스 권한(읽기 및 쓰기 저장)을 제공하지만 한 번에 하나의 노드만 지원합니다. 첫 번째 노드가 중단된 경우 보조 데이터베이스가 클러스터의 추가 노드에서 대체 서버로 실행됩니다.  
  
 장애 조치(failover) 클러스터링의 주요 이점은 서비스 오류로부터의 빠른 복구입니다. 이러한 이점은 특정 제한 사항과 함께 제공됩니다. 첫째, 장애 조치(failover)가 필요 없는 경우 클러스터의 전용 리소스가 유휴 상태입니다. 둘째, 장애 조치(failover) 시 모든 연결이 손실되므로 커밋되지 않은 작업이 손실됩니다. 대부분의 클라이언트 응용 프로그램은 이 상황을 처리할 수 있어야 합니다. 종종 응용 프로그램의 새로 고침 단추를 누르면 결과가 원래대로 다시 돌아갑니다. 
 
 WSFC를 고려할 때 다음 사항을 유의해야 합니다.

- 활성/활성은 현재 지원되지 않습니다. 활성/수동(장애 조치(failover))은 Analysis Services에 대해 지원되는 유일한 WSFC 구성입니다.
- Analysis Services를 클러스터링할 때 클러스터에 참여하는 노드가 동일하거나 매우 비슷한 하드웨어에서 실행되는지, 그리고 각 노드의 운영 컨텍스트가 운영 체제 버전 및 서비스 팩, Analysis Services 버전 및 서비스 팩(또는 누적 업데이트), 서버 모드 면에서 동일한지 확인해야 합니다.
- 다른 작업의 활성 노드인 수동 노드는 용도를 변경하지 마세요. 노드에서 두 작업을 처리할 수 없는 경우 실제 장애 조치(failover) 상황에서 짧은 시간 동안 컴퓨터를 사용할 수 없게 됩니다.
 
 장애 조치(failover) 클러스터에서 Analysis Services를 배포하는 방법에 대한 자세한 지침 및 배경 정보는 [SQL Server Analysis Services 클러스터링 방법](https://msdn.microsoft.com/library/dn736073.aspx)을 참조하세요. 이 지침은 SQL Server 2012용으로 작성되었지만 최신 버전의 Analysis Services에도 계속 적용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 데이터베이스 동기화](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Analysis Services 테이블 형식 데이터베이스에 대 한 NUMA 선호도 강제 적용](https://blogs.msdn.microsoft.com/sqlcat/2013/11/05/forcing-numa-node-affinity-for-analysis-services-tabular-databases/)   
 [Analysis Services 사례 연구: 대규모 상용 솔루션에서 테이블 형식 모델 사용](https://msdn.microsoft.com/library/dn751533.aspx)  
  
  
