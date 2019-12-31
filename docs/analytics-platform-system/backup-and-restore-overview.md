---
title: Backup 및 복원
description: 데이터 백업 및 복원이 PDW (병렬 데이터 웨어하우스)에서 작동 하는 방식을 설명 합니다. 백업 및 복원 작업은 재해 복구에 사용 됩니다. 백업 및 복원을 사용 하 여 한 어플라이언스에서 다른 어플라이언스로 데이터베이스를 복사할 수도 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 01/19/2019
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 75399480879623a39da542c68f036389c645f6ab
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401357"
---
# <a name="backup-and-restore"></a>Backup 및 복원

데이터 백업 및 복원이 PDW (병렬 데이터 웨어하우스)에서 작동 하는 방식을 설명 합니다. 백업 및 복원 작업은 재해 복구에 사용 됩니다. 백업 및 복원을 사용 하 여 한 어플라이언스에서 다른 어플라이언스로 데이터베이스를 복사할 수도 있습니다.  
    
## <a name="BackupRestoreBasics"></a>백업 및 복원 기본 사항

PDW *데이터베이스 백업은* 원본 데이터베이스를 어플라이언스로 복원 하는 데 사용할 수 있도록 형식으로 저장 된 어플라이언스 데이터베이스의 복사본입니다.  
  
PDW 데이터베이스 백업은 [BACKUP database](../t-sql/statements/backup-database-parallel-data-warehouse.md) t-sql 문을 사용 하 여 생성 되 고 [RESTORE database](../t-sql/statements/restore-database-parallel-data-warehouse.md) 문에 사용할 수 있도록 형식이 지정 됩니다. 다른 용도로는 사용할 수 없습니다. 백업은 동일한 수 또는 많은 수의 계산 노드를 포함 하는 어플라이언스로만 복원할 수 있습니다.  
  
<!-- MISSING LINKS
The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  
-->
  
PDW는 SQL Server 백업 기술을 사용 하 여 어플라이언스 데이터베이스를 백업 및 복원 합니다. SQL Server 백업 옵션은 백업 압축을 사용 하도록 미리 구성 되어 있습니다. 압축, 체크섬, 블록 크기 및 버퍼 개수 등의 백업 옵션을 설정할 수 없습니다.  
  
데이터베이스 백업은 사용자의 고객 네트워크에 존재 하는 하나 이상의 백업 서버에 저장 됩니다.  PDW는 사용자 데이터베이스 백업을 계산 노드에서 하나의 백업 서버에 직접 동시에 기록 하 고, 백업 서버에서 계산 노드로 직접 사용자 데이터베이스 백업을 병렬로 복원 합니다.  
  
백업은 Windows 파일 시스템의 파일 집합으로 백업 서버에 저장 됩니다. PDW 데이터베이스 백업은 PDW로만 복원할 수 있습니다. 그러나 표준 Windows 파일 백업 프로세스를 사용 하 여 백업 서버에서 다른 위치로 데이터베이스 백업을 보관할 수 있습니다. 백업 서버에 대 한 자세한 내용은 [백업 서버 가져오기 및 구성](acquire-and-configure-backup-server.md)을 참조 하세요.  
  
## <a name="BackupTypes"></a>데이터베이스 백업 유형

백업 해야 하는 데이터에는 사용자 데이터베이스와 시스템 데이터베이스 (예: master 데이터베이스)의 두 가지 유형이 있습니다. PDW는 트랜잭션 로그를 백업 하지 않습니다.  
  
전체 데이터베이스 백업은 전체 PDW 데이터베이스의 백업입니다. 이는 기본 백업 유형입니다. 사용자 데이터베이스의 전체 백업에는 데이터베이스 사용자 및 데이터베이스 역할이 포함 됩니다. Master 백업에는 로그인이 포함 됩니다.  
  
차등 백업은 마지막 전체 백업 이후의 모든 변경 내용을 포함 합니다. 차등 백업은 일반적으로 전체 백업보다 시간이 적게 들며 더 자주 수행할 수 있습니다. 여러 차등 백업이 동일한 전체 백업을 기반으로 하는 경우 각 차등은 이전 차등의 모든 변경 내용을 포함 합니다.  
  
예를 들어 매주 전체 백업을 만들고 매일 차등 백업을 만들 수 있습니다. 사용자 데이터베이스를 복원 하려면 전체 백업과 마지막 차등 (있는 경우)을 복원 해야 합니다.  
  
차등 백업은 사용자 데이터베이스에 대해서만 지원 됩니다. Master 백업은 항상 전체 백업입니다.  
  
전체 어플라이언스를 백업 하려면 모든 사용자 데이터베이스의 백업과 master 데이터베이스의 백업을 수행 해야 합니다.  
  
## <a name="BackupProc"></a>데이터베이스 백업 프로세스

다음 다이어그램에서는 데이터베이스 백업 중의 데이터 흐름을 보여 줍니다.  
  
![PDW 백업 프로세스](media/backup-process.png "PDW 백업 프로세스")  
  
백업 프로세스는 다음과 같이 작동 합니다.  
  
1.  사용자가 Control 노드에 BACKUP DATABASE tsql 문을 전송 합니다.  
  
    -   백업은 전체 또는 차등 백업입니다.  
  
2.  사용자 데이터베이스의 경우 제어 노드 (MPP 엔진)는 병렬 데이터베이스 백업을 수행 하는 분산 쿼리 계획을 만듭니다.  
  
3.  백업과 관련 된 각 노드는 SQL Server 백업 기능을 사용 하 여 백업 파일을 백업 서버에 복사 합니다.  
  
    -   관련 된 각 노드는 백업 서버에 백업 파일 하나를 복사 합니다.  
  
    -   사용자 데이터베이스 백업 (전체 또는 차등)에는 각 계산 노드에 저장 된 데이터베이스의 부분과 데이터베이스 사용자 및 데이터베이스 역할의 백업이 포함 됩니다.  
  
4.  어플라이언스는 InfiniBand 네트워크를 사용 하 여 백업을 병렬로 수행 합니다.  
  
    -   PDW는 각각의 전체 백업과 차등 백업을 병렬로 수행 합니다. 그러나 여러 데이터베이스 백업은 동시에 실행 되지 않습니다. 각 백업 요청은 이전에 제출 된 백업이 완료 될 때까지 기다려야 합니다.  
  
    -   Master 데이터베이스의 백업은 Control 노드의 데이터만 백업 합니다. 이 백업 유형은 직렬로 수행 됩니다.  
  
5.  PDW 데이터베이스 백업은 어플라이언스에 있는 디렉터리에 저장 된 파일의 그룹입니다. 디렉터리 이름은 네트워크 경로 및 디렉터리 이름으로 지정 됩니다. 디렉터리는 로컬 경로일 수 없으며 어플라이언스에 있을 수 없습니다.  
  
6.  백업이 완료 된 후에는 Windows 파일 시스템을 사용 하 여 원하는 경우 백업 디렉터리를 다른 위치로 복사할 수 있습니다.  
  
    -   백업은 동일한 수 이상의 계산 노드를 포함 하는 PDW 어플라이언스로만 복원할 수 있습니다.  
  
    -   복원을 수행 하기 전에 백업 이름을 변경할 수 없습니다. 백업 디렉터리의 이름은 백업의 원래 이름 이름과 일치 해야 합니다. 백업의 원래 이름은 백업 디렉터리 내의 백업 .xml 파일에 있습니다. 데이터베이스를 다른 이름으로 복원 하려면 restore 명령에 새 이름을 지정할 수 있습니다. 예: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`  
  
## <a name="RestoreModes"></a>데이터베이스 복원 모드

전체 데이터베이스 복원은 데이터베이스 백업의 데이터를 사용 하 여 PDW 데이터베이스를 다시 만듭니다. 데이터베이스 복원은 먼저 전체 백업을 복원한 다음 필요에 따라 하나의 차등 백업을 복원 하는 방법으로 수행 됩니다. 데이터베이스 복원에는 데이터베이스 사용자 및 데이터베이스 역할이 포함 됩니다.  
  
머리글만 복원은 데이터베이스에 대 한 헤더 정보를 반환 합니다. 어플라이언스로 데이터를 복원 하지 않습니다.  
  
어플라이언스 복원은 전체 어플라이언스의 복원입니다. 여기에는 모든 사용자 데이터베이스 및 master 데이터베이스를 복원 하는 작업이 포함 됩니다.  
  
## <a name="RestoreProc"></a>복원 프로세스

다음 다이어그램에서는 데이터베이스를 복원 하는 동안 발생 하는 데이터 흐름을 보여 줍니다.  
  
![복원 프로세스](media/restore-process.png "복원 프로세스")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>동일한 수의 계산 노드를 사용 하 여 어플라이언스 복원 * *  
  
데이터를 복원할 때 어플라이언스는 원본 어플라이언스 및 대상 어플라이언스에서 계산 노드 수를 검색 합니다. 두 어플라이언스의 계산 노드 수가 같으면 복원 프로세스는 다음과 같이 작동 합니다.  
  
1.  복원할 데이터베이스 백업은 비 어플라이언스 백업 서버의 Windows 파일 공유에서 사용할 수 있습니다. 최상의 성능을 위해이 서버는 어플라이언스 InfiniBand 네트워크에 연결 됩니다.  
  
2.  사용자가 Control 노드에 [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) tsql 문을 전송 합니다.  
  
    -   복원은 전체 복원 또는 헤더 복원 중 하나입니다. 전체 복원은 전체 백업을 복원한 다음 필요에 따라 차등 백업을 복원 합니다.  
  
3.  제어 노드 (MPP 엔진)는 병렬 데이터베이스 복원을 수행 하는 분산 쿼리 계획을 만듭니다.  
  
    -   SQL ServerPDW는 사용자 데이터베이스의 복원을 병렬로 수행 합니다. 그러나 여러 데이터베이스 백업 및 복원은 동시에 실행 되지 않습니다. MPP 엔진은 각 restore 문을 큐에 넣습니다. 이전에 제출 된 백업 및 복원 요청이 완료 될 때까지 기다려야 합니다.  
  
    -   Master 데이터베이스를 복원 하면 데이터는 컨트롤 노드로 복원 됩니다. 복원은 순차적으로 수행 됩니다.  
  
    -   헤더 정보 복원은 빠른 작업 이며 계산 또는 제어 노드로 데이터를 복원 하지 않습니다. 대신, 컨트롤 노드는 결과를 쿼리 출력으로 반환 합니다.  
  
4.  백업 파일은 일반적으로 어플라이언스 InfiniBand 네트워크를 통해 올바른 계산 노드로 복사 됩니다.  
  
5.  각 계산 노드는 사용자 데이터베이스의 해당 부분을 복원 합니다. 복원이 성공적으로 완료 되지 않으면 모든 데이터베이스가 제거 되 고 복원이 성공적으로 완료 되지 않습니다.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>컴퓨팅 노드 수가 더 많은 어플라이언스에 복원  
  
컴퓨팅 노드 수가 많은 어플라이언스로 백업을 복원하면 컴퓨팅 노드 수에 비례하여 할당된 데이터베이스 크기가 커집니다.  
  
예를 들어 2 노드 어플라이언스 (노드당 30gb)에서 60 GB 데이터베이스를 6 개 노드 어플라이언스로 복원 하는 경우 SQL Server PDW은 6 개 노드 어플라이언스에서 180 GB 데이터베이스 (노드당 30gb가 있는 6 개 노드)를 만듭니다. SQL Server PDW는 처음에 데이터베이스를 2 개 노드로 복원 하 여 원본 구성과 일치 하 게 한 다음 데이터를 6 개 노드 모두에 다시 배분 합니다.  
  
재배포 후 각 계산 노드는 작은 원본 어플라이언스의 각 계산 노드 보다 적은 실제 데이터와 더 많은 여유 공간을 포함 합니다. 데이터베이스에 더 많은 데이터를 추가하려면 추가 공간을 사용합니다. 복원 된 데이터베이스 크기가 필요한 크기 보다 큰 경우 [ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 를 사용 하 여 데이터베이스 파일 크기를 축소할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|백업 및 복원 태스크|설명|  
|---------------------------|---------------|  
|서버를 백업 서버로 준비 합니다.|[백업 서버 획득 및 구성](acquire-and-configure-backup-server.md)|  
|데이터베이스를 백업 합니다.|[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|데이터베이스를 복원 합니다.|[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    

<!-- MISSING LINKS

|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  

-->
