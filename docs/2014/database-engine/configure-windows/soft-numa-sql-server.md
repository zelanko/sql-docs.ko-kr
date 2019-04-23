---
title: SOFT-NUMA (SQL Server)를 사용 하도록 SQL Server 구성 | Microsoft Docs
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
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953829"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>소프트 NUMA를 사용하도록 SQL Server 구성(SQL Server)
최신 프로세서는 소켓당 여러 개에서 많은 코어를 가지고 있습니다. 일반적으로 각 소켓은 단일 NUMA 노드로 표시됩니다. SQL Server 데이터베이스 엔진은 여러 내부 구조를 분할하며 NUMA 노드에 따라 서비스 스레드를 분할합니다. NUMA (SOFT-NUMA) 일반적으로 하드웨어 NUMA 노드 분할에 소프트웨어를 사용 하 여 소켓 당 10 개 이상의 코어를 포함 하는 프로세서를 사용 하 여 확장성 및 성능 증가 합니다.   

> [!NOTE]
> Hot Add 프로세서는 soft-NUMA에서 지원되지 않습니다.
  
## <a name="automatic-soft-numa"></a>자동 soft-NUMA
부터 SQL Server 2014 서비스 팩 2를 사용 하 여 데이터베이스 엔진 서버가 시작 시 실제 프로세서 8 개 이상의 감지할 때마다 SOFT-NUMA 노드가 자동으로 만들어집니다 추적 플래그 8079 시작 매개 변수로 사용 하는 경우. 실제 프로세서 수를 계산할 때 하이퍼 스레드 프로세서 코어에 대 한 처리 하지 않은 합니다. 검색 된 실제 프로세서 수가 소켓 당 8 개 이상의 경우 데이터베이스 엔진 서비스 이상적 코어 8 개를 포함 하지만 노드당 논리 프로세서 5 개 또는 최대 9 개까지 감소할 수 있습니다 소프트 NUMA 노드가 만들어집니다. 하드웨어 노드의 크기는 CPU 선호도 마스크에 의해 제한될 수 있습니다. NUMA 노드 수는 지원되는 최대 NUMA 노드 수를 초과할 수 없습니다.

추적 플래그 없이 소프트 NUMA는 기본적으로 비활성화 됩니다. 소프트 NUMA를 설정할 수 있습니다. 추적 플래그 8079를 사용 합니다. 이 설정의 값을 변경하려면 데이터베이스 엔진의 다시 시작을 적용해야 합니다.

아래 그림에는 유형의 SQL Server 논리 프로세서 8 개 초과 가진 하드웨어 NUMA 노드를 검색 및 추적 플래그 8079를 설정 하는 경우 SQL Server 오류 로그에서 볼 수 있는 SOFT-NUMA에 관한 정보를 보여 줍니다.

![Soft-NUMA](./media/soft-numa-sql-server/soft-numa.PNG)

> [!NOTE]
> 이 동작은 엔진 및 추적 플래그 8079 통해 제어 되며 SQL Server 2016을 사용 하 여 시작 하는 것은 효과가 없습니다.

## <a name="manual-soft-numa"></a>수동 Soft-NUMA
  
구성 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소프트 NUMA를 수동으로 사용 하려면 노드 구성 선호도 마스크를 추가 하려면 레지스트리를 편집 해야 합니다. 소프트 NUMA 마스크는 이진, DWORD(16진수 또는 십진수) 또는 QWORD(16진수 또는 십진수) 레지스트리 항목으로 정의할 수 있습니다. 첫 32개 CPU 이상을 구성하려면 QWORD 또는 BINARY 레지스트리 값을 사용합니다. QWORD 값은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서만 사용할 수 있습니다. 다시 시작 해야 합니다 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 소프트 NUMA를 구성 합니다.  
  
> [!TIP]  
>  CPU 번호는 0부터 시작합니다.  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 다음 예를 살펴 보십시오. 8개의 CPU가 있고 하드웨어 NUMA가 없는 컴퓨터가 있습니다. 3개의 소프트 NUMA 노드가 구성되어 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 A는 CPU를 0부터 3까지 사용하도록 구성됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 두 번째 인스턴스가 설치되고 CPU 4에서 7까지 사용하도록 구성되었습니다. 이 예는 시각적으로 다음과 같이 나타낼 수 있습니다.  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 이제 I/O가 많은 인스턴스 A에는 I/O 스레드와 지연 기록기 스레드가 각각 한 개씩 있는 반면, 프로세서를 많이 사용하는 작업을 수행하는 인스턴스 B에는 I/O 스레드와 지연 기록기 스레드가 각각 하나뿐입니다. 두 인스턴스에 서로 다른 양의 메모리를 할당할 수 있지만 하드웨어 NUMA와 달리 두 인스턴스는 모두 동일한 운영 체제 메모리 블록에서 메모리를 받으며 메모리에서 프로세서로의 선호도가 없습니다.  
  
 지연 기록기 스레드는 물리적 NUMA 메모리 노드의 SQL OS 보기와 연결되어 있습니다. 따라서, 물리적 NUMA 노드로 표시되는 하드웨어는 생성되는 지연 기록기 스레드의 수와 같습니다. 자세한 내용은 [작동 방법: 소프트 NUMA, I/O 완료 스레드, 지연 기록기 작업자 및 메모리 노드](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)합니다.  
  
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
  
    |K 그룹이 여러 개인 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 서버의 예|형식|값 이름|값 데이터|  
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
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|형식|값 이름|값 데이터|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|그룹|0|  
  
    > [!TIP]  
    >  CPU 60 - 63을 지정하려면 QWORD 값 F000000000000000 또는 BINARY 값 1111000000000000000000000000000000000000000000000000000000000000을 사용합니다.  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|형식|값 이름|값 데이터|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|그룹|0|  
  
    |SQL Server 2008 R2|형식|값 이름|값 데이터|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|그룹|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|그룹|0|  
  
    |SQL Server 2008|형식|값 이름|값 데이터|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|형식|값 이름|값 데이터|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>관련 항목  
 [NUMA 노드에 TCP IP 포트 매핑&#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [선호도 마스크 서버 구성 옵션](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
