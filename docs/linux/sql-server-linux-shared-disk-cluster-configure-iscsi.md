---
title: 장애 조치(failover) 클러스터 인스턴스 스토리지 iSCSI 구성 - SQL Server on Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 0d52038d3e556ecc2202fd1066dc2638bfe14183
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032397"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>장애 조치(failover) 클러스터 인스턴스 구성 - iSCSI - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 FCI(장애 조치(failover) 클러스터 인스턴스)에 iSCSI 스토리지를 구성하는 방법을 설명합니다. 

## <a name="configure-iscsi"></a>iSCSI 구성 
iSCSI는 네트워크를 사용하여 대상으로 알려진 서버에서 서버로 디스크를 제공합니다. iSCSI 대상에 연결하는 서버에는 iSCSI 초기자가 구성되어 있어야 합니다. 대상의 디스크에 액세스할 수 있어야 하는 초기자만 액세스할 수 있도록 해당 디스크에 명시적 권한을 부여합니다. 대상 자체는 가용성과 안정성이 높아야 합니다.

### <a name="important-iscsi-target-information"></a>중요한 iSCSI 대상 정보
사용할 원본 유형과 관련되기 때문에 이 섹션에서는 iSCSI 대상을 구성하는 방법을 설명하지 않지만, 클러스터 노드에서 사용되는 디스크에 대한 보안이 구성되어 있는지 확인하세요.  

Linux 기반 iSCSI 대상을 사용하는 경우 FCI 노드에서 대상을 구성하면 안 됩니다. 성능 및 가용성을 위해 iSCSI 네트워크는 원본 및 클라이언트 서버 모두에서 일반 네트워크 트래픽에 사용되는 네트워크와 분리되어야 합니다. iSCSI에 사용되는 네트워크는 빨라야 합니다. 네트워크는 일부 프로세서 대역폭을 사용하므로, 일반 서버를 사용하는 경우 이에 따라 계획해야 합니다.
대상에서 완료되도록 하려면 가장 중요한 작업은 FCI에 참여하는 서버만 액세스할 수 있도록 적절한 권한을 생성되는 디스크에 할당하는 것입니다. linuxnodes1이 생성되는 이름인 Microsoft iSCSI 대상의 예제가 아래에 나와 있으며, 이 경우 노드의 IP 주소가 할당되므로 NewFCIDisk1.vhdx가 노드에 표시됩니다.

![초기자][1]

### <a name="instructions"></a>Instructions

이 섹션에서는 FCI의 노드로 사용할 서버에서 iSCSI 초기자를 구성하는 방법을 설명합니다. 지침은 RHEL 및 Ubuntu와 동일하게 적용됩니다.

지원되는 배포의 iSCSI 초기자에 대한 자세한 내용은 다음 링크를 참조하세요.
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  FCI 구성에 참여할 서버 중 하나를 선택합니다. 어떤 서버를 선택하든 상관이 없습니다. iSCSI는 전용 네트워크에 있어야 하므로 해당 네트워크를 인식하고 사용하도록 iSCSI를 구성합니다. `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new`를 실행합니다. 여기서 `<iSCSIIfaceName>`은 네트워크의 고유하거나 친숙한 이름입니다. 다음 예제에서는 `iSCSINIC`를 사용합니다.
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  `/var/lib/iscsi/ifaces/iSCSIIfaceName`을 편집합니다. 다음 값이 완전히 입력되었는지 확인합니다.

    - iface.net_ifacename은 OS에 표시된 네트워크 카드의 이름입니다.
    - iface.hwaddress는 아래에서 이 인터페이스에 대해 만들 고유한 이름의 MAC 주소입니다.
    - iface.ipaddress
    - iface.subnet_Mask 

    다음 예제를 참조하십시오.

    ![iSCSITargetSettings][2]

3.  iSCSI 대상을 찾습니다.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName>은 네트워크의 고유한/친숙한 이름이고, \<TargetIPAddress>는 iSCSI 대상의 IP 주소이고, \<TargetPort>는 iSCSI 대상의 포트입니다. 

    ![iSCSITargetResults][3]

 
4.  대상에 로그인

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName>은 네트워크의 고유한/친숙한 이름이고, \<TargetIPAddress>는 iSCSI 대상의 IP 주소입니다.

    ![iSCSITargetLogin][4]

5.  iSCSI 대상에 대한 연결이 있는지 확인합니다.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  iSCSI 연결 디스크를 확인합니다.

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  iSCSI 디스크에서 물리적 볼륨을 만듭니다.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<devicename>은 이전 단계의 디바이스 이름입니다. 

 
8.  iSCSI 디스크에서 볼륨 그룹을 만듭니다. 단일 볼륨 그룹에 할당된 디스크는 풀 또는 컬렉션으로 표시됩니다. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName>은 볼륨 그룹의 이름이고, \<devicename>은 6단계의 디바이스 이름입니다. 
 
9.  디스크의 논리 볼륨을 만들고 확인합니다.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<size>는 만들려는 볼륨의 크기이며 G(기가바이트), T(테라바이트) 등을 사용하여 지정할 수 있고, \<LogicalVolumeName>은 논리 볼륨의 이름이고, \<VolumeGroupName>은 이전 단계의 볼륨 그룹 이름입니다. 

    아래 예제에서는 25GB 볼륨을 만듭니다.
 
    ![Create25GBVol][10]

10. `sudo lvs`를 실행하여 생성된 LVM을 확인합니다.
 
11. 지원되는 파일 시스템을 사용하여 논리 볼륨을 포맷합니다. EXT4의 경우 다음 예제를 사용합니다.

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName>은 이전 단계의 볼륨 그룹 이름입니다. \<LogicalVolumeName>은 이전 단계의 논리 볼륨 이름입니다.  

12. 시스템 데이터베이스 또는 기본 데이터 위치에 저장된 항목의 경우 다음 단계를 수행합니다. 그렇지 않으면 13단계로 건너뜁니다.

   *    작업 중인 서버에서 SQL Server가 중지되었는지 확인합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    슈퍼 사용자로 완전히 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    sudo -i
    ```

   *    mssql 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    su mssql
    ```

   *    SQL Server 데이터와 로그 파일을 저장할 임시 디렉터리를 만듭니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir>은 폴더 이름입니다. 아래 예제에서는 /var/opt/mssql/TempDir이라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    SQL Server 데이터와 로그 파일을 임시 디렉터리에 복사합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir>은 이전 단계의 폴더 이름입니다.
    
   *    파일이 디렉터리에 있는지 확인합니다.

    ```bash
    ls \<TempDir>
    ```
    \<TempDir>은 d단계의 폴더 이름입니다.

   *    기존 SQL Server 데이터 디렉터리에서 파일을 삭제합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    파일이 삭제되었는지 확인합니다. 아래 그림은 전체 시퀀스 c~h의 예제를 보여 줍니다.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    `exit`를 입력하여 다시 루트 사용자로 전환합니다.

   *    SQL Server 데이터 폴더에 iSCSI 논리 볼륨을 탑재합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName>은 볼륨 그룹 이름이고, \<LogicalVolumeName>은 생성된 논리 볼륨 이름입니다. 다음 예제 구문은 이전 명령의 볼륨 그룹 및 논리 볼륨과 일치 합니다.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    탑재의 소유자를 mssql로 변경합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    탑재 그룹의 소유권을 mssql로 변경합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    mssql 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    su mssql
    ``` 

   *    임시 디렉터리 /var/opt/mssql/data에서 파일을 복사합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    파일이 있는지 확인합니다.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    `exit`를 입력하여 mssql을 종료합니다.
    
   *    `exit`를 입력하여 루트를 종료합니다.

   *    SQL Server를 시작합니다. 모든 항목이 올바르게 복사되고 보안이 올바르게 적용된 경우 SQL Server가 시작됨으로 표시되어야 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    SQL Server를 중지하고 종료되었는지 확인합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. 시스템 데이터베이스가 아닌 사용자 데이터베이스 또는 백업과 같은 항목의 경우 다음 단계를 수행합니다. 기본 위치를 사용하는 경우에만 14단계로 건너뜁니다.

   *    슈퍼 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    sudo -i
    ```

   *    SQL Server에서 사용할 폴더를 만듭니다. 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName>은 폴더 이름입니다. 올바른 위치에 없으면 폴더의 전체 경로를 지정해야 합니다. 아래 예제에서는 /var/opt/mssql/userdata라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    이전 단계에서 만든 폴더에 iSCSI 논리 볼륨을 탑재합니다. 성공하는 경우 승인이 수신되지 않습니다.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName>은 볼륨 그룹 이름이고, \<LogicalVolumeName>은 생성된 논리 볼륨 이름이고, \<FolderName>은 폴더 이름입니다. 예제 구문은 다음과 같습니다.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    생성된 폴더의 소유권을 mssql로 변경합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    chown mssql <FolderName>
    ```

    \<FolderName>은 생성된 폴더 이름입니다. 아래에 예가 나와 있습니다.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    생성된 폴더 그룹을 mssql로 변경합니다. 성공하는 경우 승인이 수신되지 않습니다.

    ```bash
    chown mssql <FolderName>
    ```

    \<FolderName>은 생성된 폴더 이름입니다. 아래에 예가 나와 있습니다.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    `exit`를 입력하여 슈퍼 사용자를 종료합니다.

   *    테스트하려면 해당 폴더에 데이터베이스를 만듭니다. 아래 표시된 예제에서는 sqlcmd를 사용하여 데이터베이스를 만들고 컨텍스트를 해당 데이터베이스로 전환한 다음, 파일이 OS 수준에 있는지 확인하고 임시 위치를 삭제합니다. SSMS를 사용할 수 있습니다.
  
    ![50-ExampleCreateSSMS][9]

   *    공유를 분리합니다. 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName>은 볼륨 그룹 이름이고, \<LogicalVolumeName>은 생성된 논리 볼륨 이름이고, \<FolderName>은 폴더 이름입니다. 예제 구문은 다음과 같습니다.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Pacemaker만 볼륨 그룹을 활성화할 수 있도록 서버를 구성합니다.

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. 서버에서 볼륨 그룹 목록을 생성합니다. iSCSI 디스크가 아닌 나열된 항목은 OS 디스크의 경우와 같이 시스템에서 사용됩니다.

    ```bash
    sudo vgs
    ```

16. /etc/lvm/lvm.conf 파일의 활성화 구성 섹션을 수정합니다. 다음 줄을 구성합니다.

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker>는 FCI에서 사용되지 않을 20단계 출력의 볼륨 그룹 목록입니다. 각 항목을 따옴표로 묶고 쉼표로 구분합니다. 아래에 예가 나와 있습니다.

    ![55-ListOfVGs][11]
 
 
17. Linux가 시작되면 파일 시스템이 탑재됩니다. Pacemaker만 iSCSI 디스크를 탑재할 수 있도록 하려면 루트 파일 시스템 이미지를 다시 빌드합니다. 

    다음 명령을 실행합니다. 완료하는 데 잠시 시간이 걸릴 수 있습니다. 성공하면 메시지가 다시 표시되지 않습니다.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 서버를 다시 부팅합니다.

19. FCI에 참여할 다른 서버에서 1~6단계를 수행합니다. 이렇게 하면 iSCSI 대상이 SQL Server에 제공됩니다. 
 
20. 서버에서 볼륨 그룹 목록을 생성합니다. 이전에 만든 볼륨 그룹을 표시해야 합니다. 

    ```bash
    sudo vgs
    ``` 
23. SQL Server를 시작하고 이 서버에서 시작할 수 있는지 확인합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. SQL Server를 중지하고 종료되었는지 확인합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. FCI에 참여할 다른 서버에서 1~6단계를 반복합니다.

이제 FCI를 구성할 준비가 되었습니다.

|배포 |항목 
|----- |-----
|**HA 추가 기능이 포함된 Red Hat Enterprise Linux** |[구성](sql-server-linux-shared-disk-cluster-configure.md)<br/>[운영](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**HA 추가 기능이 포함된 SUSE Linux Enterprise Server** |[구성](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>다음 단계

[장애 조치(failover) 클러스터 인스턴스 구성 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
