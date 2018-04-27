---
title: SQL Server에 대 한 SLES 공유 디스크 클러스터를 구성 | Microsoft Docs
description: SQL Server에 대 한 SUSE Linux Enterprise Server (SLES) 공유 디스크 클러스터를 구성 하 여 높은 가용성을 구현 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.workload: Inactive
ms.openlocfilehash: ce4bc0cec8e235abfde581a3e78b79eeee6740f2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>SQL Server에 대 한 SLES 공유 디스크 클러스터를 구성 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 가이드를 SQL Server SUSE Linux Enterprise Server (SLES)에 대 한 2 노드 공유 디스크 클러스터를 만드는 지침을 제공 합니다. 클러스터링 레이어 SUSE 기반 [높은 가용성 확장 (HAE)](https://www.suse.com/products/highavailability) 기반으로 구축 [Pacemaker](http://clusterlabs.org/)합니다. 

클러스터 구성, 리소스 에이전트 옵션, 관리, 모범 사례 및 권장 사항에 대 한 자세한 내용은 참조 하십시오. [SUSE Linux Enterprise 높은 가용성 확장 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)합니다.

## <a name="prerequisites"></a>필수 구성 요소

다음과 같은 종단 간 시나리오를 완료 하려면 두 노드 클러스터와 NFS 공유를 구성 하려면 다른 서버를 배포 하는 두 개의 컴퓨터가 필요 합니다. 아래 단계 이러한 서버는 구성 하는 방법에 대해 간략하게 설명 합니다.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>설정 하 고 각 클러스터 노드에서 운영 체제를 구성 합니다.

클러스터 노드에서 운영 체제를 구성 하는 첫 번째 단계가입니다. 이 연습 과정에 대 한 유효한 구독으로 SLES HA 추가 기능에 대해 사용 합니다.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>설치 하 고 각 클러스터 노드에서 SQL Server 구성

1. 설치 하 고 SQL Server를 두 노드에 모두 설치 합니다. 자세한 내용은 참조 [Linux에서 SQL Server 설치](sql-server-linux-setup.md)합니다.
2. 주 서버와 구성의 목적을 위해 보조로 다른으로 노드 하나를 지정 합니다. 다음에 대 한 이러한 용어를 사용 하 여이 가이드입니다. 
3. 보조 노드에서 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다. 다음 예제에서는 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > 설치 시 서버 마스터 키가 생성 된 SQL Server 인스턴스에 대 한 후 배치에 `/var/opt/mssql/secrets/machine-key`합니다. Linux에서 SQL Server는 항상 mssql 라는 로컬 계정으로 실행 됩니다. 로컬 계정을 이기 때문에 해당 id 노드 간에 공유 되지 않습니다. 따라서 서버 마스터 키를 해독 하 여 각 로컬 mssql 계정에 액세스할 수 있도록 암호화 키를 주 노드에서 각 보조 노드로 복사 해야 합니다.
4. 주 노드에서 Pacemaker에 대 한 SQL server 로그인을 만들고 실행에 로그인 권한을 부여 `sp_server_diagnostics`합니다. SQL Server를 실행 하는 노드를 확인 하려면이 계정을 사용 하는 pacemaker 합니다.

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
5. 주 노드에서 중지 하 고 SQL Server를 사용 하지 않도록 설정 합니다.
6. 지침을 따르고 [SUSE 설명서에서](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) 를 구성 하 여 각 클러스터 노드에 대 한 호스트 파일을 업데이트 합니다. 호스트 파일에는 IP 주소 및 모든 클러스터 노드의 이름이 포함 되어야 합니다.

    실행 하는 현재 노드에의 IP 주소를 확인 합니다.

    ```bash
    sudo ip addr show
    ```

    각 노드에서 다음 컴퓨터 이름을 설정 합니다. 각 노드의 고유한 이름을 15 자 이하인 합니다. 컴퓨터 이름을 추가 하 여 설정 `/etc/hostname` 를 사용 하 여 [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) 또는 [수동으로](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html)합니다.

    다음 예제와 `/etc/hosts` 라는 두 개의 노드에 대 한 추가 내용은 `SLES1` 및 `SLES2`합니다.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > 모든 클러스터 노드에 SSH를 통해 서로 액세스할 수 있어야 합니다. hb_report 또는 crm_report(문제 해결용), Hawk의 History Explorer 등의 도구에는 노드 간에 암호 없는 SSH 액세스가 필요합니다. 그렇지 않으면 현재 노드에서만 데이터를 수집할 수 있습니다. -X 옵션을 사용 하는 비표준 SSH 포트를 사용 하는 경우 ([매뉴얼 페이지를 참조](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). 예를 들어 SSH 포트가 3479 이면와 crm_report를 호출 합니다.
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >자세한 내용은 [관리 가이드에서]를 참조 하세요. (https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

다음 섹션에서 공유 저장소를 구성 하 고 해당 저장소에 데이터베이스 파일 이동 합니다.  

## <a name="configure-shared-storage-and-move-database-files"></a>공유 저장소를 구성 하 고 데이터베이스 파일 이동

공유 저장소를 제공 하는 솔루션의 여러 가지가 있습니다. 이 연습이 NFS를 사용 하 여 공유 저장소를 구성 하는 방법을 보여 줍니다. 모범 사례를 따르고 NFS를 보호 하기 위해 Kerberos를 사용 하려면이 좋습니다. 

- [NFS와 파일 시스템 공유](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

이 지침을 준수 하지 않는 경우 데이터 파일에 액세스할 수 SQL 노드의 IP 주소를 스푸핑 하 고 네트워크에 액세스할 수 있는 모든 사용자. 늘 그렇듯이 위협을 하면 프로덕션 환경에서 사용 하기 전에 시스템을 모델링 해야 합니다. 

또 다른 저장소 옵션 SMB 파일 공유를 사용 하는 것입니다.

- [SUSE 문서의 samba 섹션](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>NFS 서버 구성

NFS 서버를 구성 하려면 SUSE 설명서에서 다음 단계를 참조: [NFS 서버 구성](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server)합니다.

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>NFS 공유 저장소에 연결 하려면 모든 클러스터 노드 구성

SQL Server 데이터베이스 파일 경로 탑재 하도록 NFS를 공유 저장소 위치를 가리키도록 클라이언트를 구성 하기 전에 임시 위치로 복사할 나중에 공유 하려면 데이터베이스 파일을 저장 해야 합니다.

1. **주 노드의**, 데이터베이스 파일을 임시 위치에 저장 합니다. 다음 스크립트에서는 새로운 임시 디렉터리를 만듭니다 하 고, 데이터베이스 파일을 새 디렉터리를 복사, 오래 된 데이터베이스 파일을 제거 합니다. SQL Server mssql 로컬 사용자로 실행 되는 탑재 된 공유에 데이터 전송, 후 로컬 사용자가 공유에 대 한 읽기 / 쓰기 액세스 있는지 확인 해야 합니다. 

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
    > SUSE의 모범 사례 및 항상 사용 가능한 NFS 저장소와 관련 한 권장 사항을 따라야 하는 것이 좋습니다.: [DRBD 및 Pacemaker 항상 사용 가능한 NFS 저장소](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html)합니다.

2. SQL Server 새 파일 경로에 성공적으로 시작을 확인 합니다. 각 노드에서이 작업을 수행 합니다. 이 시점에서 한 번에 하나의 노드만 SQL Server를 실행 해야 합니다. 실행할 수 없습니다 둘 다 동시에는 둘 다 동시에 (을 방지 하려면 실수로 두 노드에서 모두 SQL Server를 시작 하는 파일 시스템 클러스터 리소스를 사용 하 여 공유의 다른 노드에 의해 두 번 탑재 되어 있지 않으면 되도록) 데이터 파일에 액세스 하려면 시도 하기 때문에. 다음 명령을 SQL Server를 시작 하 고 상태를 확인 한 다음 SQL Server를 중지 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

이 시점에서 SQL Server의 두 인스턴스는 공유 저장소에 있는 데이터베이스 파일을 사용 하 여 실행 하도록 구성 됩니다. 다음 단계 Pacemaker에 대 한 SQL Server를 구성 하는 것입니다. 

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

다음 단계에서는 SQL Server에 대 한 클러스터 리소스를 구성 하는 방법에 설명 합니다. 사용자 지정 하는 두 가지 설정이 있습니다.

- **SQL Server 리소스 이름**: 클러스터 된 SQL Server 리소스에 대 한 이름입니다. 
- **제한 시간 값**: 시간 제한 값은 클러스터 된 리소스가 온라인 상태가 되는 동안 대기 하는 시간입니다. SQL Server 하기 위해 수행할 수 있어야 하는 경우 SQL server는 `master` 데이터베이스를 온라인 상태로 있습니다. 

사용자 환경에 대 한 다음 스크립트에서 값을 업데이트 합니다. 구성 및 클러스터 된 서비스를 시작 하는 노드 하나에서 실행 합니다.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

예를 들어 다음 스크립트는 mssqlha 라는 SQL Server에서 클러스터 된 리소스를 만듭니다. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

구성이 커밋된 후 가상 IP 리소스와 동일한 노드에서 SQL Server가 시작 됩니다. 

자세한 내용은 참조 [구성 및 관리 클러스터 리소스 (명령줄)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)합니다. 

### <a name="verify-that-sql-server-is-started"></a>SQL Server가 시작 되었는지 확인 합니다. 

SQL Server 시작 되어 있는지를 확인 하려면 실행는 **crm 상태** 명령:

```bash
crm status
```

다음 예에서는 클러스터형 리소스로 Pacemaker가 성공적으로 시작 하는 경우 결과 보여줍니다. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>클러스터 리소스 관리

클러스터 리소스를 관리 하려면 다음 SUSE 항목을 참조: [클러스터 리소스 관리](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>수동 장애 조치(manual failover)

자동으로 장애 조치 (또는 마이그레이션)을 하드웨어 또는 소프트웨어 오류가 발생할 경우 클러스터의 다른 노드로 구성 된 리소스가 있지만 Pacemaker GUI 또는 명령줄을 사용 하는 클러스터의 다른 노드로 리소스를 직접 이동할 수 있습니다. 

이 작업에 대 한 마이그레이션 명령을 사용 합니다. 예를 들어 마이그레이션할 SQL 리소스 클러스터 노드 이름 SLES2 실행 합니다. 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>추가 리소스

[SUSE Linux Enterprise 고가용성 확장-관리 가이드](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
