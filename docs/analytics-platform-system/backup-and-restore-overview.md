---
title: 백업 및 복원-병렬 데이터 웨어하우스 | Microsoft Docs
description: 데이터 백업 및 복원 작동 병렬 데이터 웨어하우스 (PDW)에 대 한 방법을 설명 합니다. 백업 및 복원 작업은 재해 복구에 사용 됩니다. 백업 및 복원 다른 어플라이언스에 하나의 기기에서 데이터베이스를 복사 하려면 사용할 수 있습니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 118b9ced12e01ac6655d85969bb61717f2b31e0b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544815"
---
# <a name="backup-and-restore"></a>백업 및 복원
데이터 백업 및 복원 작동 병렬 데이터 웨어하우스 (PDW)에 대 한 방법을 설명 합니다. 백업 및 복원 작업은 재해 복구에 사용 됩니다. 백업 및 복원 다른 어플라이언스에 하나의 기기에서 데이터베이스를 복사 하려면 사용할 수 있습니다.  
    
## <a name="BackupRestoreBasics"></a>백업 및 복원 기본 사항  
PDW *데이터베이스 백업* 기기를 원본 데이터베이스를 복원 하려면 사용할 수 있는 형식으로 저장 하는 어플라이언스 데이터베이스의 복사본입니다.  
  
PDW 데이터베이스 백업을 사용 하 여 만들어집니다는 [백업 데이터베이스](../t-sql/statements/backup-database-parallel-data-warehouse.md) t-sql 문을 사용 하도록 포맷는 [데이터베이스 복원](../t-sql/statements/restore-database-parallel-data-warehouse.md) 문과 아니므로 사용할 수 있는 다른 용도로 합니다. 만 백업이 동일한 번호 또는 계산 노드 수를 더 기기에 복원할 수 있습니다.  
  
<!-- MISSING LINKS

The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  

-->
  
PDW는 어플라이언스 데이터베이스 백업 및 복원에 SQL Server 백업 기술을 사용 합니다. SQL Server 백업 옵션은 백업 압축을 사용 하도록 미리 구성 합니다. 압축, 체크섬, 블록 크기 및 버퍼 개수 등의 백업 옵션을 설정할 수 없습니다.  
  
데이터베이스 백업은 하나 이상의 백업 하는 서버에 고유한 고객 네트워크에 저장 됩니다.  PDW는 사용자 데이터베이스 백업을 동시에 계산 노드에서 직접 단일 백업 서버로 쓰고는 계산 노드 백업 서버에서 직접 동시에 사용자 데이터베이스 백업을 복원 합니다.  
  
백업은은 Windows 파일 시스템에 백업 서버에 파일 집합으로 저장 됩니다. PDW 데이터베이스 백업은 PDW에만 복원할 수 있습니다. 그러나 표준 Windows 파일 백업 프로세스를 사용 하 여 데이터베이스 백업을 백업 서버에서 다른 위치에 보관할 수 있습니다. 백업 서버에 대 한 자세한 내용은 참조 [Acquire 백업 서버를 구성 하 고](acquire-and-configure-backup-server.md)합니다.  
  
## <a name="BackupTypes"></a>데이터베이스 백업 유형  
백업이 필요한 데이터의 두 가지: 사용자 데이터베이스와 시스템 데이터베이스 (예: master 데이터베이스). PDW는 트랜잭션 로그를 백업 하지 않습니다.  
  
전체 데이터베이스 백업에 전체 PDW 데이터베이스의 백업이입니다. 기본 백업 형식입니다. 데이터베이스 사용자 및 데이터베이스 역할에 사용자 데이터베이스의 전체 백업에 포함 되어 있습니다. 백업 마스터의 로그인이 포함 됩니다.  
  
차등 백업은 마지막 전체 백업 이후 모든 변경 내용을 포함합니다. 차등 백업은 일반적으로 전체 백업보다 시간이 적게 들며 더 자주 수행할 수 있습니다. 각 차등을 여러 차등 백업 전체를 같은 백업을 기반으로 이전 차등에 모든 변경 내용을 포함 합니다.  
  
예를 들어 매주 전체 백업 및 차등 백업은 매일 만들 수 있습니다. 사용자 데이터베이스, 전체 백업 및 마지막 복원 하려면 차등 (있는 경우)를 복원 해야 합니다.  
  
사용자 데이터베이스에 대 한 차등 백업은 지원 됩니다. Master의 백업 항상 전체 백업이입니다.  
  
전체 기기를 백업 하려면 모든 사용자 데이터베이스의 백업 및 master 데이터베이스의 백업을 수행 해야 합니다.  
  
## <a name="BackupProc"></a>데이터베이스 백업 프로세스  
다음 다이어그램은 데이터베이스를 백업 하는 동안 데이터 흐름을 보여 줍니다.  
  
![PDW 백업 프로세스](media/backup-process.png "PDW 백업 프로세스")  
  
백업 프로세스는 다음과 같습니다.  
  
1.  사용자가 하는 제어 노드에 BACKUP DATABASE tsql 문을 전송 합니다.  
  
    -   백업이 전체 또는 차등 백업이입니다.  
  
2.  사용자 데이터베이스에 대 한 제어 노드 (MPP 엔진) 병렬 데이터베이스 백업을 수행 하는 분산된 쿼리 계획을 만듭니다.  
  
3.  각 노드는 SQL Server 백업 기능을 사용 하 여 백업 서버에 백업 파일의 백업 복사본에 관여 합니다.  
  
    -   각 노드의 백업 서버에 복사본 한 백업 파일에 관련 되었습니다.  
  
    -   사용자 데이터베이스 백업 (전체 또는 차등) 각 계산 노드 및 데이터베이스 사용자 및 데이터베이스 역할의 백업에 저장 된 데이터베이스의 부분 백업에 포함 됩니다.  
  
4.  어플라이언스에는 InfiniBand 네트워크를 사용 하 여 병렬 백업을 수행 합니다.  
  
    -   PDW 동시에 각 전체 및 차등 백업을 수행합니다. 그러나 여러 데이터베이스 백업이 동시에 실행 되지 않습니다. 각 백업 요청을 완료 하는 데 이전에 제출 된 백업을 기다려야 합니다.  
  
    -   Master 데이터베이스의 백업이 백업 데이터는 제어 노드에에서 합니다. 이 백업 유형은 직렬로 수행 됩니다.  
  
5.  PDW 데이터베이스 백업을 오프 어플라이언스에 있는 디렉터리에 저장 된 파일 그룹입니다. 네트워크 경로 디렉터리 이름으로 디렉터리 이름이 지정 됩니다. 디렉터리는 로컬 경로 수 없습니다 및 어플라이언스에 있을 수 없습니다.  
  
6.  백업이 완료 된 후 원하는 경우 다른 위치에 백업 디렉터리를 복사 하는 Windows 파일 시스템을 사용할 수 있습니다.  
  
    -   백업 된 같거나 더 큰 수의 계산 노드를 가진 PDW 장치에만 복원할 수 있습니다.  
  
    -   복원을 수행 하기 전에 백업 이름을 변경할 수 없습니다. 백업 디렉터리의 이름 백업의 원래 이름의 이름과 일치 해야 합니다. 백업의 원래 이름은 백업 디렉터리 내에 있는 backup.xml 파일에 있습니다. 다른 이름으로 데이터베이스를 복원 하려면 복원 명령에 새 이름을 지정할 수 있습니다. 예를 들면 `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`과 같습니다.  
  
## <a name="RestoreModes"></a>데이터베이스 복원 모드  
전체 데이터베이스 복원이 데이터베이스 백업에 데이터를 사용 하 여 PDW 데이터베이스를 다시 만듭니다. 먼저 전체 백업을 복원 하 고 다음 차등 백업을 하나 필요에 따라 복원으로 데이터베이스 복원 수행 됩니다. 데이터베이스 복원에는 데이터베이스 사용자 및 데이터베이스 역할에 포함 됩니다.  
  
헤더만 복원 하는 데이터베이스에 대 한 헤더 정보를 반환합니다. 어플라이언스로 데이터를 복원 하지 않습니다.  
  
어플라이언스 복원 하는 경우에 전체 어플라이언스의 복원이입니다. 여기에 모든 사용자 데이터베이스 및 master 데이터베이스를 복원 합니다.  
  
## <a name="RestoreProc"></a>복원 프로세스  
다음 다이어그램은 데이터베이스를 복원 하는 동안 데이터 흐름을 보여 줍니다.  
  
![복원 프로세스](media/restore-process.png "복원 프로세스")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>동일한 수의 계산 노드 * * 어플라이언스에 복원  
  
데이터를 복원할 때 어플라이언스에 원본 어플라이언스와 대상 기기에서 계산 노드 수를 검색 합니다. 두 어플라이언스 계산 노드는 동일한 개수의 있으면 복원 프로세스는 다음과 같습니다.  
  
1.  데이터베이스 백업을 복원 해야 하는 비 어플라이언스 백업 서버에서 Windows 파일 공유에 있습니다. 최상의 성능을 위해이 서버는 일반적으로 어플라이언스에 InfiniBand 네트워크에 연결 됩니다.  
  
2.  사용자가을 제출는 [데이터베이스 복원](../t-sql/statements/restore-database-parallel-data-warehouse.md) 하는 제어 노드에 tsql 문입니다.  
  
    -   복원이 전체 복원 또는 헤더 복원 됩니다. 전체 백업을 복원 하 고 차등 백업을 필요에 따라 복원 하는 전체 복원 합니다.  
  
3.  제어 노드에 (MPP 엔진) 병렬 데이터베이스 복원을 수행 하는 분산된 쿼리 계획을 만듭니다.  
  
    -   SQL ServerPDW 동시에 사용자 데이터베이스의 복원을 수행합니다. 그러나 여러 데이터베이스 백업 및 복원 실행 되지 않습니다 동시에. MPP 엔진은 각 복원 문에; 큐에 배치 이전에 제출 된 백업에 대 한 대기 하 고 복원 요청을 완료 해야 합니다.  
  
    -   Master 데이터베이스를 복원 하는 제어 노드에; 데이터 복원 복원이 직렬로 수행 됩니다.  
  
    -   복원 하는 헤더 정보 빠른 작업으로 계산 또는 컨트롤 노드 데이터를 복원 하지 않습니다. 대신,는 제어 노드에 쿼리 출력으로 결과 반환합니다.  
  
4.  백업 파일 복사는 올바른 계산 노드를 병렬로 일반적으로 어플라이언스에 InfiniBand 네트워크를 통해.  
  
5.  각 계산 노드는 사용자 데이터베이스의 해당 부분을 복원합니다. 복원의 하나라도 성공적으로 완료 되지 않으면, 모든 데이터베이스 제거 하 고 복원이 성공적으로 완료 되었습니다.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>계산 노드 수가 많으면 어플라이언스에 복원  
  
계산 노드 수가 많은 어플라이언스로 백업을 복원하면 계산 노드 수에 비례하여 할당된 데이터베이스 크기가 커집니다.  
  
예를 들어 2 노드 기기 (30GB 노드당)에서 6 개 노드 어플라이언스에 60GB 데이터베이스를 복원, SQL Server PDW 6 개 노드 어플라이언스에 180 GB 데이터베이스 (6 노드 30GB 노드당)를 만듭니다. SQL Server PDW 처음 2 노드 소스 구성과 일치 하도록 데이터베이스를 복원 하 고 6 노드 모두에 데이터를 다시 배포 합니다.  
  
재배포 후 각 계산 노드는 더 작은 원본 어플라이언스에서 각 계산 노드에 비해 더 적은 실제 데이터와 더 많은 여유 공간을 포함하게 됩니다. 데이터베이스에 더 많은 데이터를 추가하려면 추가 공간을 사용합니다. 복원 된 데이터베이스 크기가 필요한 것 보다 더 큰 경우 사용할 수 있습니다 [ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md) 데이터베이스 파일 크기를 축소 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|백업 및 복원 태스크|Description|  
|---------------------------|---------------|  
|백업 서버로 서버를 준비 합니다.|[획득 하 고 백업 서버를 구성 합니다. ](acquire-and-configure-backup-server.md)|  
|데이터베이스를 백업 합니다.|[데이터베이스 백업](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|데이터베이스를 복원 합니다.|[데이터베이스 복원](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    
<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
