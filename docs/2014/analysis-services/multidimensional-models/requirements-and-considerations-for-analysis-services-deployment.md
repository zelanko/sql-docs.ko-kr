---
title: 요구 사항 및 고려 사항 분석을 위해 서비스 배포 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6759c38aa519979bdf05ba8848aaccbb89f37a94
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376925"
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Analysis Services 배포에 대한 요구 사항 및 고려 사항
  솔루션의 성능과 가용성은 기본 하드웨어의 기능, 서버 배포 토폴로지, 해당 솔루션의 특성(예: 여러 서버에 분산된 파티션을 갖는가 또는 관계형 엔진에 직접 액세스해야 하는 ROLAP 저장소를 사용하는가), SLA(서비스 수준 계약) 및 데이터 모델의 복잡성을 포함하여 여러 요인에 따라 달라질 수 있습니다.  
  
## <a name="memory-and-processor-requirements"></a>메모리 및 프로세서 요구 사항  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 더 많은 메모리와 프로세서 리소스가 필요합니다.  
  
-   크거나 복잡한 큐브를 처리할 경우. 이러한 큐브에는 작거나 간단한 큐브보다 더 많은 메모리와 프로세서 리소스가 필요합니다.  
  
-   단일 데이터베이스 내의 큐브 수가 증가할 경우  
  
-   단일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 내의 데이터베이스 수가 늘어날 경우  
  
-   단일 컴퓨터의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 수가 증가할 경우  
  
-   동시에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 리소스에 액세스하는 사용자 수가 늘어날 경우  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용할 수 있는 메모리와 프로세서 리소스의 양은 SQL Server 버전, 운영 체제, 하드웨어 용량 및 가상 또는 물리 프로세서를 사용 중인지 여부에 따라 달라집니다. 자세한 내용은 다음 링크를 참조하십시오.  
  
 [SQL Server 2014 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [SQL Server의 버전별 계산 용량 제한](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [SQL Server 2014 버전에서 지원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
 [최대 용량 사양&#40;Analysis Services&#41;](olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>디스크 공간 요구 사항  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구성 요소와 개체 처리 관련 태스크에 따라 필요한 디스크 공간이 다릅니다. 다음 목록에서는 이러한 요구 사항을 설명합니다.  
  
 큐브  
 큰 팩트 테이블이 있는 큐브에는 작은 팩트 테이블이 있는 큐브보다 더 많은 디스크 공간이 필요합니다. 마찬가지로 팩트 테이블에 비해 정도는 적지만 큰 차원이 많이 있는 큐브에는 보다 작은 차원 멤버가 있는 큐브보다 더 많은 디스크 공간이 필요합니다. 일반적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에는 기본 관계형 데이터베이스에 동일 데이터를 저장하는 데 필요한 공간의 약 20%가 필요합니다.  
  
 Aggregations  
 집계 필요한 추가 집계에 비례하여 추가 공간이 집계가 많을, 더 많은 공간이 필요 합니다. 필요 없는 집계를 만들지 않으려면 집계에 필요한 추가 디스크 공간이 대체로 기본 관계형 데이터베이스에 저장되는 데이터 크기의 약 10% 이하여야 합니다.  
  
 데이터 마이닝  
 기본적으로 마이닝 구조는 학습에 사용된 데이터 세트를 디스크에 캐시합니다. 마이닝 구조 개체에서 **구조 지우기 처리** 처리 옵션을 사용하여 디스크에서 이 캐시된 데이터를 제거할 수 있습니다. 자세한 내용은 [처리 요구 사항 및 고려 사항&#40;데이터 마이닝&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md)을 참조하세요.  
  
 개체 처리  
 처리 과정에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 처리가 완료될 때까지 처리 트랜잭션에서 처리 중인 개체의 복사본을 디스크에 저장합니다. 처리가 완료되면 원래 개체가 개체의 처리된 복사본으로 바뀝니다. 따라서 각 개체의 복사본을 처리하기 위해서는 충분한 추가 디스크 공간이 있어야 합니다. 예를 들어 단일 트랜잭션에서 전체 큐브를 처리하려면 전체 큐브의 복사본을 저장하기에 충분한 하드 디스크 공간이 있어야 합니다.  
  
##  <a name="BKMK_Availability"></a> 가용성 고려 사항  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 환경에서 하드웨어나 소프트웨어 장애 때문에 큐브나 마이닝 모델을 쿼리에 사용할 수 없는 경우가 있습니다. 큐브를 처리해야 하기 때문에 사용할 수 없는 경우도 있습니다.  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>하드웨어나 소프트웨어 장애 발생 시 가용성 제공  
 다양한 이유로 하드웨어나 소프트웨어 장애가 발생할 수 있습니다. 그러나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 가용성을 유지하는 작업은 장애 원인을 찾아내서 문제를 해결하는 작업인 동시에 오류 발생 시 사용자가 시스템을 계속 사용할 수 있도록 대체 리소스를 제공하는 작업이기도 합니다. 하드웨어나 소프트웨어 장애 발생 시 대개 서버 클러스터링과 로드 균형 조정을 사용하여 가용성을 유지하는 데 필요한 대체 리소스를 제공합니다.  
  
 하드웨어나 소프트웨어 장애 발생 시 가용성을 제공하려면 장애 조치 클러스터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 배포해 봅니다. 장애 조치 클러스터에서 어떤 이유로든 주 노드에 장애가 발생하거나 주 노드를 다시 부팅해야 할 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 클러스터링이 보조 노드로 장애 조치합니다. 장애 조치는 매우 빠르게 수행되며 이후부터 쿼리를 실행하는 사용자는 보조 노드에서 실행되고 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 액세스하게 됩니다. 장애 조치 클러스터에 대 한 자세한 내용은 참조 하세요. [Windows Server 기술:  장애 조치 클러스터](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)합니다.  
  
 가용성 문제를 해결하는 또 다른 방법은 둘 이상의 프로덕션 서버에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포하는 것입니다. 그런 다음 Windows 서버의 네트워크 로드 균형 조정(NLB) 기능을 사용하여 이러한 프로덕션 서버를 단일 클러스터로 결합할 수 있습니다. NLB 클러스터에서 하드웨어나 소프트웨어 문제로 인해 클러스터의 서버를 사용할 수 없으면 NLB 서비스가 사용 가능한 서버로 사용자 쿼리를 보냅니다.  
  
### <a name="providing-availability-while-processing-structural-changes"></a>구조 변경 처리 시 가용성 제공  
 큐브의 특정 변경 내용으로 인해 큐브가 처리될 때까지 해당 큐브를 사용할 수 없는 경우가 있습니다. 예를 들어 큐브에 있는 차원의 구조를 변경하면 차원을 다시 처리해야 할 뿐 아니라 수정된 차원을 사용하는 각 큐브도 처리해야 합니다. 이러한 큐브를 처리할 때까지 사용자는 해당 큐브를 쿼리하거나 수정된 차원이 있는 큐브를 기반으로 하는 마이닝 모델을 쿼리할 수 없습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 하나 이상의 큐브에 영향을 줄 수 있는 구조 변경 내용을 처리하는 동안 가용성을 제공하려면 준비 서버를 통합하고 데이터베이스 동기화 마법사를 사용해 봅니다. 이 기능을 사용하면 준비 서버에서 데이터와 메타데이터를 업데이트한 다음 프로덕션 서버와 준비 서버(staging server)의 온라인 동기화를 수행할 수 있습니다. 자세한 내용은 [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md)을(를) 참조하세요.  
  
 원본 데이터에 대한 증분 업데이트를 투명하게 처리하려면 자동 관리 캐싱을 사용합니다. 자동 관리 캐싱은 수동 처리 없이 큐브 가용성에 영향을 주지 않고 새 원본 데이터로 큐브를 업데이트합니다. 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.  
  
##  <a name="BKMK_Scalability"></a> 확장성 고려 사항  
 한 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 여러 개 있으면 성능 문제가 발생할 수 있습니다. 이러한 문제를 해결하는 방법 중 하나는 서버의 프로세서, 메모리 및 디스크 리소스를 늘리는 것입니다. 그러나 여러 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 확장해야 할 수도 있습니다.  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>여러 컴퓨터에 Analysis Services 확장  
 여러 컴퓨터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 확장하는 방법은 다양합니다. 다음 목록에서는 이러한 방법에 대해 설명합니다.  
  
-   한 컴퓨터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 여러 개 있으면 하나 이상의 인스턴스를 다른 컴퓨터로 이동할 수 있습니다.  
  
-   한 컴퓨터에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스가 여러 개 있으면 하나 이상의 데이터베이스를 다른 컴퓨터에 있는 자체 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스로 이동할 수 있습니다.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 데이터를 제공하는 관계형 데이터베이스가 여러 개 있으면 이러한 데이터베이스를 다른 컴퓨터로 이동할 수 있습니다. 데이터베이스를 이동하기 전에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스와 해당 기본 데이터베이스 간의 네트워크 속도와 대역폭을 고려합니다. 네트워크가 느리거나 혼잡한 경우 기본 데이터베이스를 다른 컴퓨터로 이동하면 처리 성능이 저하됩니다.  
  
-   처리에는 쿼리 성능에 영향을 감소 쿼리 로드의 시간 동안 처리할 수 없습니다. 하지만 경우 스테이징 서버에 처리 태스크를 이동한 다음 프로덕션 서버와 스테이징 서버의 온라인 동기화를 수행할 것이 좋습니다. 자세한 내용은 [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md)을(를) 참조하세요. 원격 파티션을 사용하여 여러 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 처리를 분산할 수도 있습니다. 원격 파티션 처리에는 로컬 컴퓨터의 리소스 대신 원격 서버의 프로세서와 메모리 리소스가 사용됩니다. 원격 파티션 관리에 대한 자세한 내용은 [원격 파티션 만들기 및 관리&#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)를 참조하세요.  
  
-   쿼리 성능이 나쁘지만 로컬 서버의 프로세서와 메모리 리소스를 늘릴 수 없으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 둘 이상의 프로덕션 서버에 배포해 봅니다. 그런 다음 NLB를 사용하여 서버를 단일 클러스터로 결합할 수 있습니다. NLB 클러스터에서 쿼리는 NLB 클러스터에 속한 모든 서버에 자동으로 분산됩니다.  
  
  
