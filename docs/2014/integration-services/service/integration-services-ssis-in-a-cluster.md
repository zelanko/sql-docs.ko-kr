---
title: 클러스터의 Integration Services(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a918816d8fd90624b625ed6107bbdc5e86b2cc08
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250463"
---
# <a name="integration-services-ssis-in-a-cluster"></a>클러스터의 Integration Services(SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 클러스터형 또는 클러스터 인식형 서비스가 아니며 클러스터 노드 간 장애 조치(failover) 기능을 지원하지 않으므로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 클러스터링이 권장되지 않습니다. 따라서 클러스터형 환경에서는 클러스터의 노드마다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치하고 독립 실행형 서비스로 시작해야 합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 클러스터형 서비스가 아니지만 클러스터의 각 노드에 별도로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 를 설치한 후 이러한 서비스가 클러스터 리소스로 작동하도록 수동으로 구성할 수 있습니다.  
  
 그러나 클러스터형 하드웨어 환경 설정의 목표가 고가용성인 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성하지 않고도 이러한 목표를 달성할 수 있습니다.  클러스터 노드의 패키지를 클러스터의 다른 노드에서 관리하려면 클러스터의 각 노드에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 구성 파일을 수정합니다. 이러한 각 구성 파일을 수정하여 패키지가 저장되어 있는 모든 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 가리키도록 할 수 있습니다. 이렇게 하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성할 때 발생할 수 있는 문제를 방지하고 대부분의 고객이 원하는 고가용성을 제공할 수 있습니다. 구성 파일을 변경하는 방법에 대한 자세한 내용은 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](integration-services-service-ssis-service.md)을 참조하세요.  
  
 클러스터형 환경에서 서비스를 구성하는 방법을 합리적으로 결정하려면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 역할을 이해하는 것이 중요합니다. 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](integration-services-service-ssis-service.md)를 참조하세요.  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>Integration Services를 클러스터 리소스로 구성할 경우의 단점 이해  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 클러스터 리소스로 구성할 경우 단점은 다음과 같습니다.  
  
-   장애 조치(failover)가 수행될 경우 실행 중인 패키지가 다시 시작되지 않습니다. 검사점에서 패키지를 다시 시작하면 패키지 오류를 복구할 수 있습니다. 서비스를 클러스터 리소스로 구성하지 않고 검사점부터 다시 시작할 수 있습니다. 자세한 내용은 [검사점을 사용하여 패키지 다시 시작](../packages/restart-packages-by-using-checkpoints.md)을 참조하세요.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 리소스 그룹에 구성하는 경우 클라이언트 컴퓨터에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 msdb 데이터베이스에 저장된 패키지를 관리할 수 없습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 이러한 이중 홉 시나리오에서 자격 증명을 위임할 수 없습니다.  
  
-   클러스터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 포함된 여러 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 리소스 그룹이 있는 경우 장애 조치(failover)로 인해 예기치 않은 결과가 발생할 수 있습니다. 다음과 같은 시나리오를 고려해 보십시오. 그룹1은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 포함하며 노드 A에서 실행 중입니다. 그룹2도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 포함하며 노드 B에서 실행 중입니다. 그룹2는 노드 A로 장애 조치(failover)됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스는 단일 인스턴스 서비스이므로 노드 A에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 다른 인스턴스를 시작하려고 하면 오류가 발생합니다. 노드 A로 장애 조치(failover)를 시도하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 실패 여부는 그룹 2의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스 구성에 따라 달라집니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 리소스 그룹의 다른 서비스에 영향을 주도록 구성되어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 실패로 인해 장애 조치(failover)를 시도하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스도 실패하게 됩니다. 서비스가 리소스 그룹 내의 다른 서비스에 영향을 주지 않도록 구성된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스는 노드 A로 장애 조치(failover)할 수 있습니다. 그룹2의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스가 리소스 그룹의 다른 서비스에 영향을 주지 않도록 구성되지 않았다면 장애 조치(failover) 중인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스의 실패로 인해 장애 조치(failover) 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스까지 실패할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 클러스터에서 Integration Services 서비스를 구성하는 단계별 지침은 [Integration Services 서비스를 클러스터 리소스로 구성](../configure-the-integration-services-service-as-a-cluster-resource.md)을 참조하세요.  
  
  
