---
title: "장애 조치 클러스터 인스턴스 저장소 SMB-Linux에서 SQL Server 구성 | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: c32c0593df6b40cc76ecafaabc0571090f2907fa
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>SMB-Linux에서 SQL Server 장애 조치 클러스터 인스턴스-를 구성 합니다.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 문서는 Linux에서 장애 조치 클러스터 인스턴스 (FCI)에 대 한 SMB 저장소를 구성 하는 방법을 설명 합니다. 
 
비 Windows 환경에서 SMB는 종종으로 파일 시스템 CIFS (Common Internet) 공유 하려면 이라고 하며 Samba 통해 구현 합니다. Windows 환경에서 SMB 공유에 액세스 하는이 작업 방식이으로 수행: \\SERVERNAME\SHARENAME 합니다. Linux 기반 SQL Server 설치의 경우 SMB 공유 폴더로 탑재 되어야 합니다.

## <a name="important-source-and-server-information"></a>원본 및 서버에 대 한 중요 한 정보

다음은 몇 가지 팁과 성공적으로 SMB 사용에 대 한 정보입니다.
- Windows, Linux, 또는 SMB 3.0을 사용 하는 것 처럼 장기 또는 그 이상으로 어플라이언스에 에서도 SMB 공유 될 수 있습니다. Samba 및 SMB 3.0에 대 한 자세한 내용은 참조 하십시오. [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) Samba 구현 SMB 3.0과 호환 되는지 합니다.
- SMB 공유를 항상 사용 가능 해야 합니다.
- 보안을 설정 해야 SMB 공유에 적절 합니다. 다음은 예 /etc/samba/smb.conf에서 SQLData1은 공유의 이름입니다.

![05 smbsource][1]

## <a name="instructions"></a>Instructions

1.  FCI 구성에 참여 하는 서버 중 하나를 선택 합니다. 어떤 것은 중요 하지 않습니다.

2.  Mssql 사용자에 대 한 정보를 가져옵니다.

    ```bash
    sudo id mssql
    ```
    
    Uid, gid 및 그룹 note 합니다. 

3. `sudo smbclient -L //NameOrIP/ShareName -U User`을 실행합니다.

    \<NameOrIP > DNS 이름 또는 SMB 공유를 호스팅하는 서버의 IP 주소입니다.

    \<공유 이름 >은 SMB 공유의 이름입니다. 

4. 시스템 데이터베이스 또는 기본 데이터 위치에 저장 된 내용은 다음이 단계를 수행 합니다. 그렇지 않으면 5 단계로 건너뜁니다. 

   *    SQL Server에서 작업 하는 서버에서 중지 되었는지 확인 합니다.
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    스위치는 superuser를 완벽 하 게 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```

   *    Mssql 사용자 전환 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   *    SQL Server 데이터를 저장 및 로그 파일을 임시 디렉터리를 만듭니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    mkdir <TempDir>
    ```

    <TempDir>폴더의 이름이입니다. 다음 예제에서는 /var/opt/mssql/tmp 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   *    SQL Server 데이터 및 로그 파일을 임시 디렉터리에 복사 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir >의 이전 단계에서 폴더의 이름입니다.
    
   *    파일 디렉터리에 있는지 확인 합니다.

    ```bash
    ls <TempDir>
    ```

    \<TempDir > d 단계에 있는 폴더의 이름입니다.
    
   *    기존 SQL Server 데이터 디렉터리에서 파일을 삭제 합니다. 성공 하는 경우에 승인을 받지 못합니다.
 
    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    파일 삭제를 확인 합니다. 

    ```bash
    ls /var/opt/mssql/data
    ```
 
   *    루트 사용자로 다시 전환 하려면 exit를 입력 합니다.

   *    SQL Server 데이터 폴더에 SMB 공유를 탑재 합니다. 성공 하는 경우에 승인을 받지 못합니다. 이 예제에는 Windows 서버 기반 SMB 3.0 공유에 연결 하기 위한 구문을 보여 줍니다.

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<서버 이름 >은 SMB 공유를 사용 하 여 서버 이름
    
    \<공유 이름 > 공유의 이름

    \<사용자 이름 > 공유에 액세스 하려면 사용자의 이름

    \<암호 > 사용자에 대 한 암호

    \<도메인 >은 Active Directory의 이름

    \<mssqlUID > mssql 사용자 UID은 
 
    \<mssqlGID > mssql 사용자 GID은
 
   *    스위치 없이 탑재를 실행 하 여 탑재 성공 했음을 확인 합니다.

    ```bash
    mount
    ```
 
   *    Mssql 사용자로 전환 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    su mssql
    ```

   *    임시 디렉터리 /var/opt/mssql/data에서 파일을 복사 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssql/data
    ```

   *    파일이 있는지 확인 합니다.

    ```bash
    ls /var/opt/mssql/data
    ```

   *    종료 되지 않고 mssql를 입력 합니다. 

   *    종료 되지 않고 루트를 입력 합니다.

   *    SQL Server를 시작 합니다. 모든 항목이 올바르게 복사 하 고 적용 된 보안 올바르게 SQL Server 해야 표시 시작 될 때입니다.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
 
   *    추가 테스트 하려면 만족 하는 사용 권한을 확인 하려면 데이터베이스를 만듭니다. 다음 예제에서는 TRANSACT-SQL을 사용 하 여 SSMS를 사용할 수 있습니다.

    ![10_testcreatedb][2] 
  
   *    SQL Server를 중지 하 고 종료 되었는지 확인 합니다. 추가 하거나 다른 디스크를 테스트 하려는 경우 종료 하지 마세요 SQL Server 때까지 추가 되 고 테스트 하는 것입니다.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    완료 하는 경우에 공유를 마운트 해제 합니다. 파일이 없으면 추가 디스크를 테스트 하거나 추가 완료 한 후 탑재 해제 합니다.

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
    ```

    \<IPAddressOrServerName >는 IP 주소 또는 SMB 호스트의 이름

    \<공유 이름 > 공유의 이름
    
    \<FolderMountedIn >은 SMB 탑재 된 폴더의 이름

5.  사용자 데이터베이스 또는 백업 등의 시스템 데이터베이스가 아닌 다른 항목에 대 한 다음이 단계를 수행 합니다. 기본 위치를 사용 하 여 경우에 14 단계를 건너뜁니다.
    
   *    전환의 superuser 이어야 합니다. 성공 하는 경우에 승인을 받지 못합니다.

    ```bash
    sudo -i
    ```
    
   *    SQL Server에서 사용 될 폴더를 만듭니다. 

    ```bash
    mkdir <FolderName>
    ```

    \<폴더 이름 > 폴더의 이름입니다. 폴더의 전체 경로를 지정 해야 할 경우 올바른 위치에 없습니다. 다음 예제에서는 /var/opt/mssql/userdata 라는 폴더를 만듭니다.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    SQL Server 데이터 폴더에 SMB 공유를 탑재 합니다. 성공 하는 경우에 승인을 받지 못합니다. 이 예제에는 Samba 기반 SMB 3.0 공유에 연결 하기 위한 구문을 보여 줍니다.

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<서버 이름 >은 SMB 공유를 사용 하 여 서버 이름

    \<공유 이름 > 공유의 이름

    \<폴더 이름 > 마지막 단계에서 만든 폴더의 이름  

    \<사용자 이름 > 공유에 액세스 하려면 사용자의 이름

    \<암호 > 사용자에 대 한 암호

    \<mssqlUID > mssql 사용자 UID은

    \<mssqlGID > mssql 사용자 GID 됩니다.
 
   * 스위치 없이 탑재를 실행 하 여 탑재 성공 했음을 확인 합니다.
 
   * 더 이상 수는 superuser exit를 입력 합니다.

   * 를 테스트 하려면 해당 폴더에 데이터베이스를 만듭니다. Sqlcmd를 사용 하 여 데이터베이스 만들기, 컨텍스트를 전환할 OS 수준에 있는 파일과 임시 위치를 삭제 한 다음 확인는 아래 표시 된 예제입니다. SSMS를 사용할 수 있습니다.
 
   * 공유를 마운트 해제 

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
    ```
    
    \<IPAddressOrServerName >는 IP 주소 또는 SMB 호스트의 이름
 
    \<공유 이름 > 공유의 이름
 
    \<FolderMountedIn > SMB 탑재 된 폴더의 이름입니다.
 
6.  다른 노드에서에서 단계를 반복 합니다.

이제 FCI를 구성할 준비가 되었습니다.

## <a name="next-steps"></a>다음 단계

[장애 조치 클러스터 인스턴스-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 

