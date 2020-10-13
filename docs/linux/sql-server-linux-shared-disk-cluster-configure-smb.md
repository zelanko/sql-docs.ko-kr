---
title: SMB 스토리지 FCI 구성 - SQL Server on Linux
description: SQL Server on Linux에 SMB 스토리지를 사용하여 FCI(장애 조치 클러스터 인스턴스)를 구성하는 방법을 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: b57aec5c6abc9bbeb6928c5310a3217957d2d02b
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784899"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>장애 조치(failover) 클러스터 인스턴스 구성 - SMB - SQL Server on Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux에서 FCI(장애 조치(failover) 클러스터 인스턴스)에 SMB 스토리지를 구성하는 방법을 설명합니다. 
 
Windows 이외의 환경에서 SMB는 대체로 CIFS(Common Internet File System) 공유로 불리고 Samba를 통해 구현됩니다. Windows 환경에서는 \\SERVERNAME\SHARENAME과 같은 방법으로 SMB 공유에 액세스합니다. Linux 기반 SQL Server 설치에서는 SMB 공유를 폴더로 탑재해야 합니다.

## <a name="important-source-and-server-information"></a>중요한 원본 및 서버 정보

다음은 성공적인 SMB 사용을 위한 몇 가지 팁과 참고 사항입니다.
- SMB 공유는 Windows, Linux 또는 SMB 3.0 이상을 사용하는 경우 어플라이언스에서도 사용할 수 있습니다. Samba 및 SMB 3.0에 대한 자세한 내용을 보려면 [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0)에서 Samba 구현이 SMB 3.0을 준수하는지 확인합니다.
- SMB 공유는 고가용성이어야 합니다.
- SMB 공유에 보안이 올바르게 설정되어 있어야 합니다. 다음은 /etc/samba/smb.conf의 예입니다. 여기서 SQLData1은 공유의 이름입니다.

![05-smbsource][1]

## <a name="instructions"></a>Instructions

1. FCI 구성에 참여할 서버 중 하나를 선택합니다. 어떤 서버를 선택하든 상관이 없습니다.
   
1. mssql 사용자에 대한 정보를 가져옵니다.
   
   ```bash
    sudo id mssql
   ```
   
   uid, gid 및 그룹을 적어 둡니다. 
   
1. `sudo smbclient -L //NameOrIP/ShareName -U User`을 실행합니다.
   
   \<NameOrIP>는 SMB 공유를 호스트하는 서버의 DNS 이름 또는 IP 주소입니다.
   
   \<ShareName>은 SMB 공유의 이름입니다. 
   
1. 시스템 데이터베이스 또는 기본 데이터 위치에 저장된 항목의 경우 다음 단계를 수행합니다. 그렇지 않으면 5단계로 건너뜁니다. 
   
   1. 작업 중인 서버에서 SQL Server가 중지되었는지 확인합니다.
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 슈퍼 사용자로 완전히 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      sudo -i
      ```
      
   1. mssql 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      su mssql
      ```
      
   1. SQL Server 데이터와 로그 파일을 저장할 임시 디렉터리를 만듭니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir>은 폴더 이름입니다. 다음 예제에서는 /var/opt/mssql/tmp라는 폴더를 만듭니다.
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. SQL Server 데이터와 로그 파일을 임시 디렉터리에 복사합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir>은 이전 단계의 폴더 이름입니다.
      
   1. 파일이 디렉터리에 있는지 확인합니다.
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir>은 d 단계의 폴더 이름입니다.
      
   1. 기존 SQL Server 데이터 디렉터리에서 파일을 삭제합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. 파일이 삭제되었는지 확인합니다. 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. exit를 입력하여 다시 루트 사용자로 전환합니다.
      
   1. SQL Server 데이터 폴더에 SMB 공유를 탑재합니다. 성공하는 경우 승인이 수신되지 않습니다. 이 예제에서는 Windows Server 기반 SMB 3.0 공유에 연결하는 구문을 보여 줍니다.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName>은 SMB 공유가 있는 서버의 이름입니다.
      
      \<ShareName>은 공유의 이름입니다.
      
      \<UserName>은 공유에 액세스할 사용자의 이름입니다.
      
      \<Password>는 사용자의 암호입니다.
      
      \<domain>은 Active Directory의 이름입니다.
      
      \<mssqlUID>는 mssql 사용자의 UID입니다. 
      
      \<mssqlGID>는 mssql 사용자의 GID입니다.
      
   1. 스위치 없이 mount를 실행하여 탑재에 성공했는지 확인합니다.
      
      ```bash
      mount
      ```
      
   1. mssql 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      su mssql
      ```
      
   1. 임시 디렉터리 /var/opt/mssql/data에서 파일을 복사합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. 파일이 있는지 확인합니다.
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. exit를 입력하여 mssql을 종료합니다. 
      
   1. exit를 입력하여 루트를 종료합니다.
   
   1. SQL Server를 시작합니다. 모든 항목이 올바르게 복사되고 보안이 올바르게 적용된 경우 SQL Server가 시작됨으로 표시되어야 합니다.
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 추가로 테스트하려면 데이터베이스를 만들어 사용 권한이 적절한지 확인합니다. 다음 예제에서는 Transact-SQL을 사용합니다. SSMS를 사용할 수도 있습니다.
      
      ![10_testcreatedb][2] 
      
   1. SQL Server를 중지하고 종료되었는지 확인합니다. 다른 디스크를 추가하거나 테스트하려는 경우 해당 디스크가 추가 및 테스트될 때까지 SQL Server를 종료하지 않습니다.
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 작업이 완료된 경우에만 공유를 분리합니다. 완료되지 않은 경우 다른 디스크 테스트/추가를 마친 후에 분리합니다.
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName>은 SMB 호스트의 IP 주소 또는 이름입니다.
      
      \<ShareName>은 공유의 이름입니다.
      
      \<FolderMountedIn>은 SMB가 탑재된 폴더의 이름입니다.
      
5. 시스템 데이터베이스가 아닌 사용자 데이터베이스 또는 백업과 같은 항목의 경우 다음 단계를 수행합니다. 기본 위치를 사용하는 경우에만 14단계로 건너뜁니다.
   
   1. 슈퍼 사용자로 전환합니다. 성공하는 경우 승인이 수신되지 않습니다.
      
      ```bash
      sudo -i
      ```
      
   1. SQL Server에서 사용할 폴더를 만듭니다. 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<FolderName>은 폴더 이름입니다. 올바른 위치에 없으면 폴더의 전체 경로를 지정해야 합니다. 다음 예제에서는 /var/opt/mssql/userdata라는 폴더를 만듭니다.
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. SQL Server 데이터 폴더에 SMB 공유를 탑재합니다. 성공하는 경우 승인이 수신되지 않습니다. 이 예제에서는 Samba 기반 SMB 3.0 공유에 연결하는 구문을 보여 줍니다.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName>은 SMB 공유가 있는 서버의 이름입니다.
      
      \<ShareName>은 공유의 이름입니다.
      
      \<FolderName>은 마지막 단계에서 만든 폴더의 이름입니다.  
      
      \<UserName>은 공유에 액세스할 사용자의 이름입니다.
      
      \<Password>는 사용자의 암호입니다.
      
      \<mssqlUID>는 mssql 사용자의 UID입니다.
      
      \<mssqlGID>는 mssql 사용자의 GID입니다.
      
   1. 스위치 없이 mount를 실행하여 탑재에 성공했는지 확인합니다.
   
   1. exit를 입력하여 슈퍼 사용자를 종료합니다.
   
   1. 테스트하려면 해당 폴더에 데이터베이스를 만듭니다. 다음 예제에서는 sqlcmd를 사용하여 데이터베이스를 만들고 컨텍스트를 해당 데이터베이스로 전환한 다음, 파일이 OS 수준에 있는지 확인하고 임시 위치를 삭제합니다. SSMS를 사용할 수 있습니다.
   
   1. 공유를 분리합니다. 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName>은 SMB 호스트의 IP 주소 또는 이름입니다.
      
      \<ShareName>은 공유의 이름입니다.
      
      \<FolderMountedIn>은 SMB가 탑재된 폴더의 이름입니다.
   
1. 다른 노드에 대해 단계를 반복합니다.

이제 FCI를 구성할 준비가 되었습니다.

## <a name="next-steps"></a>다음 단계

[장애 조치(failover) 클러스터 인스턴스 구성 - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
