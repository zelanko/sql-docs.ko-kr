---
title: SQL Server 에이전트를 사용하여 원격 서버의 패키지 부하 분산 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- load-balancing [Integration Services]
- parent packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7c1f4792d97ae82561f0d05fe9754daae0a2bf3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62890189"
---
# <a name="load-balancing-packages-on-remote-servers-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 원격 서버의 패키지 로드 균형 조정
  패키지를 여러 개 실행해야 하는 경우 사용 가능한 다른 서버를 사용하는 것이 편리합니다. 모든 패키지를 한 부모 패키지에서 관리하고 다른 서버를 사용하여 패키지를 실행하는 이 방법을 로드 균형 조정이라고 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 부하 분산은 패키지 소유자가 직접 설계해야 하며 서버에서 자동으로 수행되지 않습니다. 또한 원격 서버에서 실행되는 패키지는 다른 패키지의 개별 태스크가 아닌 전체 패키지여야 합니다.  
  
 로드 균형 조정은 다음 시나리오에서 유용합니다.  
  
-   패키지를 동시에 실행할 수 있습니다.  
  
-   패키지가 크고 순차적으로 실행할 경우 처리에 허용된 시간보다 오래 걸릴 수 있습니다.  
  
 관리자와 설계자가 처리에 추가 서버를 사용하는 것이 프로세스에 유리한지 여부를 결정할 수 있습니다.  
  
## <a name="illustration-of-load-balancing"></a>로드 균형 조정의 그림  
 다음 다이어그램에서는 서버의 부모 패키지를 보여 줍니다. 부모 패키지에는 여러 개의 SQL 작업 에이전트 실행 태스크가 들어 있습니다. 부모 패키지에 있는 각 태스크는 원격 서버의 SQL Server 에이전트를 호출합니다. 이러한 원격 서버에는 해당 서버의 패키지를 호출하는 단계가 포함된 SQL Server 에이전트 작업이 들어 있습니다.  
  
 ![SSIS 부하 분산 아키텍처 개요](../media/loadbalancingoverview.gif "SSIS 부하 분산 아키텍처 개요")  
  
 이 아키텍처에서 로드 균형을 조정하는 데 필요한 단계는 새로운 개념이 아닙니다. 대신 기존 개념 및 일반 SSIS 개체를 새로운 방식으로 사용하여 로드 균형을 조정합니다.  
  
## <a name="execution-of-packages-on-a-remote-instance-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 원격 인스턴스에서 패키지 실행  
 원격 패키지 실행을 위한 기본 아키텍처에서 중앙 패키지는 다른 원격 패키지를 제어하는 SQL Server의 인스턴스에 있습니다. 다이어그램은 이 중앙 패키지, 즉 SSIS 부모를 보여 줍니다. 이 부모 패키지가 있는 인스턴스는 자식 패키지를 실행하는 SQL Server 에이전트 작업의 실행을 제어합니다. 자식 패키지는 원격 서버에서 SQL Server 에이전트가 제어하는 고정 일정에 따라 실행되지 않습니다. 대신 자식 패키지는 부모 패키지가 호출하면 SQL Server 에이전트에 의해 시작되고 SQL Server 에이전트가 있는 SQL Server 인스턴스와 같은 인스턴스에서 실행됩니다.  
  
 SQL Server 에이전트를 사용하여 원격 패키지를 실행하려면 부모 및 자식 패키지를 구성하고 자식 패키지를 제어하는 SQL Server 에이전트 작업을 설정해야 합니다. 다음 섹션에서는 원격 서버에서 실행되는 패키지를 만들고, 구성하고, 실행하고, 유지 관리하는 방법을 설명합니다. 이 프로세스에는 여러 단계가 있습니다.  
  
-   원격 서버에서 자식 패키지 만들기 및 설치  
  
-   패키지를 실행할 원격 인스턴스에 SQL Server 에이전트 작업 만들기  
  
-   부모 패키지 만들기  
  
-   자식 패키지에 대한 로깅 시나리오 결정  
  
 다음 표에서는 전체 프로세스를 안내하는 항목에 대한 링크를 보여 줍니다.  
  
|항목|설명|  
|-----------|-----------------|  
|[자식 패키지 구현](../implementation-of-child-packages.md)|패키지를 설치하고 해당 패키지를 실행할 SQL Server 에이전트 작업을 만드는 방법을 설명합니다.|  
|[부모 패키지 구현](../implementation-of-the-parent-package.md)|여러 개의 SQL Server 에이전트 작업 실행 태스크가 포함된 부모 패키지를 만드는 방법을 설명합니다. 각 태스크는 자식 패키지 중 하나를 실행합니다.|  
|[원격 서버의 로드 균형 조정된 패키지 로깅](../logging-for-load-balanced-packages-on-remote-servers.md)|원격 패키지에 대한 로깅 시나리오를 설명합니다.|  
  
## <a name="related-tasks"></a>관련 작업  
 [SQL Server 에이전트를 사용하여 패키지 예약](../schedule-a-package-by-using-sql-server-agent.md)  
  
  
