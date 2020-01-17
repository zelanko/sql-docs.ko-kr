---
title: soft-NUMA(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68232821ac186aa63d113319373b8326dae987a4
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165183"
---
# <a name="soft-numa-sql-server"></a>soft-NUMA(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

최신 프로세서에는 소켓당 여러 코어가 있습니다. 일반적으로 각 소켓은 단일 NUMA 노드로 표시됩니다. SQL Server 데이터베이스 엔진은 여러 내부 구조를 분할하며 NUMA 노드에 따라 서비스 스레드를 분할합니다.  소켓당 10개 이상의 코어를 포함하고 있는 프로세서의 경우 소프트웨어 NUMA를 사용하여 하드웨어 NUMA 노드를 분할하면 일반적으로 확장성 및 성능이 향상됩니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 soft-NUMA(소프트웨어 기반 NUMA) 이전에는 레지스트리를 편집하여 노드 구성 선호도 마스크를 추가해야 했으며 인스턴스가 아닌 호스트 수준에서 구성했습니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 및 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스가 시작될 때 데이터베이스 인스턴스 수준에서 soft-NUMA가 자동으로 구성됩니다.  
  
> [!NOTE]  
> Hot Add 프로세서는 soft-NUMA에서 지원되지 않습니다.  
  
## <a name="automatic-soft-numa"></a>자동 soft-NUMA  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 시작 시 NUMA 노드 또는 소켓당 8개 초과의 실제 코어를 감지할 때마다 soft-NUMA 노드가 기본적으로 자동 생성됩니다. 하이퍼 스레드 프로세서 코어는 노드에서 실제 코어 수를 계산할 때 구별되지 않습니다.  실제 코어 수가 소켓당 8개를 초과하여 감지된 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 코어 8개를 포함하는 이상적인 soft-NUMA 노드를 만들지만 노드당 논리 코어가 5개 또는 최대 9개까지 감소하거나 증가할 수 있습니다. 하드웨어 노드의 크기는 CPU 선호도 마스크에 의해 제한될 수 있습니다. NUMA 노드 수는 지원되는 최대 NUMA 노드 수를 초과할 수 없습니다.  
  
`SET SOFTNUMA` 인수가 포함된 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 문을 사용하여 soft-NUMA를 비활성화하거나 다시 활성화할 수 있습니다. 이 설정의 값을 변경하려면 데이터베이스 엔진의 다시 시작을 적용해야 합니다.  
  
아래 그림은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 각 노드 또는 소켓당 8개를 초과하는 실제 코어를 가진 하드웨어 NUMA 노드를 검색할 때 SQL Server 오류 로그에서 볼 수 있는 soft-NUMA에 관한 정보를 보여줍니다.  


```
2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.     
2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.     
2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.     
2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.   
```   

> [!NOTE]
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2부터 추적 플래그 8079를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 자동 소프트 NUMA를 사용하도록 허용합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 이 동작은 엔진에서 제어되며, 8079 추적 플래그는 아무 효과가 없습니다. 자세한 내용은 [DBCC TRACEON - 추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.

## <a name="manual-soft-numa"></a>수동 Soft-NUMA  
soft-NUMA를 사용하도록 수동으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 구성하려면 자동 soft_NUMA를 비활성화하고 레지스트리를 편집하여 노드 구성 선호도 마스크를 추가합니다. 이 방법을 사용할 때 soft-NUMA 마스크는 이진, DWORD(16진수 또는 십진수) 또는 QWORD(16진수 또는 십진수) 레지스트리 항목으로 정의할 수 있습니다. 첫 번째 32개를 초과하는 CPU를 구성하려면 QWORD 또는 BINARY 레지스트리 값을 사용합니다(QWORD 값은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전에 사용할 수 없음). 레지스트리를 수정한 후 soft-NUMA 구성이 적용되려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작해야 합니다.  
  
> [!TIP]
> CPU 번호는 0부터 시작합니다.  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
하드웨어 NUMA가 없는 8개의 CPU를 포함한 컴퓨터 예제를 가정합니다. 3개의 소프트 NUMA 노드가 구성되어 있습니다.   
[!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 A는 CPU를 0부터 3까지 사용하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 두 번째 인스턴스가 설치되고 CPU 4에서 7까지 사용하도록 구성되었습니다. 이 예는 시각적으로 다음과 같이 나타낼 수 있습니다.  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 이제 I/O가 많은 인스턴스 A에는 I/O 스레드 두 개와 지연 기록기 스레드 하나가 있습니다. 프로세서를 많이 사용하는 작업을 수행하는 인스턴스 B에는 I/O 스레드와 지연 기록기 스레드가 각각 하나뿐입니다. 두 인스턴스에 서로 다른 양의 메모리를 할당할 수 있지만 하드웨어 NUMA와 달리 두 인스턴스는 모두 동일한 운영 체제 메모리 블록에서 메모리를 받으며 메모리에서 프로세서로의 선호도가 없습니다.  
  
 지연 기록기 스레드는 물리적 NUMA 메모리 노드의 SQLOS 보기와 연결되어 있습니다. 따라서, 물리적 NUMA 노드 수로 표시되는 하드웨어는 생성되는 지연 기록기 스레드의 수와 같습니다. 자세한 내용은 [작동 방법: 소프트 NUMA, I/O 완료 스레드, 지연 기록기 노동자와 메모리 노드](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)를 참조하세요.  
  
> [!NOTE]
> **Soft-NUMA** 레지스트리 키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 업그레이드할 때 복사되지 않습니다.  
  
### <a name="set-the-cpu-affinity-mask"></a>CPU 선호도 마스크 설정  
 인스턴스 A에서 CPU 선호도 마스크를 설정하는 다음 문을 실행하여 CPU 0, 1, 2, 3을 사용하도록 구성합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
인스턴스 B에서 CPU 선호도 마스크를 설정하는 다음 문을 실행하여 CPU 4, 5, 6, 7을 사용하도록 구성합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>CPU에 소프트 NUMA 노드 매핑  
 레지스트리 편집기 프로그램(regedit.exe)에서 다음 레지스트리 키를 추가하여 soft-NUMA 노드 0을 CPU 0과 1에, soft-NUMA 노드 1을 CPU 2와 3에, soft-NUMA 노드 2를 CPU 4, 5, 6, 7에 각각 매핑합니다.  
  
> [!TIP]
> CPU 60 - 63을 지정하려면 QWORD 값 F000000000000000 또는 BINARY 값 1111000000000000000000000000000000000000000000000000000000000000을 사용합니다.  
  
 다음 예제에서는 DL580 G9 서버가 있고 4개의 소켓에서 소켓당 18개의 코어가 있으며 각 소켓은 자체 K 그룹에 있다고 가정합니다. 만들 수 있는 soft-NUMA 구성은 노드당 6개의 코어, 그룹당 3개의 노드, 4개의 그룹과 같습니다.  
  
|K 그룹이 여러 개인 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 서버의 예|Type|값 이름|값 데이터|  
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
 다음 DMV를 사용하여 soft-NUMA의 현재 상태 및 구성을 볼 수 있습니다.  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md): SOFTNUMA에 대한 현재 값(0 또는 1)을 표시합니다.  
  
-   [sys.dm_os_sys_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md): *softnuma_configuration* 및 *softnuma_configuration_desc* 열은 현재 구성 값을 표시합니다.  
  
> [!NOTE]
> [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 자동 soft-NUMA에 대한 실행 값을 볼 수 있지만 **sp_configure**를 사용하여 해당 값을 변경할 수는 없습니다. `SET SOFTNUMA` 인수가 포함된 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) 문을 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[NUMA 노드에 TCP IP 포트 매핑&#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)    
[선호도 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)    
[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)     
[sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)   
  
