---
title: 장애 조치(failover) 클러스터 인스턴스 - SQL Server on Linux
description: Linux의 SQL Server 장애 조치(failover) 클러스터 인스턴스와 관련된 개념에는 클러스터링 레이어, 인스턴스 개수, IP 주소와 이름, 공유 스토리지 등이 있습니다.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1b2b852a1c1acecefa3b702bb140d9128d04a212
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784636"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>장애 조치(failover) 클러스터 인스턴스 - SQL Server on Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux의 SQL Server FCI(장애 조치(failover) 클러스터 인스턴스)에 관련된 개념을 설명합니다. 

Linux에서 SQL Server FCI를 만들려면 [Linux에서 SQL Server FCI 구성](sql-server-linux-shared-disk-cluster-configure.md)을 참조하세요.

## <a name="the-clustering-layer"></a>클러스터링 계층

* RHEL에서 클러스터링 계층은 RHEL(Red Hat Enterprise Linux) [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)을 기반으로 합니다. 

    > [!NOTE] 
    > Red Hat HA 추가 기능 및 설명서에 액세스하려면 구독이 필요합니다. 

* SLES에서 클러스터링 계층은 SUSE Linux Enterprise [HAE(High Availability Extension)](https://www.suse.com/products/highavailability)를 기반으로 합니다.

    클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대한 자세한 내용은 [SUSE Linux Enterprise High Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)를 참조하세요.

RHEL HA 추가 기능과 SUSE HAE는 모두 [Pacemaker](https://clusterlabs.org/)를 기반으로 빌드됩니다.

다음 다이어그램에 표시된 대로 스토리지는 두 개의 서버에 제공됩니다. 클러스터링 구성 요소인 Corosync와 Pacemaker는 통신 및 리소스 관리를 조정합니다. 서버 중 하나에는 스토리지 리소스 및 SQL Server에 대한 활성 연결이 있습니다. Pacemaker가 오류를 탐지하면 클러스터링 구성 요소는 리소스를 다른 노드로 이동하는 작업을 관리합니다.  

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 이때 Linux의 Pacemaker와 SQL Server의 통합은 Windows의 WSFC와 같이 결합되지 않습니다. SQL 내에 클러스터의 현재 상태 정보가 없으며, 모든 오케스트레이션이 외부에서 수행되고, 서비스는 Pacemaker에서 독립 실행형 인스턴스로 제어됩니다. 또한 가상 네트워크 이름은 WSFC에만 해당되며, Pacemaker에는 동일한 항목이 없습니다. @@servername 및 sys.servers가 노드 이름을 반환해야 하지만, cluster dmvs sys.dm_os_cluster_nodes 및 sys.dm_os_cluster_properties에 레코드가 없습니다. 문자열 서버 이름을 가리키는 연결 문자열을 사용하고 IP를 사용하지 않으려면 선택된 서버 이름을 사용하여 다음 섹션에 설명된 대로 가상 IP 리소스를 만드는 데 사용된 IP를 DNS 서버에 등록해야 합니다.

## <a name="number-of-instances-and-nodes"></a>인스턴스 및 노드 수

SQL Server on Linux의 한 가지 주요 차이는 Linux 서버당 SQL Server 설치가 하나만 있을 수 있다는 것입니다. 해당 설치를 인스턴스라고 합니다. 즉, WSFC(Windows Server 장애 조치(failover) 클러스터)당 최대 25개의 FCI를 지원하는 Windows Server와 달리 Linux 기반 FCIS에는 단일 인스턴스만 있습니다. 이 단일 인스턴스는 기본 인스턴스이기도 합니다. Linux에는 명명된 인스턴스의 개념이 없습니다. 

Corosync가 관련된 경우 Pacemaker 클러스터에는 최대 16개 노드만 포함될 수 있으므로 단일 FCI는 최대 16개 서버에 걸쳐 있을 수 있습니다. SQL Server Standard Edition으로 구현된 FCI는 Pacemaker 클러스터에 최대 16개 노드가 있는 경우에도 한 클러스터에서 최대 두 개의 노드를 지원합니다.

SQL Server FCI에서 SQL Server 인스턴스는 두 노드 중 하나에서 활성화됩니다.

## <a name="ip-address-and-name"></a>IP 주소 및 이름
Linux Pacemaker 클러스터에서 각 SQL Server FCI에는 고유한 IP 주소와 이름이 필요합니다. FCI 구성이 여러 서브넷에 걸쳐 있는 경우 서브넷당 하나의 IP 주소가 필요합니다. FCI에 액세스하는 데 고유 이름 및 IP 주소가 사용되므로 애플리케이션 및 최종 사용자는 Pacemaker 클러스터의 기본 서버를 알 필요가 없습니다.

DNS의 FCI 이름은 Pacemaker 클러스터에서 생성되는 FCI 리소스의 이름과 동일해야 합니다.
이름 및 IP 주소는 둘 다 DNS에 등록해야 합니다.

## <a name="shared-storage"></a>공유 스토리지
Linux 또는 Windows Server에 있는지 여부에 관계없이 모든 FCI에는 어떤 형태로든 공유 스토리지가 필요합니다. 이 스토리지는 FCI를 호스트할 수 있는 모든 서버에 제거되지만, 단일 서버에서만 특정 시점에 FCI에 스토리지를 사용할 수 있습니다. Linux에서 공유 스토리지에 사용할 수 있는 옵션은 다음과 같습니다.

- iSCSI
- NFS(네트워크 파일 시스템)
- SMB(서버 메시지 블록) Windows Server에서는 약간 다른 옵션을 사용할 수 있습니다. 현재 Linux 기반 FCI에 지원되지 않는 한 가지 옵션은 SQL Server 임시 작업 영역인 TempDB 노드에 로컬인 디스크를 사용하는 기능입니다.

여러 위치에 걸쳐 있는 구성에서는 하나의 데이터 센터에 저장된 항목이 다른 데이터 센터와 동기화되어야 합니다. 장애 조치(failover)를 수행할 때 FCI는 온라인 상태가 되고 스토리지는 동일하게 표시됩니다. 기본 스토리지 하드웨어 또는 일부 소프트웨어 기반 유틸리티를 통해 수행되는지 여부에 관계없이 이 작업을 수행하려면 스토리지 복제를 위한 외부 메서드가 필요합니다. 

>[!NOTE]
>SQL Server의 경우 서버에 직접 제공되는 디스크를 사용하는 Linux 기반 배포를 XFS 또는 EXT4로 포맷해야 합니다. 다른 파일 시스템은 현재 지원되지 않습니다. 여기에 변경 내용이 반영됩니다.

공유 스토리지를 제공하는 프로세스는 지원되는 다양한 메서드에 대해 동일합니다.

- 공유 스토리지 구성
- FCI에 대한 Pacemaker 클러스터의 노드로 사용할 서버에 스토리지를 폴더로 탑재합니다.
- 필요한 경우 SQL Server 시스템 데이터베이스를 공유 스토리지로 이동합니다.
- 공유 스토리지에 연결된 각 서버에서 SQL Server가 작동하는지 테스트합니다.

SQL Server on Linux의 한 가지 주요 차이는 기본 사용자 데이터와 로그 파일 위치는 구성 가능하지만 시스템 데이터베이스는 항상 `/var/opt/mssql/data`에 있어야 한다는 것입니다. Windows Server에는 TempDB를 포함하여 시스템 데이터베이스를 이동하는 기능이 있습니다. 이 사실은 FCI에 대해 공유 스토리지를 구성하는 방법의 영향을 받습니다.

비시스템 데이터베이스의 기본 경로는 `mssql-conf` 유틸리티를 사용하여 변경할 수 있습니다. 기본값을 변경하는 방법에 대한 자세한 내용은 [기본 데이터 또는 로그 디렉터리 위치 변경](sql-server-linux-configure-mssql-conf.md#datadir)을 참조하세요. 또한 기본 위치가 아니더라도 적절한 보안을 유지하는 경우 다른 위치에 SQL Server 데이터와 트랜잭션을 저장할 수 있으며, 위치를 명시해야 합니다.

다음 항목에서는 Linux 기반 SQL Server FCI에 대해 지원되는 스토리지 유형을 구성하는 방법을 설명합니다.

- [장애 조치(failover) 클러스터 인스턴스 구성 - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [장애 조치(failover) 클러스터 인스턴스 구성 - NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [장애 조치(failover) 클러스터 인스턴스 구성 - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
