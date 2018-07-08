---
title: affinity I/O mask 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 905421043a2d595d08bc1780213f91811f5c0960
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159044"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>선호도 입력-출력 마스크 서버 구성 옵션
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 및 Windows Server 2003에서는 멀티태스킹을 수행하기 위해 경우에 따라 여러 프로세서 사이에 프로세스 스레드를 이동하기도 합니다. 운영 체제 측면에서는 효율적이지만 각 프로세서 캐시에 데이터가 반복적으로 다시 로드되어 시스템 로드가 많은 경우 이로 인해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능이 저하될 수 있습니다. 프로세서를 특정 스레드에 할당하면 프로세서가 다시 로드되지 않으므로 이러한 조건에서도 성능을 향상시킬 수 있습니다. 스레드와 프로세서 간의 이러한 연결을 프로세서 선호도라고 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 두 가지 선호도 마스크 옵션인 **선호도 마스크** ( **CPU 선호도 마스크**라고도 함)와 **선호도 I/O 마스크**를 통해 프로세서 선호도를 지원합니다. **affinity mask** 옵션에 대한 자세한 내용은 [affinity mask 서버 구성 옵션](affinity-mask-server-configuration-option.md)을 참조하세요. 33-64개 프로세서가 있는 서버에 대한 CPU 및 I/O 선호도를 지원할 경우 [affinity64 mask 서버 구성 옵션](affinity64-mask-server-configuration-option.md) 및 [affinity64 Input-Output mask 서버 구성 옵션](affinity64-input-output-mask-server-configuration-option.md) 을 추가로 사용해야 합니다.  
  
> [!NOTE]  
>  33개에서 64개의 프로세서를 가지는 서버에 대한 선호도 지원은 64비트 운영 체제에서만 가능합니다.  
  
 **affinity I/O mask** 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O를 지정된 CPU 하위 집합에 바인딩합니다. 고성능 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP(온라인 트랜잭션 처리) 환경에서 이러한 확장을 통해 I/O를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스레드의 성능을 향상시킬 수 있습니다. 이 향상된 기능은 개별 디스크 또는 디스크 컨트롤러의 하드웨어 선호도를 지원하지 않습니다.  
  
 **affinity I/O mask** 의 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O 작업을 처리하는 데 적합한 다중 프로세서 컴퓨터의 CPU를 지정합니다. 마스크는 가장 오른쪽 비트가 최하위 CPU(0)를 지정하고 그 다음 왼쪽에 있는 비트가 두 번째 최하위 CPU(1)를 지정하는 방식으로 이어지는 비트맵입니다. 33개 이상의 프로세서를 구성하려면 **affinity I/O mask** 및 **affinity64 I/O mask**를 모두 설정합니다.  
  
 **affinity I/O mask** 의 값은 다음과 같습니다.  
  
-   1바이트 **affinity I/O mask** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 8개까지 허용됩니다.  
  
-   2바이트 **affinity I/O mask** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 16개까지 허용됩니다.  
  
-   3바이트 **affinity I/O mask** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 24개까지 허용됩니다.  
  
-   4바이트 **affinity I/O mask** 의 경우 하나의 다중 프로세서 컴퓨터에서 CPU가 32개까지 허용됩니다.  
  
-   33개 이상의 CPU를 처리하려면 처음 32개의 CPU에 대해 4바이트 **affinity I/O mask** 를 구성하고 나머지 CPU에 대해 최대 4바이트 **affinity64 I/O mask** 를 구성합니다.  
  
 affinity I/O 패턴의 1비트는 해당 CPU가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O 작업을 수행하는 데 적합함을 나타내고 0비트는 해당 CPU에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O 작업이 예약되지 않음을 나타냅니다. 모든 비트가 0으로 설정되어 있거나 **affinity I/O mask** 가 지정되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크 I/O는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스레드를 처리하는 데 적합한 모든 CPU에 대해 예약됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **affinity I/O mask** 옵션 설정은 특수 작업이므로 필요한 경우에만 사용해야 합니다. 대부분의 경우 Windows 2000 또는 Windows Server 2003 기본 선호도를 사용할 때 최상의 성능을 제공합니다.  
  
 **affinity I/O mask** 옵션을 지정할 때는 **affinity mask** 구성 옵션과 함께 사용해야 합니다. **affinity I/O mask** 스위치와 **affinity mask** 옵션에서 동일한 CPU를 사용하지 마세요. 각 CPU에 해당하는 비트는 다음 3가지 상태 중 하나여야 합니다.  
  
-   **affinity I/O mask** 옵션과 **affinity mask** 옵션이 모두 0  
  
-   **affinity I/O mask** 옵션이 1이고 **affinity mask** 옵션이 0  
  
-   **affinity I/O mask** 옵션이 0이고 **affinity mask** 옵션이 1  
  
 **affinity I/O mask** 옵션은 고급 옵션입니다. 사용 중인 경우는 `sp_configure` 시스템 저장 프로시저 설정을 변경 하려면, 변경할 수 있습니다 **affinity I/O mask** 경우에만 **고급 옵션 표시** 1로 설정 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 **affinity I/O mask** 옵션을 다시 구성하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야 합니다.  
  
> [!CAUTION]  
>  Windows 운영 체제에서 CPU 선호도를 구성하지 말고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 선호도 마스크를 구성하지 마십시오. 동일한 결과를 얻기 위해 이렇게 설정하는 경우도 있지만 구성이 일치하지 않는 경우 예상치 못한 결과가 나올 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 선호도는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 `sp_configure` 옵션을 사용하면 가장 잘 구성됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
