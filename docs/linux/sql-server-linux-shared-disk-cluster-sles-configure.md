---
title: SQL Server에 대 한 SLES 공유 디스크 클러스터 구성 | Microsoft Docs
description: SQL Server 용 SUSE Linux Enterprise Server (SLES) 공유 디스크 클러스터를 구성 하 여 고가용성을 구현 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 84c242d3c7c8e38642f1ee76f109f90a1ea9520e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635821"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>SQL Server에 대 한 SLES 공유 디스크 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드는 SUSE Linux Enterprise Server (SLES) SQL Server에 대 한 2 노드 공유 디스크 클러스터를 만드는 지침을 제공 합니다. SUSE 클러스터링 계층 더해서 [높은 가용성 확장 (HAE)](https://www.suse.com/products/highavailability) 기반으로 구축 [Pacemaker](http://clusterlabs.org/)합니다. 

클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대 한 자세한 내용은 참조 하세요. [SUSE Linux Enterprise 높은 가용성 확장 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)합니다.

## <a name="prerequisites"></a>사전 요구 사항

다음 종단 간 시나리오를 완료 하려면 두 개의 머신을 두 노드 클러스터와 NFS 공유를 구성 하려면 다른 서버를 배포 해야 합니다. 아래 단계는이 서버를 구성 하는 방법을 간략하게 설명 합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>설정 하 고 각 클러스터 노드의 운영 체제를 구성 합니다.

먼저는 클러스터 노드의 운영 체제를 구성 하는 것입니다. 이 연습에서는 HA 추가 기능에 대 한 SLES을 유효한 구독을 사용 하 여 사용 합니다.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 SQL Server 구성

1. 설치 하 고 두 노드에서 모두 SQL Server를 설치 합니다. 자세한 지침은 [Linux의 SQL Server 설치](sql-server-linux-setup.md)합니다.
2. 기본 및 보조 구성의 목적으로 다른 노드 하나를 지정 합니다. 이러한 용어를 사용 하 여 다음에 대 한이 가이드입니다. 
3. 보조 노드를 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다. 다음 예에서는 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > 설치 시 서버 마스터 키를 SQL Server 인스턴스에 대해 생성 되며에 배치 `/var/opt/mssql/secrets/machine-key`합니다. Linux에서 SQL Server mssql 라는 로컬 계정으로 항상 실행 됩니다. 로컬 계정 이기 때문에 해당 id는 노드 간에 공유 되지 않습니다. 따라서 서버 마스터 키를 해독 하도록 각 로컬 mssql 계정에 액세스할 수 있도록 각 보조 노드에 주 노드에서 암호화 키를 복사 해야 합니다.
4. 주 노드에서 Pacemaker 용 SQL server 로그인 만들기 및 실행에 로그인 권한을 부여 `sp_server_diagnostics`합니다. Pacemaker는 노드는 SQL Server를 실행 중인지 확인 하려면이 계정을 사용 합니다.

    ```bash
    sudo systemctl start mssql-server
    ```
    'Sa' 계정으로 SQL Server 마스터 데이터베이스에 연결 하 고 다음을 실행 합니다.

    ```tsql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. 주 노드를 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다.
6. 지침을 따릅니다 [SUSE 설명서의](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) 구성 하 고 각 클러스터 노드에 대 한 호스트 파일을 업데이트 합니다. '호스트' 파일에는 IP 주소 및 모든 클러스터 노드의 이름이 포함 되어야 합니다.

    현재 실행 노드의 IP 주소를 확인:

    ```bash
    sudo ip addr show
    ```

    각 노드의 컴퓨터 이름을 설정 합니다. 각 노드는 고유한 이름을 15 자 이하의 합니다. 컴퓨터 이름을 추가 하 여 설정 `/etc/hostname` 를 사용 하 여 [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) 하거나 [수동으로](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html)합니다.

    다음 예와 `/etc/hosts` 라는 두 노드에 대 한 추가 기능을 사용 하 여 `SLES1` 고 `SLES2`입니다.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > 모든 클러스터 노드에 SSH를 통해 서로 액세스할 수 있어야 합니다. hb_report 또는 crm_report(문제 해결용), Hawk의 History Explorer 등의 도구에는 노드 간에 암호 없는 SSH 액세스가 필요합니다. 그렇지 않으면 현재 노드에서만 데이터를 수집할 수 있습니다. 비표준 SSH 포트를 사용 하는 경우-X 옵션을 사용 하 여 ([매뉴얼 페이지를 참조](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). 예를 들어 SSH 포트가 3479 이면는 crm_report 사용 하 여 호출 합니다.
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >자세한 내용은 [관리 가이드]를 참조 하세요. (https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

다음 섹션에서 공유 저장소를 구성 하 고 해당 저장소에 데이터베이스 파일을 이동 합니다.  

## <a name="configure-shared-storage-and-move-database-files"></a>공유 저장소를 구성 하 고 데이터베이스 파일 이동

공유 저장소를 제공 하기 위한 솔루션도 여러 가지가 있습니다. 이 연습에서는 NFS를 사용 하 여 공유 저장소를 구성 하는 방법을 보여 줍니다. 모범 사례를 따르고 Kerberos를 사용 하 여 NFS를 보호 하는 좋습니다. 

- [NFS를 사용 하 여 파일 시스템 공유](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

이 지침을 따르지 않으면 SQL 노드의 IP 주소를 스푸핑 하 고 네트워크에 액세스할 수 있는 모든 사용자 데이터 파일에 액세스할 수 있게 됩니다. 늘 그렇듯이 위협을 하면 프로덕션 환경에서 사용 하기 전에 시스템을 모델링 해야 합니다. 

또 다른 저장소 옵션 SMB 파일 공유를 사용 하는 것입니다.

- [SUSE 설명서의 samba 섹션](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>NFS 서버 구성

NFS 서버를 구성 하려면 SUSE 설명서의 다음 단계를 참조 하세요. [NFS 서버 구성](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server)합니다.

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 공유 저장소에 연결 하려면 모든 클러스터 노드 구성

SQL Server 데이터베이스 파일 경로 탑재 하는 NFS 공유 저장소 위치를 가리키도록 클라이언트를 구성 하기 전에 임시 위치로 복사한 나중에 공유 하려면 데이터베이스 파일을 저장 하 고 있는지 확인 합니다.

1. **주 노드에서**, 데이터베이스 파일을 임시 위치에 저장 합니다. 다음 스크립트를 새 임시 디렉터리를 만듭니다, 그리고 데이터베이스 파일을 새 디렉터리를 복사 및 이전 데이터베이스 파일을 제거 합니다. SQL Server mssql 로컬 사용자로 실행 되 면 후 탑재 된 공유에 데이터 전송, 로컬 사용자에 공유에 대 한 읽기 / 쓰기 액세스 있는지 확인 해야 합니다. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    모든 클러스터 노드에서 NFS 클라이언트를 구성 합니다.

    - [클라이언트 구성](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > SUSE의 모범 사례 및 항상 사용 가능한 NFS 저장소에 대 한 권장 사항을 따라야 하는 것이 좋습니다: [DRBD 및 Pacemaker를 사용 하 여 항상 사용 가능한 NFS 저장소](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html)합니다.

2. SQL Server의 새 파일 경로 사용 하 여 성공적으로 시작 하는 유효성을 검사 합니다. 각 노드에서이 작업을 수행 합니다. 이 시점에서 한 번에 하나의 노드만 SQL Server를 실행 해야 합니다. 실행할 수 없습니다 둘 다 동시에는 모두 데이터 파일에 동시에 (을 실수로 두 노드에서 모두 SQL Server를 시작 하지 않도록 클러스터 파일 시스템 리소스를 사용 하 여 다른 노드에 의해 두 번 공유를 탑재 되지 않은 되도록) 액세스를 시도 하기 때문입니다. SQL Server 시작한 상태를 확인 한 다음 SQL Server를 중지 하는 다음 명령을 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

이 시점에서 SQL Server의 두 인스턴스는 공유 저장소에 있는 데이터베이스 파일을 사용 하 여 실행 하도록 구성 됩니다. Pacemaker 용 SQL Server를 구성 하려면 다음 단계가입니다. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 Pacemaker 구성

1. **두 클러스터 노드에서 모두 Pacemaker 로그인을 위한 SQL Server 사용자 이름 및 암호를 저장할 파일을 만듭니다.** 다음 명령은 이 파일을 만들고 채웁니다.

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **모든 클러스터 노드는 SSH를 통해 서로 액세스할 수 있어야 합니다**. hb_report 또는 crm_report(문제 해결용), Hawk의 History Explorer 등의 도구에는 노드 간에 암호 없는 SSH 액세스가 필요합니다. 그렇지 않으면 현재 노드에서만 데이터를 수집할 수 있습니다. 표준이 아닌 SSH 포트를 사용할 경우 -X 옵션을 사용합니다(기본 페이지 참조). 예를 들어 SSH 포트가 3479이면 함께 hb_report를 호출합니다.

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    자세한 내용은 [System Requirements and Recommendations in the SUSE documentation](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)(SUSE 설명서의 시스템 요구 사항 및 권장 사항)을 참조하세요.

3. **고가용성 확장을 설치합니다**. 확장을 설치하려면 다음 SUSE 항목의 단계를 따릅니다.
    
    [Installation and Setup Quick Start](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)(설치 및 설정 빠른 시작)

4. **SQL Server용 FCI 리소스 에이전트를 설치합니다**. 두 노드에서 모두 다음 명령을 실행합니다.

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **첫 번째 노드를 자동으로 설정합니다**. 다음 단계에서는 첫 번째 노드 SLES1을 구성하여 실행 중인 단일 노드 클러스터를 설정합니다. SUSE 항목 [Setting Up the First Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)(첫 번째 노드 설정)의 지침을 따릅니다.

    완료되면 `crm status`를 사용하여 클러스터 상태를 확인합니다.
    ```bash
    crm status
    ```

    단일 노드 SLES1이 구성된 것으로 표시됩니다.

6. **기존 클러스터에 노드를 추가합니다**. 그 다음에 SLES2 노드를 클러스터에 조인합니다. SUSE 항목 [Adding the Second Node](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node)(두 번째 노드 추가)의 지침을 따릅니다.
    
    완료되면 **crm status**를 사용하여 클러스터 상태를 확인합니다. 두 번째 노드를 성공적으로 추가한 경우 출력이 다음과 같이 표시됩니다.
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr**는 초기 단일 노드 클러스터 설정 중에 구성된 가상 IP 클러스터 리소스입니다.

7.  **제거 절차**. 클러스터에서 노드를 제거해야 할 경우 **ha-cluster-remove** 부트스트랩 스크립트를 사용합니다. 자세한 내용은 [Overview of the Bootstrap Scripts](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap)(부트스트랩 스크립트 개요)를 참조하세요.  

## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server에 대 한 클러스터 리소스를 구성 합니다.

다음 단계를 SQL Server에 대 한 클러스터 리소스를 구성 하는 방법에 설명 합니다. 사용자 지정 해야 하는 방법은 두 가지 설정이 있습니다.

- **SQL Server 리소스 이름**: 클러스터형된 SQL Server 리소스의 이름입니다. 
- **시간 제한 값**: 시간 제한 값은 클러스터 된 리소스가 온라인 상태가 되는 동안 대기 하는 시간의 양입니다. SQL Server, SQL Server 상태로 전환 하는 데 예상 되는 시간입니다는 `master` 온라인 데이터베이스입니다. 

사용자 환경에 대 한 다음 스크립트에서 값을 업데이트 합니다. 구성 및 클러스터 된 서비스를 시작 하려면 하나의 노드에서 실행 합니다.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

예를 들어, 다음 스크립트를 mssqlha 라는 SQL Server 클러스터형 리소스를 만듭니다. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

구성을 커밋한 후 가상 IP 리소스와 동일한 노드에서 SQL Server가 시작 됩니다. 

자세한 내용은 [구성 및 클러스터 리소스 관리 (명령줄)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)합니다. 

### <a name="verify-that-sql-server-is-started"></a>SQL Server가 시작 되었는지 확인 합니다. 

SQL Server가 시작 되었는지 확인 하려면 실행 합니다 **crm 상태** 명령:

```bash
crm status
```

다음 예제에서는 Pacemaker 클러스터 된 리소스와 성공적으로 시작 하는 경우 결과 보여 줍니다. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>클러스터 리소스 관리

클러스터 리소스를 관리 하려면 다음 SUSE 항목을 참조 하세요. [클러스터 리소스 관리](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>수동 장애 조치(manual failover)

리소스를 Pacemaker GUI 또는 명령줄을 사용 하 여 클러스터의 다른 노드로 수동으로 이동할 수 있지만 리소스를 자동으로 장애 조치 (마이그레이션) 하드웨어 또는 소프트웨어 오류가 발생할 경우 클러스터의 다른 노드로 구성 됩니다, . 

이 태스크에 대 한 마이그레이션 명령을 사용 합니다. 예를 들어, 마이그레이션하려는 클러스터 노드 이름 그 다음에 SLES2 SQL 리소스가 실행 합니다. 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>추가 자료

[SUSE Linux Enterprise 고가용성 확장-관리 가이드](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
