---
title: SQL Server의 SLES 공유 디스크 클러스터 구성
description: SQL Server에 대해 SLES(SUSE Linux Enterprise Server) 공유 디스크 클러스터를 구성하여 고가용성을 구현합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 70701d5c0103da089444177db1143066d0c862cd
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032226"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>SQL Server의 SLES 공유 디스크 클러스터 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드에서는 SLES(SUSE Linux Enterprise Server)에서 SQL Server에 대해 2노드 공유 디스크 클러스터를 만들기 위한 지침을 제공합니다. 클러스터링 계층은 [Pacemaker](https://clusterlabs.org/)를 토대로 구축된 SUSE [HAE(고가용성 확장)](https://www.suse.com/products/highavailability)를 기준으로 합니다. 

클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대한 자세한 내용은 [SUSE Linux Enterprise High Availability Extension 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

다음 엔드투엔드 시나리오를 완료하려면 2노드 클러스터와 다른 서버를 배포하여 NFS 공유를 구성하는 두 대의 컴퓨터가 필요합니다. 아래 단계에서는 이러한 서버를 구성하는 방법을 간략하게 설명합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>각 클러스터 노드에서 운영 체제 설정 및 구성

첫 번째 단계는 클러스터 노드에서 운영 체제를 구성하는 것입니다. 이 연습에서는 HA 추가 기능을 위한 유효한 구독과 함께 SLES를 사용합니다.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>각 클러스터 노드에 SQL Server 설치 및 구성

1. 두 노드에 SQL Server를 설치하고 설정합니다. 자세한 지침은 [Linux에서 SQL Server 설치](sql-server-linux-setup.md)를 참조하세요.
2. 구성의 목적에 따라 노드 하나를 주 노드로 지정하고 다른 노드를 보조 노드로 지정합니다. 이 지침에 따라 이러한 용어를 사용합니다. 
3. 보조 노드에서 SQL Server를 중지하고 사용하지 않도록 설정합니다. 다음 예제에서는 SQL Server를 중지하고 사용하지 않도록 설정합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > 설정 시에 SQL Server 인스턴스에 대해 서버 마스터 키가 생성되고 `/var/opt/mssql/secrets/machine-key`에 배치됩니다. Linux에서 SQL Server는 항상 mssql이라는 로컬 계정으로 실행됩니다. 이 계정은 로컬 계정이므로 해당 ID가 노드 간에 공유되지 않습니다. 따라서 각 로컬 mssql 계정이 서버 마스터 키의 암호를 해독하기 위해 액세스할 수 있도록 주 노드에서 각 보조 노드로 암호화 키를 복사해야 합니다.
4. 주 노드에서 Pacemaker에 대한 SQL server 로그인을 만들고 `sp_server_diagnostics`를 실행하기 위한 로그인 권한을 부여합니다. Pacemaker는 이 계정을 사용하여 SQL Server를 실행 중인 노드를 확인합니다.

    ```bash
    sudo systemctl start mssql-server
    ```
    'sa' 계정을 사용하여 SQL Server master 데이터베이스에 연결하고 다음을 실행합니다.

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. 주 노드에서 SQL Server를 중지하고 사용하지 않도록 설정합니다.
6. [SUSE 설명서](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html)의 지시에 따라 각 클러스터 노드용 hosts 파일을 구성하고 업데이트합니다. 'hosts' 파일은 모든 클러스터 노드의 IP 주소와 이름을 포함해야 합니다.

    현재 노드의 IP 주소를 확인하려면 다음을 실행합니다.

    ```bash
    sudo ip addr show
    ```

    각 노드에서 컴퓨터 이름을 설정합니다. 각 노드에 15자 이하의 고유 이름을 지정합니다. [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html)를 사용하거나 [수동으로](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html) `/etc/hostname`에 추가하여 컴퓨터 이름을 설정합니다.

    다음 예제에서는 `SLES1` 및 `SLES2`라는 두 노드를 추가하여 `/etc/hosts`를 보여 줍니다.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > 모든 클러스터 노드는 SSH를 통해 서로 액세스할 수 있어야 합니다. hb_report 또는 crm_report(문제 해결용), Hawk의 History Explorer 등의 도구에는 노드 간에 암호 없는 SSH 액세스가 필요합니다. 그렇지 않으면 현재 노드에서만 데이터를 수집할 수 있습니다. 표준이 아닌 SSH 포트를 사용할 경우 -X 옵션을 사용합니다([기본 페이지 참조](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). 예를 들어, SSH 포트가 3479이면 다음을 사용하여 crm_report를 호출합니다.
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >자세한 내용은 [관리 가이드]를 참조하세요.(https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

다음 섹션에서는 공유 스토리지를 구성하고 데이터베이스 파일을 해당 스토리지로 이동합니다.  

## <a name="configure-shared-storage-and-move-database-files"></a>공유 스토리지 구성 및 데이터베이스 파일 이동

공유 스토리지를 제공하는 다양한 솔루션이 있습니다. 이 연습에서는 NFS를 사용하여 공유 스토리지를 구성하는 방법을 보여 줍니다. 모범 사례를 따르고 Kerberos를 사용하여 NFS를 보호하는 것이 좋습니다. 

- [NFS를 사용하여 파일 시스템 공유](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

이 지침을 따르지 않으면 네트워크에 액세스하고 SQL 노드의 IP 주소를 스푸핑할 수 있는 누구든지 사용자의 데이터 파일에 액세스할 수 있습니다. 항상 그런 것처럼 프로덕션 환경에서 사용하기 전에 시스템에 대해 위협 모델링을 수행해야 합니다. 

또 다른 스토리지 옵션은 다음과 같이 SMB 파일 공유를 사용하는 것입니다.

- [SUSE 설명서의 Samba 섹션](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>NFS 서버 구성

NFS 서버를 구성하려면 SUSE 설명서에서 다음 단계를 참조하세요. [NFS 서버 구성](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server).

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 공유 스토리지에 연결하도록 모든 클러스터 노드 구성

공유 스토리지 위치를 가리키는 SQL Server 데이터베이스 파일 경로를 탑재하도록 클라이언트 NFS를 구성하기 전에, 데이터베이스 파일을 나중에 공유에 복사할 수 있도록 임시 위치에 저장해야 합니다.

1. **주 노드에서만** 데이터베이스 파일을 임시 위치에 저장합니다. 다음 스크립트는 새 임시 디렉터리를 만들고, 데이터베이스 파일을 새 디렉터리에 복사하고, 이전 데이터베이스 파일을 제거합니다. SQL Server는 로컬 사용자 mssql로 실행되므로, 탑재된 공유로 데이터가 전송된 후 로컬 사용자에게 공유에 대한 읽기/쓰기 권한이 있는지 확인해야 합니다. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    다음과 같이 모든 클러스터 노드에서 NFS 클라이언트를 구성합니다.

    - [클라이언트 구성](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > 고가용성 NFS 스토리지와 관련해서 SUSE의 모범 사례 및 다음 권장 사항을 따르는 것이 좋습니다. [DRBD 및 Pacemaker를 사용하는 고가용성 NFS 스토리지](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html).

2. SQL Server가 새 파일 경로를 사용하여 시작되는지 확인합니다. 각 노드에서 이러한 확인 작업을 수행합니다. 이때 한 번에 하나의 노드만 SQL Server를 실행해야 합니다. 두 노드 모두 데이터 파일에 동시에 액세스하려고 하므로 동시에 실행할 수 없습니다(두 노드에서 실수로 SQL Server를 시작하지 않도록 하려면 파일 시스템 클러스터 리소스를 사용하여 해당 노드가 다른 노드에서 두 번 탑재되지 않도록 확인). 다음 명령은 SQL Server를 시작하고, 상태를 확인하고, SQL Server를 중지합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

이때 SQL Server의 두 인스턴스는 모두 공유 스토리지의 데이터베이스 파일을 사용하여 실행되도록 구성됩니다. 다음 단계는 Pacemaker에 맞게 SQL Server를 구성하는 것입니다. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>각 클러스터 노드에 Pacemaker 설치 및 구성

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

## <a name="configure-the-cluster-resources-for-sql-server"></a>SQL Server의 클러스터 리소스 구성

다음 단계에서는 SQL Server의 클러스터 리소스를 구성하는 방법을 설명합니다. 사용자 지정해야 하는 두 가지 설정이 있습니다.

- **SQL Server 리소스 이름**: 클러스터형 SQL Server 리소스의 이름입니다. 
- **제한 시간 값**: 제한 시간 값은 리소스가 온라인 상태가 되는 동안 클러스터가 대기하는 시간입니다. SQL Server의 경우에는 SQL Server에서 `master` 데이터베이스를 온라인 상태로 전환하는 데 필요한 시간입니다. 

작업 환경에서는 다음 스크립트의 값을 업데이트합니다. 한 노드에서를 실행하여 클러스터형 서비스를 구성하고 시작합니다.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

예를 들어, 다음 스크립트는 mssqlha라는 SQL Server 클러스터형 리소스를 만듭니다. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

구성이 커밋되면 SQL Server는 가상 IP 리소스와 동일한 노드에서 시작됩니다. 

자세한 내용은 [클러스터 리소스 구성 및 관리(명령줄)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)를 참조하세요. 

### <a name="verify-that-sql-server-is-started"></a>SQL Server가 시작되었는지 확인합니다. 

SQL Server가 시작되었는지 확인하려면 **crm status** 명령을 실행합니다.

```bash
crm status
```

다음 예제에서는 Pacemaker가 클러스터형 리소스로 시작된 경우의 결과를 보여 줍니다. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>클러스터 리소스 관리

클러스터 리소스를 관리하려면 다음 SUSE 항목을 참조하세요. [클러스터 리소스 관리](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>수동 장애 조치(manual failover)

리소스는 하드웨어 또는 소프트웨어 장애가 발생할 경우 클러스터의 다른 노드로 자동 장애 조치(failover) 또는 마이그레이션하도록 구성되지만, Pacemaker GUI 또는 명령줄을 사용하여 리소스를 클러스터의 다른 노드로 수동으로 이동할 수도 있습니다. 

이 작업에는 migrate 명령을 사용합니다. 예를 들어, SQL 리소스를 클러스터 노드 이름 SLES2로 마이그레이션하려면 다음을 실행합니다. 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>추가 리소스

[SUSE Linux Enterprise 고가용성 확장 - 관리 가이드](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
