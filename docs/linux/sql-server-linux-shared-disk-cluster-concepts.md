---
title: "장애 조치 클러스터 인스턴스-Linux에서 SQL Server | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 36c5b7ccd0cc8c3a56dca700469fb4fd05fa2871
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>장애 조치 클러스터 인스턴스-Linux에서 SQL Server

이 문서는 Linux에서 SQL Server 장애 조치 클러스터 인스턴스 (FCI)와 관련 된 개념을 설명 합니다. 

Linux에서 SQL Server FCI를 만들려면 [Linux에서 SQL Server FCI 구성](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>클러스터링 계층

* RHEL에서 클러스터링 레이어 Red Hat Enterprise Linux (RHEL) 기반 [HA 추가 기능](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)합니다. 

    > [!NOTE] 
    > Red Hat HA 추가 기능 및 문서에 대 한 액세스는 구독이 필요합니다. 

* SLES, 클러스터링 레이어 SUSE Linux enterprise 기반 [높은 가용성 확장 (HAE)](https://www.suse.com/products/highavailability)합니다.

    클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대 한 자세한 내용은 참조 하십시오. [SUSE Linux Enterprise 높은 가용성 확장 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)합니다.

RHEL HA 추가 기능 및 SUSE HAE 둘 다에 작성 됩니다 [Pacemaker](http://clusterlabs.org/)합니다.

아래 다이어그램에서 보듯이으로 두 명의 서버에 저장소가 제공 됩니다. -Corosync 및 Pacemaker-클러스터링 구성 요소는 통신 및 리소스 관리를 조정 합니다. 서버 중 하나에 저장소 리소스와 SQL Server에 연결 되어 있습니다. Pacemaker 오류를 발견 하면 클러스터링 구성 요소 관리 하는 리소스를 다른 노드로 이동 합니다.  

![Red Hat Enterprise Linux 7 공유 디스크 SQL 클러스터](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 이 시점에서 linux Pacemaker와 SQL Server의 통합 Windows에서 WSFC와으로으로 결합 된 않습니다. sql에서 클러스터의 존재에 대 한 지식이 없는, 외부 모든 오케스트레이션은 되며 서비스는 독립 실행형 인스턴스로 Pacemaker에 의해 제어 됩니다. 또한 가상 네트워크 이름은 WSFC 관련, Pacemaker에는 동일한 동등한 옵션이 없습니다. 것으로 예상 되는 @@servername 및 이름을 반환 하는 노드를 클러스터 dmv sys.dm_os_cluster_nodes 및 sys.dm_os_cluster_properties는 레코드가 없는 동안 sys.servers 합니다. 문자열 서버 이름이를 가리키는 연결 문자열을 사용 하는 IP를 사용 하지 있습니다 (아래 설명 됨)는 선택한 서버 이름으로 가상 IP 리소스를 만드는 데 IP를 DNS 서버에 등록 해야 합니다.

## <a name="number-of-instances-and-nodes"></a>인스턴스 수 및 노드

Linux에서 SQL Server와 함께 한 가지 주요 차이점은 있을 수 있습니다만 Linux 서버 마다 SQL Server의 한 설치 합니다. 설치 프로그램을 인스턴스를 라고 합니다. 이 Windows Server 장애 조치 클러스터 (WSFC) 당 최대 25 명의 Fci를 지 원하는 Windows Server와 달리 Linux 기반 FCI만 들이 있는 단일 인스턴스를 의미 합니다. 또한이 하나의 인스턴스가 기본 인스턴스가; Linux에서 명명 된 인스턴스의 한 개념이 없습니다. 

Pacemaker 클러스터 수만 없으므로 최대 16 개의 노드로 Corosync 관련 된 경우 단일 FCI 최대 16 명의 서버를 확장할 수 있습니다. SQL Server의 Standard Edition을 사용 하 여 구현 하는 FCI Pacemaker 클러스터에 최대 16 개의 노드로 구성 된 경우에 클러스터의 최대 두 개의 노드를 지원 합니다.

SQL Server FCI를 사용 하는 SQL Server 인스턴스는 하나의 노드 또는 다른에서 활성입니다.

## <a name="ip-address-and-name"></a>IP 주소와 이름
Linux Pacemaker 클러스터에서 각 SQL Server FCI 자체 고유한 IP 주소와 이름이 필요 합니다. FCI 구성에서 여러 서브넷에 걸쳐 있는 경우 하나의 IP 주소는 서브넷별로 해야 합니다. 응용 프로그램 및 최종 사용자에 게 불필요 Pacemaker 클러스터의 기본 서버에 알아야 하는 FCI를 액세스 하는 고유 이름 및 IP 주소 사용 됩니다.

DNS에서 FCI의 이름을 Pacemaker 클러스터에 생성 되는 FCI 리소스의 이름과 동일 해야 합니다.
이름과 IP 주소가 DNS에 등록 되어야 합니다.

## <a name="shared-storage"></a>공유 저장소
Linux 또는 Windows Server 되었든 관계 없이 모든 Fci는 특정 형태의 공유 저장소에 필요 합니다. FCI를 호스팅할 수 있는 수 있는 모든 서버를이 저장소가 제공 됩니다 하지만 서버 한 대만 언제 든 지 FCI에 대 한 저장소에 사용할 수 있습니다. Linux에서 공유 저장소에 사용할 수 있는 옵션이 있습니다.

- iSCSI
- 네트워크 파일 시스템 (NFS)
- 서버 메시지 블록 (SMB)에서 Windows Server는 약간 다른 옵션이 있습니다. 현재 지원 하지 않는 Linux 기반 Fci에 대 한 한 가지 옵션은 디스크의 로컬에 SQL Server의 임시 작업 영역에는 TempDB에 대 한 노드를 사용 하려면 기능입니다.

여러 위치에 걸쳐 있는 구성에서 하나의 데이터 센터에 저장 된 항목와 동기화 해야 다른 합니다. 장애 조치 될 경우 FCI가 온라인 상태가 수 하 고 저장소는 동일 하 게 나타납니다. 이 내용의 일부 외부 메서드 저장소 복제에 대 한 기본 저장소 하드웨어 또는 소프트웨어 기반 일부 유틸리티를 통해 위배 됩니다. 

>[!NOTE]
>SQL Server 2017 년에 대 한 이러한 서버에 직접 제공 하는 디스크를 사용 하 여 Linux 기반 배포 XFS 또는 EXT4로 포맷 되어야 합니다. 다른 파일 시스템은 현재 지원 되지 않습니다. 변경 내용을 여기에 반영 됩니다.

공유 저장소를 표시 하기 위한 프로세스는 서로 다른 지원 되는 방법에 대 한 같습니다.

- 공유 저장소 구성
- FCI에 대 한 Pacemaker 클러스터의 노드로 역할 하는 서버에 폴더와 저장소를 탑재 합니다.
- 필요한 경우 공유 저장소로 SQL Server 시스템 데이터베이스 이동
- 공유 저장소에 연결 된 각 서버에서 작동 하는 SQL Server 테스트

Linux에서 SQL Server와 함께 한 가지 주요 차이점은는 기본 사용자 데이터 및 로그 파일 위치를 구성할 수는 시스템 데이터베이스인 항상에 존재 해야 합니다 `/var/opt/mssql/data`합니다. Windows Server에서 TempDB를 포함 하 여 시스템 데이터베이스를 이동할 수가 있습니다. 이 팩트 FCI에 대 한 재생 어떻게 공유 저장소로 구성 됩니다.

비 시스템 데이터베이스에 대 한 기본 경로 사용 하 여 변경할 수 있습니다는 `mssql-conf` 유틸리티입니다. 기본값을 변경 하는 방법에 대 한 내용은 [기본 데이터 또는 로그 디렉터리 위치를 변경](sql-server-linux-configure-mssql-conf.md#datadir)합니다. 저장할 수도 있습니다. SQL Server 데이터 및 트랜잭션 다른 위치에 있는 기본 위치; 없는 경우에 적절 한 보안을가지고 있습니다. 위치를 정의할 수 해야 합니다.

다음 항목에서는 Linux 기반 SQL Server FCI에 대 한 지원 되는 저장소 형식을 구성 하는 방법을 설명 합니다.

- [장애 조치 클러스터 인스턴스-iSCSI-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [장애 조치 클러스터 인스턴스-NFS-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [SMB-Linux에서 SQL Server 장애 조치 클러스터 인스턴스-를 구성 합니다.](sql-server-linux-shared-disk-cluster-configure-smb.md)
