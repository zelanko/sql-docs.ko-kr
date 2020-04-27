---
title: 소프트 NUMA (SQL Server)를 사용 하도록 SQL Server 구성 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6ad0e30c0db83daf7e0cae4f7353d1f0a96a96d9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62809043"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>소프트 NUMA를 사용하도록 SQL Server 구성(SQL Server)
최신 프로세서는 소켓당 여러 개에서 많은 코어를 가지고 있습니다. 일반적으로 각 소켓은 단일 NUMA 노드로 표시됩니다. SQL Server 데이터베이스 엔진은 여러 내부 구조를 분할하며 NUMA 노드에 따라 서비스 스레드를 분할합니다. 소켓 당 10 개 이상의 코어가 포함 된 프로세서의 경우 소프트웨어 NUMA (소프트 NUMA)를 사용 하 여 하드웨어 NUMA 노드를 분할 하면 일반적으로 확장성 및 성능이 향상 됩니다.   

> [!NOTE]
> Hot Add 프로세서는 soft-NUMA에서 지원되지 않습니다.
  
## <a name="automatic-soft-numa"></a>자동 soft-NUMA
SQL Server 2014 서비스 팩 2부터 시작 시 데이터베이스 엔진 서버가 8 개 이상의 실제 프로세서를 검색할 때마다 추적 플래그 8079이 시작 매개 변수로 설정 되 면 소프트 NUMA 노드가 자동으로 만들어집니다. 하이퍼 스레드 프로세서 코어는 실제 프로세서 수를 계산 하는 경우에는 고려 되지 않습니다. 검색 된 실제 프로세서 수가 소켓 당 8 개를 초과 하는 경우에는 데이터베이스 엔진 서비스에서 8 개 코어를 포함 하는 소프트 NUMA 노드를 만들지만 노드당 5 개 또는 최대 9 개의 논리적 프로세서로 이동할 수 있습니다. 하드웨어 노드의 크기는 CPU 선호도 마스크에 의해 제한될 수 있습니다. NUMA 노드 수는 지원되는 최대 NUMA 노드 수를 초과할 수 없습니다.

추적 플래그 없이 소프트 NUMA는 기본적으로 사용 되지 않습니다. 추적 플래그 8079을 사용 하 여 소프트 NUMA를 사용 하도록 설정할 수 있습니다. 이 설정의 값을 변경하려면 데이터베이스 엔진의 다시 시작을 적용해야 합니다.

아래 그림에서는 8 개 이상의 논리적 프로세서를 사용 하 여 하드웨어 NUMA 노드를 검색 하 고 8079 추적 플래그을 사용 하는 경우 SQL Server 오류 SQL Server 로그에 표시 되는 소프트 NUMA 관련 정보 유형을 보여 줍니다.

![Soft-NUMA](./media/soft-numa-sql-server/soft-numa.PNG)

> [!NOTE]
> SQL Server 2016부터이 동작은 엔진에서 제어 되며 추적 플래그 8079는 영향을 주지 않습니다.

## <a name="manual-soft-numa"></a>수동 Soft-NUMA
  
소프트 NUMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 수동으로 사용 하도록를 구성 하려면 레지스트리를 편집 하 여 노드 구성 선호도 마스크를 추가 해야 합니다. 소프트 NUMA 마스크는 이진, DWORD(16진수 또는 십진수) 또는 QWORD(16진수 또는 십진수) 레지스트리 항목으로 정의할 수 있습니다. 첫 32개 CPU 이상을 구성하려면 QWORD 또는 BINARY 레지스트리 값을 사용합니다. (이 (가) 이전에는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]qword(64 값을 사용할 수 없습니다.) 소프트 NUMA를 구성 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 하려면를 다시 시작 해야 합니다.  
  
> [!TIP]  
>  CPU 번호는 0부터 시작합니다.  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 아래 예제를 고려해 보세요. 8개의 CPU가 있고 하드웨어 NUMA가 없는 컴퓨터가 있습니다. 3개의 소프트 NUMA 노드가 구성되어 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 A는 CPU를 0부터 3까지 사용하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 두 번째 인스턴스가 설치되고 CPU 4에서 7까지 사용하도록 구성되었습니다. 이 예는 시각적으로 다음과 같이 나타낼 수 있습니다.  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 이제 I/O가 많은 인스턴스 A에는 I/O 스레드와 지연 기록기 스레드가 각각 한 개씩 있는 반면, 프로세서를 많이 사용하는 작업을 수행하는 인스턴스 B에는 I/O 스레드와 지연 기록기 스레드가 각각 하나뿐입니다. 두 인스턴스에 서로 다른 양의 메모리를 할당할 수 있지만 하드웨어 NUMA와 달리 두 인스턴스는 모두 동일한 운영 체제 메모리 블록에서 메모리를 받으며 메모리에서 프로세서로의 선호도가 없습니다.  
  
 지연 기록기 스레드는 물리적 NUMA 메모리 노드의 SQL OS 보기와 연결되어 있습니다. 따라서, 물리적 NUMA 노드로 표시되는 하드웨어는 생성되는 지연 기록기 스레드의 수와 같습니다. 자세한 내용은 [작동 방식: 소프트 NUMA, I/O 완료 스레드, 지연 기록기 작업자 및 메모리 노드](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)를 참조하세요.  
  
> [!NOTE]  
>  **Soft-NUMA** 레지스트리 키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 업그레이드할 때 복사되지 않습니다.  
  
### <a name="set-the-cpu-affinity-mask"></a>CPU 선호도 마스크 설정  
  
1.  인스턴스 A에서 CPU 선호도 마스크를 설정하는 다음 문을 실행하여 CPU 0, 1, 2, 3을 사용하도록 구성합니다.  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  인스턴스 B에서 CPU 선호도 마스크를 설정하는 다음 문을 실행하여 CPU 4, 5, 6, 7을 사용하도록 구성합니다.  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>CPU에 소프트 NUMA 노드 매핑  
  
-   레지스트리 편집기 프로그램(regedit.exe)에서 다음 레지스트리 키를 추가하여 소프트 NUMA 노드 0을 CPU 0과 1에, 소프트 NUMA 노드 1을 CPU 2와 3에, 소프트 NUMA 노드 2를 CPU 4, 5, 6, 7에 각각 매핑합니다.  
  
     다음 예제에서는 DL580 G9 서버가 있고 4개의 소켓에서 소켓당 18개의 코어가 있으며 각 소켓은 자체 K 그룹에 있다고 가정합니다. 만들 수 있는 소프트 NUMA 구성은 다음과 유사할 것입니다. (노드당 6개의 코어, 그룹당 3개의 노드, 4개의 그룹).  
  
    |K 그룹이 여러 개인 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 서버의 예|유형|값 이름|값 데이터|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|그룹|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|그룹|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|그룹|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|그룹|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|그룹|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|그룹|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|그룹|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|그룹|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|그룹|3|  
  
     추가 예:  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|유형|값 이름|값 데이터|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|그룹|0|  
  
    > [!TIP]  
    >  CPU 60 - 63을 지정하려면 QWORD 값 F000000000000000 또는 BINARY 값 1111000000000000000000000000000000000000000000000000000000000000을 사용합니다.  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|유형|값 이름|값 데이터|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|그룹|0|  
  
    |SQL Server 2008 R2|유형|값 이름|값 데이터|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|그룹|0|  
  
    |SQL Server 2008|유형|값 이름|값 데이터|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|유형|값 이름|값 데이터|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server&#41;&#40;NUMA 노드에 TCP IP 포트 매핑](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [affinity mask 서버 구성 옵션](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
