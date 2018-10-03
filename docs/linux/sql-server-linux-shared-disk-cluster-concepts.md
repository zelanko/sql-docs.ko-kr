---
title: Linux의 SQL Server 장애 조치 클러스터 인스턴스 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 14d54a9e004364db783a4462d9e941f0e513a292
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659811"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Linux의 SQL Server 장애 조치 클러스터 인스턴스

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux의 SQL Server 장애 조치 클러스터 인스턴스 (FCI)와 관련 된 개념을 설명 합니다. 

Linux에서 SQL Server FCI를 만들려면 참조 [Linux에서 SQL Server FCI 구성](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>클러스터링 계층

* RHEL에서 클러스터링 계층 Red Hat Enterprise Linux (RHEL) 기반 [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)합니다. 

    > [!NOTE] 
    > Red Hat HA 추가 기능 및 설명서에 대 한 액세스는 구독이 필요 합니다. 

* SLES, 클러스터링 계층을 기반으로 하며 SUSE Linux Enterprise [높은 가용성 확장 (HAE)](https://www.suse.com/products/highavailability)합니다.

    클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대 한 자세한 내용은 참조 하세요. [SUSE Linux Enterprise 높은 가용성 확장 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)합니다.

RHEL HA 추가 기능 및 SUSE HAE에서 빌드된 [Pacemaker](http://clusterlabs.org/)합니다.

다음 다이어그램에서 알 수 있듯이, 저장소는 두 서버에 표시 됩니다. -Corosync 및 Pacemaker-클러스터링 구성 요소 통신 및 리소스 관리를 조정합니다. 저장소 리소스 및 SQL Server에 활성 연결이 서버 중 하나입니다. Pacemaker 오류를 발견 하면 클러스터링 구성 요소 관리 리소스를 다른 노드로 이동 합니다.  

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 이 시점에서 Linux의 Pacemaker 사용 하 여 SQL Server의 통합은 Windows에 WSFC를 사용 하 여으로 결합 없습니다. 내의 SQL에는 클러스터의 현재 상태에 대해 모든 오케스트레이션 외부에서 이며 서비스는 독립 실행형 인스턴스로 Pacemaker에 의해 제어 됩니다. 또한 가상 네트워크 이름은 WSFC 관련, Pacemaker에 동일한 동등한 옵션이 없습니다. 것으로 예상 되는 @@servername 및 sys.servers 클러스터 dmv sys.dm_os_cluster_nodes 및 sys.dm_os_cluster_properties를 레코드가 하는 동안 노드 이름을 반환할 합니다. 문자열 서버 이름으로 가리키는 연결 문자열을 사용 하 고 IP를 사용 하지를 선택한 서버 이름 (다음 섹션에서 설명)으로 가상 IP 리소스를 만드는 데 IP을 해당 DNS 서버에 등록 해야 합니다.

## <a name="number-of-instances-and-nodes"></a>인스턴스 수 및 노드

Linux의 SQL Server를 사용 하 여 한 가지 주요 차이점은 있을 수 있습니다만 Linux 서버당 하나의 SQL Server 설치 해당 설치 것을 인스턴스라고를 부릅니다. 이 Windows Server 장애 조치 클러스터 (WSFC) 당 최대 25 개의 Fci를 지 원하는 Windows Server와 달리 Linux 기반 FCI만 되어 단일 인스턴스를 의미 합니다. 이 하나의 인스턴스는 또한 기본; Linux의 명명된 된 인스턴스에 대 한 개념이 없습니다 있습니다. 

Pacemaker 클러스터를 하나만 사용할 수 있습니다 최대 16 개의 노드로 Corosync 관련 된 경우 단일 FCI 최대 16 명의 서버에 걸쳐 있을 수 있도록 합니다. SQL Server의 Standard Edition을 사용 하 여 구현 하는 FCI는 Pacemaker 클러스터에 최대 16 개의 노드로 구성 된 경우에 최대 2 개의 클러스터 노드를 지원 합니다.

SQL Server FCI를 SQL Server 인스턴스는 하나의 노드 또는 다른 활성입니다.

## <a name="ip-address-and-name"></a>IP 주소 및 이름
Linux Pacemaker 클러스터에서 각 SQL Server FCI에는 자체 고유 IP 주소 및 이름이 필요합니다. FCI 구성에서 여러 서브넷에 걸쳐 있는 경우 하나의 IP 주소는 서브넷별로 해야 합니다. 응용 프로그램 및 최종 사용자에 게 않아도 Pacemaker 클러스터의 기본 서버는 알 수 있도록 FCI를 액세스 하는 고유한 이름 및 IP 주소 사용 됩니다.

DNS에서 FCI의 이름을 Pacemaker 클러스터에서 생성 되는 FCI 리소스의 이름과 동일 해야 합니다.
이름 및 IP 주소가 모두 DNS에 등록 되어야 합니다.

## <a name="shared-storage"></a>공유 저장소
Linux 또는 Windows Server에서 되었든 관계 없이 모든 Fci는 일종의 공유 저장소에 필요 합니다. 이 저장소는 FCI를 호스팅할 수 있는 수 있는 모든 서버에 표시 됩니다 있지만 단일 서버에서 언제 든 지 FCI에 대 한 저장소를 사용할 수 있습니다. Linux에서 공유 저장소에 사용 가능한 옵션은 같습니다.

- iSCSI
- 네트워크 파일 시스템 (NFS)
- 서버 메시지 블록 (SMB)에서 Windows Server는 약간 다른 옵션이 있습니다. 현재 지원 되지 않는 Linux 기반 Fci에 대 한 한 가지 옵션, TempDB는 SQL Server의 임시 작업 영역에 대 한 노드의 로컬 디스크를 사용 하려면 있다는 점입니다.

여러 위치에 걸쳐 있는 구성에서 하나의 데이터 센터에 저장 된 것와 동기화 해야 다른 합니다. 장애 조치 시 FCI를 온라인 상태로 수 및 저장소 동일 하도록 표시 됩니다. 이렇게 해야 일부 외부 메서드의 저장소 복제의 경우 기본 저장소 하드웨어 또는 소프트웨어를 기반으로 일부 유틸리티를 통해 위배 됩니다. 

>[!NOTE]
>SQL Server에 대 한 이러한 서버에 직접 제공 하는 디스크를 사용 하 여 Linux 기반 배포 EXT4 또는 XFS로 포맷 되어야 합니다. 다른 파일 시스템 현재 지원 되지 않습니다. 변경 내용을 여기에 반영 됩니다.

공유 저장소를 제공 하기 위한 프로세스는 다양 한 지원 되는 방법에 대 한 같습니다.

- 공유 저장소를 구성 합니다.
- FCI에 대 한 Pacemaker 클러스터의 노드로 사용할 서버에 폴더를 저장소 탑재
- 필요한 경우 공유 저장소에 SQL Server 시스템 데이터베이스 이동
- 공유 저장소에 연결 된 SQL Server는 각 서버에서 작동 하는 테스트

Linux의 SQL Server를 사용 하 여 한 가지 주요 차이점은는 기본 사용자 데이터 및 로그 파일 위치를 구성할 수도 있지만, 시스템 데이터베이스는 항상에 있어야 `/var/opt/mssql/data`합니다. Windows Server에서 TempDB를 비롯 한 시스템 데이터베이스를 이동할 수가 있습니다. 이 팩트 FCI에 대 한 공유 저장소로 재생 구성 됩니다.

비 시스템 데이터베이스에 대 한 기본 경로 사용 하 여 변경할 수 있습니다는 `mssql-conf` 유틸리티입니다. 기본값을 변경 하는 방법에 대 한 내용은 [기본 데이터 또는 로그 디렉터리 위치를 변경할](sql-server-linux-configure-mssql-conf.md#datadir)합니다. 저장할 수도 있습니다. SQL Server 데이터 및 트랜잭션 다른 위치에서 기본 위치입니다; 없는 경우에 적절 한 보안을가지고 있습니다. 위치를 명시 해야 합니다.

다음 항목을 Linux 기반 SQL Server FCI에 대 한 지원 되는 저장소 형식을 구성 하는 방법에 설명 합니다.

- [장애 조치 클러스터 인스턴스-iSCSI-Linux의 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [장애 조치 클러스터 인스턴스-NFS-Linux의 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [장애 조치 클러스터 인스턴스-SMB-Linux의 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-smb.md)
