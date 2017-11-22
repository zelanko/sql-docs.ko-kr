---
title: soft-NUMA(SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
caps.latest.revision: "53"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: adde08cc4584568c42d896b70ffbcc49689d6416
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="soft-numa-sql-server"></a>soft-NUMA(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  최신 프로세서는 소켓당 여러 개에서 많은 코어를 가지고 있습니다. 일반적으로 각 소켓은 단일 NUMA 노드로 표시됩니다. SQL Server 데이터베이스 엔진은 여러 내부 구조를 분할하며 NUMA 노드에 따라 서비스 스레드를 분할합니다.  소켓당 10개 이상의 코어를 포함하고 있는 프로세서의 경우 소프트웨어 NUMA를 사용하여 하드웨어 NUMA 노드를 분할하면 일반적으로 확장성 및 성능이 향상됩니다. SQL Server 2014 SP2 soft-NUMA(소프트웨어 기반 NUMA) 이전에는 레지스트리를 편집하여 노드 구성 선호도 마스크를 추가해야 했으며 인스턴스가 아닌 컴퓨터별로 구성했습니다.  SQL Server 2014 SP2 및 SQL Server 2016에서는 SQL Server 서비스가 시작될 때 데이터베이스 인스턴스 수준에서 soft-NUMA가 자동으로 구성됩니다.  
  
> [!NOTE]  
>  Hot Add 프로세서는 soft-NUMA에서 지원되지 않습니다.  
  
## <a name="automatic-soft-numa"></a>자동 soft-NUMA  
 SQL Server 2016에서는 데이터베이스 엔진 서버가 시작 시 NUMA 노드 또는 소켓당 8개보다 많은 실제 코어를 검색할 때마다 soft-NUMA 노드가 기본적으로 자동 생성됩니다. 하이퍼 스레드 프로세서 코어는 노드에서 실제 코어 수를 계산할 때 구별되지 않습니다.  실제 코어 수가 소켓당 8개보다 많이 검색된 경우 데이터베이스 엔진 서비스는 코어 8개를 포함하는 것이 최적인 soft-NUMA 노드를 만들지만 노드당 논리 코어가 5개 또는 최대 9개까지 감소할 수 있습니다. 하드웨어 노드의 크기는 CPU 선호도 마스크에 의해 제한될 수 있습니다. 참조 항목   
            [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) NUMA 노드 수는 지원되는 최대 NUMA 노드 수를 초과할 수 없습니다.  
  
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 문을 SET SOFTNUMA 인수와 함께 사용하여 soft-NUMA를 비활성화하거나 다시 활성화할 수 있습니다. 이 설정의 값을 변경하려면 데이터베이스 엔진의 다시 시작을 적용해야 합니다.  
  
 아래 그림은 SQL Server가 각 노드 또는 소켓에서 8개보다 많은 실제 코어를 가진 하드웨어 NUMA 노드를 검색할 때 SQL Server 오류 로그에서 볼 수 있는 soft-NUMA에 관한 정보를 보여 줍니다.  


``2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.``  
  **``2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.``**  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``

  
## <a name="manual-soft-numa"></a>수동 Soft-NUMA  
 자동 soft_NUMA를 비활성화하고 레지스트리를 편집하여 노드 구성 선호도 마스크를 추가함으로써 soft-NUMA를 사용하도록 수동으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 구성합니다. 이 방법을 사용할 때 soft-NUMA 마스크는 이진, DWORD(16진수 또는 십진수) 또는 QWORD(16진수 또는 십진수) 레지스트리 항목으로 정의할 수 있습니다. 첫 32개 CPU 이상을 구성하려면 QWORD 또는 BINARY 레지스트리 값을 사용합니다. QWORD 값은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서만 사용할 수 있습니다. 레지스트리를 수정한 후 soft-NUMA 구성이 적용되려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작해야 합니다.  
  
> [!TIP]
> CPU 번호는 0부터 시작합니다.  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 다음 예를 살펴 보십시오. 8개의 CPU가 있고 하드웨어 NUMA가 없는 컴퓨터가 있습니다. 3개의 소프트 NUMA 노드가 구성되어 있습니다.   
            [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 A는 CPU를 0부터 3까지 사용하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 두 번째 인스턴스가 설치되고 CPU 4에서 7까지 사용하도록 구성되었습니다. 이 예는 시각적으로 다음과 같이 나타낼 수 있습니다.  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 이제 I/O가 많은 인스턴스 A에는 I/O 스레드와 지연 기록기 스레드가 각각 한 개씩 있는 반면, 프로세서를 많이 사용하는 작업을 수행하는 인스턴스 B에는 I/O 스레드와 지연 기록기 스레드가 각각 하나뿐입니다. 두 인스턴스에 서로 다른 양의 메모리를 할당할 수 있지만 하드웨어 NUMA와 달리 두 인스턴스는 모두 동일한 운영 체제 메모리 블록에서 메모리를 받으며 메모리에서 프로세서로의 선호도가 없습니다.  
  
 지연 기록기 스레드는 물리적 NUMA 메모리 노드의 SQL OS 보기와 연결되어 있습니다. 따라서, 물리적 NUMA 노드로 표시되는 하드웨어는 생성되는 지연 기록기 스레드의 수와 같습니다. 자세한 내용은 다음을 참조하세요.   
            [작동 방식: soft-NUMA, I/O 완료 스레드, 지연 기록기 작업자 및 메모리 노드](http://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)  
  
> [!NOTE]
> **Soft-NUMA** 레지스트리 키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 업그레이드할 때 복사되지 않습니다.  
  
### <a name="set-the-cpu-affinity-mask"></a>CPU 선호도 마스크 설정  
 인스턴스 A에서 CPU 선호도 마스크를 설정하는 다음 문을 실행하여 CPU 0, 1, 2, 3을 사용하도록 구성합니다.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
 인스턴스 B에서 CPU 선호도 마스크를 설정하는 다음 문을 실행하여 CPU 4, 5, 6, 7을 사용하도록 구성합니다.  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>CPU에 소프트 NUMA 노드 매핑  
 레지스트리 편집기 프로그램(regedit.exe)에서 다음 레지스트리 키를 추가하여 소프트 NUMA 노드 0을 CPU 0과 1에, 소프트 NUMA 노드 1을 CPU 2와 3에, 소프트 NUMA 노드 2를 CPU 4, 5, 6, 7에 각각 매핑합니다.  
  
> [!TIP]
> CPU 60 - 63을 지정하려면 QWORD 값 F000000000000000 또는 BINARY 값 1111000000000000000000000000000000000000000000000000000000000000을 사용합니다.  
  
 다음 예제에서는 DL580 G9 서버가 있고 4개의 소켓에서 소켓당 18개의 코어가 있으며 각 소켓은 자체 K 그룹에 있다고 가정합니다. 만들 수 있는 소프트 NUMA 구성은 다음과 유사할 것입니다. (노드당 6개의 코어, 그룹당 3개의 노드, 4개의 그룹).  
  
|K 그룹이 여러 개인 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 서버의 예|유형|값 이름|값 데이터|  
|-----------------------------------------------------------------------------------------------------------------|----------|----------------|----------------|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|그룹|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|그룹|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|그룹|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|그룹|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|그룹|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|그룹|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|그룹|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|그룹|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|그룹|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|그룹|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|그룹|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|그룹|3|  
  
## <a name="metadata"></a>메타데이터  
 다음 DMV를 사용하여 soft_NUMA의 현재 상태 및 구성을 볼 수 있습니다.  
  
-   [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md): SOFTNUMA에 대한 현재 값(0 또는 1)을 표시합니다.  
  
-   [sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md): 각 NUMA 노드에 대한 node_state_desc 열은 soft-NUMA에 의해 노드가 생성되는지 여부를 보여 줍니다.  
  
-   [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md): Softnuma 및 softnuma_desc 열은 구성 값을 표시합니다.  
  
> [!NOTE]
> [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 자동 soft-NUMA에 대한 실행 값을 볼 수 있지만 **sp_configure**를 사용하여 해당 값을 변경할 수는 없습니다. [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 문과 함께 SET SOFTNUMA 인수를 사용해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [NUMA 노드에 TCP IP 포트 매핑&#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [선호도 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  

