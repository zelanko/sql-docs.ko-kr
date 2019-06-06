---
title: 장애 조치 클러스터 인스턴스 저장소 iSCSI-Linux의 SQL Server 구성 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 9a64460b2d04f1d6957a181657af7255d64cc829
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705070"
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>장애 조치 클러스터 인스턴스-iSCSI-Linux의 SQL Server 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 장애 조치 클러스터 인스턴스 (FCI)에 대 한 iSCSI 저장소를 구성 하는 방법에 설명 합니다. 

## <a name="configure-iscsi"></a>ISCSI를 구성 합니다. 
iSCSI 서버를 대상으로 알려진 서버에서 디스크를 제공 합니다. 네트워킹을 사용 합니다. ISCSI 대상에 연결 하는 서버는 iSCSI 초기자 구성 되어 있는지 필요 합니다. 대상 디스크에 액세스할 수 있어야 하는 초기자만 작업을 수행할 수 있도록 명시적 권한은 제공 됩니다. 항상 사용 가능 하 고 신뢰할 수 있는 자체 대상이 있어야 합니다.

### <a name="important-iscsi-target-information"></a>중요 한 iSCSI 대상 정보
이 섹션에서는 사용 하려는 원본 유형의 관련이 있기 때문에 iSCSI 대상을 구성 하는 방법을 설명 하지, 하는 동안 클러스터 노드에서 사용할 디스크에 대 한 보안 구성 되어 있는지 확인 합니다.  

Linux 기반 iSCSI 대상을 사용 하는 경우 대상 FCI 노드에서 구성할 수 없습니다. 성능 및 가용성에 대 한 iSCSI 네트워크에서 원본 서버와 클라이언트 서버 모두에서 일반 네트워크 트래픽을 사용 하는 구분 되어야 합니다. Iscsi 사용 네트워크는 빨라야 합니다. 해당 네트워크 일부 프로세서 대역폭 소비를 일반 서버를 사용 하는 경우 적절 하 게 계획 해야 합니다.
되도록 가장 중요 한 점은 FCI에 참여 하는 서버에만 액세스할 수 있도록 만든 디스크를 적절 한 권한이 할당 된 되는 대상에서 완료 합니다. Linuxnodes1 만들어지면 이름이 고 NewFCIDisk1.vhdx에 나타나도록 노드의 IP 주소를 할당 하는 예제의 경우 Microsoft iSCSI 대상의 예는 다음과 같습니다.

![초기자][1]

### <a name="instructions"></a>Instructions

이 섹션에서는 FCI에 대 한 노드로 사용할 서버에서 iSCSI 초기자를 구성 하는 방법을 설명 합니다. Ubuntu 및 RHEL 지침 작동 해야 합니다.

지원 되는 배포에 대 한 iSCSI 초기자에 대 한 자세한 내용은 다음 링크를 참조 하세요.
- [Red Hat](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](https://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  FCI 구성에 참여 하는 서버 중 하나를 선택 합니다. 어떤 것은 중요 하지 않습니다. iSCSI 해야 전용 네트워크에서 인식 하 고 해당 네트워크를 사용 하는 iSCSI를 구성 하므로 합니다. 실행할 `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new` 여기서 `<iSCSIIfaceName>` 네트워크에 대 한 고유 또는 친숙 한 이름입니다. 다음 예제에서는 `iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  편집 `/var/lib/iscsi/ifaces/iSCSIIfaceName`합니다. 다음 값을 완전히 작성 되어 있는지 확인 합니다.

    - OS에서 볼 수 있듯이 iface.net_ifacename 네트워크 카드의 이름을입니다.
    - iface.hwaddress는 MAC 주소 아래에이 인터페이스에 대해 생성 될 고유한 이름입니다.
    - iface.ipaddress
    - iface.subnet_Mask 

    다음 예제를 참조하십시오.

    ![iSCSITargetSettings][2]

3.  ISCSI 대상을 찾습니다.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > 네트워크에 대해 고유한/친숙 한 이름인 \<TargetIPAddress >는 iSCSI 대상의 IP 주소 및 \<TargetPort > iSCSI 대상의 포트입니다. 

    ![iSCSITargetResults][3]

 
4.  대상에 로그인

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName >은 네트워크에 대 한 고유/친숙 한 이름 및 \<TargetIPAddress >는 iSCSI 대상의 IP 주소입니다.

    ![iSCSITargetLogin][4]

5.  ISCSI 대상에 연결 되어 있는지 확인 합니다.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  ISCSI 연결 디스크 확인

    ```bash
    sudo grep "Attached SCSI" /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  ISCSI 디스크에 실제 볼륨을 만듭니다.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<장치 이름 >은 이전 단계에서 장치의 이름입니다. 

 
8.  ISCSI 디스크에 볼륨 그룹을 만듭니다. 단일 볼륨 그룹에 할당 된 디스크는 풀 또는 컬렉션으로 표시 됩니다. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > 볼륨 그룹의 이름 및 \<devicename > 6 단계에서에서 장치의 이름입니다. 
 
9.  만들고 디스크에 대 한 논리 볼륨을 확인 합니다.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<크기 >을 만들려면 볼륨의 크기가 G (기가바이트), T (테라바이트) 등을 사용 하 여 지정할 수 있습니다\<LogicalVolumeName > 논리 볼륨에 대 한 이름 및 \<VolumeGroupName >에서 볼륨 그룹의 이름인는 이전 단계입니다. 

    아래 예제에서는 25GB 볼륨을 만듭니다.
 
    ![Create25GBVol][10]

10. 실행 `sudo lvs` 만들어진 LVM을 확인 합니다.
 
11. 지원 되는 파일 시스템을 사용 하 여 논리 볼륨을 포맷 합니다. EXT4, 다음 예제를 사용 합니다.

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > 이전 단계에서 볼륨 그룹의 이름입니다. \<LogicalVolumeName > 이전 단계에서 논리 볼륨의 이름입니다.  

12. 시스템 데이터베이스 또는 기본 데이터 위치에 저장 된 모든 것에 대해 다음이 단계를 수행 합니다. 그렇지 않을 경우 13 단계로 건너뜁니다.

   *    SQL Server에서 작업 하는 서버에서 중지 되었는지 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Superuser를 완벽 하 게 전환 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```

   *    Mssql 사용자 전환 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   *    SQL Server 데이터를 저장 하 고 로그 파일을 임시 디렉터리를 만듭니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 폴더의 이름입니다. 아래 예제에서는 /var/opt/mssql/TempDir 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    SQL Server 데이터 및 로그 파일을 임시 디렉터리에 복사 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 이전 단계에서 폴더의 이름입니다.
    
   *    파일 디렉터리 인지 확인 합니다.

    ```bash
    ls \<TempDir>
    ```
    \<TempDir > d 단계에 있는 폴더의 이름입니다.

   *    기존 SQL Server 데이터 디렉터리에서 파일을 삭제 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   *    파일이 삭제 되었는지 확인 합니다. 아래 그림에는 c h ~에서 전체 시퀀스의 예가 나와 있습니다.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45-CopyMove][8]
 
   *    형식 `exit` 루트 사용자로 다시 전환 합니다.

   *    SQL Server 데이터 폴더에 iSCSI 논리 볼륨을 탑재 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > 볼륨 그룹의 이름 및 \<LogicalVolumeName > 만든 논리 볼륨의 이름입니다. 다음 예에서는 구문을 볼륨 그룹 및 이전 명령에서 논리 볼륨을 찾습니다.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Mssql에 탑재의 소유자를 변경 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    Mssql에 탑재 그룹의 소유권을 변경 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    Mssql 사용자로 전환 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    su mssql
    ``` 

   *    임시 디렉터리 /var/opt/mssql/data에서 파일을 복사 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    파일 위치에 있는지 확인 합니다.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    입력 `exit` mssql 되지 않습니다.
    
   *    입력 `exit` 루트 되지 않습니다.

   *    SQL Server를 시작 합니다. 모든 항목이 올바르게 복사 되었는지 하 고 적용 하는 보안 올바르게 SQL Server 해야 표시 시작 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    SQL Server를 중지 하 고 종료 하는 것이 것을 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. 사용자 데이터베이스 백업 등의 시스템 데이터베이스 이외의 항목에 대 한 다음이 단계를 수행 합니다. 기본 위치를 사용 하는 경우만 14 단계를 건너뜁니다.

   *    Superuser를 스위치입니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```

   *    SQL Server에서 사용 될 폴더를 만듭니다. 

    ```bash
    mkdir <FolderName>
    ```

    \<폴더 이름 > 폴더의 이름입니다. 폴더의 전체 경로 지정 해야 합니다. 올바른 위치에 없는 경우. 아래 예제에서는 /var/opt/mssql/userdata 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    이전 단계에서 만든 폴더에 iSCSI 논리 볼륨을 탑재 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 볼륨 그룹의 이름인 \<LogicalVolumeName >은 생성 된 논리 볼륨의 이름 및 \<FolderName > 폴더의 이름입니다. 예제 구문은 다음과 같습니다.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    Mssql에 만든 폴더의 소유권을 변경 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    chown mssql <FolderName>
    ```

    \<폴더 이름 > 만든 폴더의 이름입니다. 예제는 다음과 같습니다.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    Mssql에 만든 폴더의 그룹을 변경 합니다. 성공 하는 경우에 모든 승인을 받지 못합니다.

    ```bash
    chown mssql <FolderName>
    ```

    \<폴더 이름 > 만든 폴더의 이름입니다. 예제는 다음과 같습니다.

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    형식 `exit` superuser를 더 이상 되도록 합니다.

   *    를 테스트 하려면 해당 폴더에 데이터베이스를 만듭니다. 아래 예제에서는 sqlcmd를 사용 하 여 데이터베이스 만들기, 컨텍스트 전환, OS 수준에 있는 파일과 임시 위치를 삭제 한 다음 확인 합니다. SSMS를 사용할 수 있습니다.
  
    ![50-ExampleCreateSSMS][9]

   *    공유 마운트 해제 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > 볼륨 그룹의 이름인 \<LogicalVolumeName >은 생성 된 논리 볼륨의 이름 및 \<FolderName > 폴더의 이름입니다. 예제 구문은 다음과 같습니다.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. 유일한 Pacemaker 해당 볼륨 그룹을 활성화할 수 있도록 서버를 구성 합니다.

    ```bash
    sudo lvmconf --enable-halvm --services -startstopservices
    ```
 
15. 서버에서 볼륨 그룹의 목록을 생성 합니다. OS 디스크와 같은 시스템에 의해 사용 됩니다 나열 없는 모든 iSCSI 디스크.

    ```bash
    sudo vgs
    ```

16. 파일 /etc/lvm/lvm.conf의 활성화 구성 섹션을 수정 합니다. 다음 줄을 구성 합니다.

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker >는 FCI가 사용 되지 것입니다 하는 단계 20의 출력에서 볼륨 그룹의 목록입니다. 쉼표로 따옴표에 별도 각각을 배치 합니다. 예제는 다음과 같습니다.

    ![55-ListOfVGs][11]
 
 
17. Linux 시작 되 면 파일 시스템이 마운트됩니다. Pacemaker만 iSCSI 디스크를 탑재할 수 있도록 루트 파일 시스템 이미지를 다시 작성 합니다. 

    다음 명령을 완료 하려면 몇 분 정도 걸릴 수 있습니다. 메시지가 표시 됩니다 없는 다시 성공 합니다.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. 서버를 다시 부팅 합니다.

19. FCI는 참여 하는 다른 서버에서 1-6 단계를 수행 합니다. ISCSI 대상을 SQL Server에 나타납니다. 
 
20. 서버에서 볼륨 그룹의 목록을 생성 합니다. 앞에서 만든 볼륨 그룹을 표시 됩니다. 

    ```bash
    sudo vgs
    ``` 
23. SQL Server를 시작 하 고이 서버에서 시작을 확인 합니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. SQL Server를 중지 하 고 종료 될 때를 확인 합니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. FCI에 참여할 모든 다른 서버에서 1-6 단계를 반복 합니다.

이제 FCI를 구성할 준비가 되었습니다.

|배포 |항목 
|----- |-----
|**HA 추가 기능을 사용 하 여 Red Hat Enterprise Linux** |[구성](sql-server-linux-shared-disk-cluster-configure.md)<br/>[운영](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**HA 추가 기능을 사용 하 여 SUSE Linux Enterprise Server** |[구성](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>다음 단계

[장애 조치 클러스터 인스턴스-Linux의 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure.md)

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
