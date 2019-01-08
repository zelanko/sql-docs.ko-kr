---
title: 리소스 관리자 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, overview
- Resource Governor
ms.assetid: 2bc89b66-e801-45ba-b30d-8ed197052212
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d2cdad589ac9c669ae06672260bd99a1de72e8f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807315"
---
# <a name="resource-governor"></a>관리
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 관리자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 작업 및 시스템 리소스 소비량을 관리하는 데 사용할 수 있는 기능입니다. 리소스 관리자를 사용하면 들어오는 애플리케이션 요청이 사용할 수 있는 CPU, 물리적 IO 및 메모리 양을 제한할 수 있습니다.  
  
## <a name="benefits-of-resource-governor"></a>리소스 관리자의 이점  
 리소스 관리자를 사용하여 리소스 소비량에 대한 제한을 들어오는 요청별로 지정하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 작업과 리소스를 관리할 수 있습니다. 리소스 관리자 컨텍스트에서 작업이란 단일 엔터티로 취급해야 하거나 취급할 수 있는 비슷한 크기의 쿼리 또는 요청 집합입니다. 반드시 그래야 하는 것은 아니지만 작업의 리소스 사용 패턴이 균일할수록 리소스 관리자를 통해 얻을 수 있는 이점이 많아집니다. 리소스 제한은 실행 중인 작업에 미치는 영향을 최소화하면서 실시간으로 다시 구성할 수 있습니다.  
  
 같은 서버에 고유 작업이 여러 개 있는 환경에서 리소스 관리자를 사용하면 이러한 여러 작업을 구별할 수 있으며 지정한 제한에 따라 요청된 공유 리소스를 할당할 수 있습니다. CPU, 물리적 IO 및 메모리가 이러한 리소스에 해당합니다.  
  
 리소스 관리자를 사용하면 다음을 수행할 수 있습니다.  
  
-   여러 클라이언트 작업을 처리하는 단일 SQL Server 인스턴스에서 다중 테넌트 지원 및 리소스 격리를 제공합니다. 즉, 서버의 사용 가능한 리소스를 여러 작업으로 분산하여 작업 간 리소스 경합이 발생할 때 야기되는 문제를 최소화할 수 있습니다.  
  
-   다중 작업 및 다중 사용자 환경에서 작업 테넌트에 대한 예측 가능한 성능 및 지원 SLA를 제공합니다.  
  
-   IO 하위 시스템을 포화 상태로 만들어 다른 작업의 성능을 저하시킬 수 있는 DBCC CHECKDB 등의 작업에 대해 IO 리소스를 제한하거나 런어웨이 쿼리를 격리 및 제한합니다.  
  
-   리소스 사용 비용 환불을 위한 세분화된 리소스 추적 기능을 추가하고 서버 리소스 소비자에게 예측 가능한 요금 청구 기능을 제공합니다.  
  
## <a name="resource-governor-constraints"></a>리소스 관리자 제약 사항  
 이 리소스 관리자 릴리스의 제약 사항은 다음과 같습니다.  
  
-   리소스 관리가 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]으로 제한되며 리소스 관리자를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 사용할 수 없습니다.  
  
-   SQL Server 인스턴스 간 작업 모니터링 또는 작업 관리가 없습니다.  
  
-   리소스 관리자는 OLTP 작업을 관리할 수는 있지만 이러한 유형의 쿼리는 일반적으로 지속 시간이 매우 짧으므로 대역폭 제어를 적용할 수 있을 정도로 오래 CPU에 항상 상주하지 않습니다. 이로 인해 CPU 사용량(%)으로 반환되는 통계가 왜곡될 수 있습니다.  
  
-   물리적 IO 관리 기능은 사용자 작업에만 적용되고 시스템 태스크에는 적용되지 않습니다. 시스템 태스크에는 트랜잭션 로그에 대한 쓰기 작업 및 지연 기록기 IO 작업이 포함됩니다. 대부분의 쓰기 작업은 일반적으로 시스템 태스크에 의해 수행되므로 리소스 관리자는 주로 사용자 읽기 작업에 적용됩니다.  
  
-   내부 리소스 풀에 대해서는 IO 임계값을 설정할 수 없습니다.  
  
## <a name="resource-concepts"></a>리소스 개념  
 다음은 리소스 관리자를 이해하고 사용하기 위한 세 가지 기본 개념입니다.  
  
-   **리소스 풀** 리소스 풀은 서버의 물리적 리소스를 나타냅니다. 풀은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 내부의 가상 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴트로 간주할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하면 두 개의 리소스 풀(내부 및 기본)이 만들어집니다. 또한 리소스 관리자는 사용자 정의 리소스 풀을 지원합니다. 자세한 내용은 [Resource Governor Resource Pool](resource-governor-resource-pool.md)을(를) 참조하세요.  
  
-   **작업 그룹** 작업 그룹은 분류 기준이 유사한 세션 요청에 대한 컨테이너의 역할을 합니다. 작업 그룹을 사용하면 세션의 집계 모니터링이 가능하며 작업 그룹으로 세션의 정책을 정의할 수 있습니다. 각 작업 그룹은 리소스 풀에 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치하면 두 개의 작업 그룹(내부 및 기본)이 만들어지고 해당 리소스 풀에 매핑됩니다. 또한 리소스 관리자는 사용자 정의 작업 그룹을 지원합니다. 자세한 내용은 [Resource Governor Workload Group](resource-governor-workload-group.md)를 참조하세요.  
  
-   **분류** 분류 프로세스는 세션 특징에 기초하여 들어오는 세션을 작업 그룹에 할당합니다. 분류자 함수라고 하는 사용자 정의 함수를 작성하여 원하는 분류 논리를 지정할 수 있습니다. 또한 리소스 관리자는 분류 규칙을 구현하는 분류자 사용자 정의 함수를 지원합니다. 자세한 내용은 [Resource Governor Classifier Function](resource-governor-classifier-function.md)을(를) 참조하세요.  
  
> [!NOTE]  
>  리소스 관리자는 DAC(관리자 전용 연결)를 제어하지 않습니다. 내부 작업 그룹과 리소스 풀에서 실행되는 DAC 쿼리는 분류할 필요가 없습니다.  
  
 리소스 관리자의 컨텍스트에서는 위의 개념이 구성 요소로 간주될 수 있습니다. 다음 그림에서는 이러한 구성 요소와 이러한 구성 요소가 데이터베이스 엔진 환경에 있을 때 서로 어떤 관계가 있는지를 보여 줍니다. 처리 측면에서 이 흐름은 다음과 같이 요약할 수 있습니다.  
  
-   세션에 대한 들어오는 연결(세션 1/ *n*)이 있습니다.  
  
-   세션이 분류됩니다(분류).  
  
-   세션 작업이 작업 그룹(예: 그룹 4)으로 라우팅됩니다.  
  
-   작업 그룹이 관련 리소스 풀(예: 풀 2)을 사용합니다.  
  
-   리소스 풀이 애플리케이션(예: 애플리케이션 3)에 필요한 리소스를 제공하고 제한합니다.  
  
 ![리소스 관리자 기능 구성 요소](../../database-engine/media/rg-basic-funct-components.gif "Resource Governor Functional Components")  
  
## <a name="resource-governor-tasks"></a>리소스 관리자 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|리소스 관리자를 사용하도록 설정하는 방법에 대해 설명합니다.|[리소스 관리자 사용](resource-governor.md)|  
|리소스 관리자를 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[리소스 관리자 사용 안 함](disable-resource-governor.md)|  
|리소스 풀의 생성, 수정 및 삭제 방법에 대해 설명합니다.|[리소스 관리자 리소스 풀](resource-governor-resource-pool.md)|  
|작업 그룹의 생성, 수정, 이동 및 삭제 방법에 대해 설명합니다.|[리소스 관리자 작업 그룹](resource-governor-workload-group.md)|  
|분류자 사용자 정의 함수를 만들고 테스트하는 방법에 대해 설명합니다.|[리소스 관리자 분류자 함수](resource-governor-classifier-function.md)|  
|템플릿을 사용하여 리소스 관리자를 구성하는 방법에 대해 설명합니다.|[템플릿을 사용하여 리소스 관리자 구성](configure-resource-governor-using-a-template.md)|  
|리소스 관리자의 속성을 보는 방법에 대해 설명합니다.|[리소스 관리자 속성 보기](view-resource-governor-properties.md)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 인스턴스&#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
