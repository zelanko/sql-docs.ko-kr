---
title: SQL Server 빅 데이터 클러스터에 데이터베이스 복원 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 04514fb0184fa28e0ba959f3dd33cb2e1ec945cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48796445"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>SQL Server 빅 데이터 클러스터 마스터 인스턴스에 데이터베이스를 복원 합니다.

기존 SQL Server 데이터베이스의 마스터 인스턴스 상태로, 백업, 복사를 사용 하는 것이 좋습니다에서는 및 접근 방식을 복원 합니다.  이 예제에서 AdventureWorks 데이터베이스를 복원 하는 방법을 보여줍니다 있지만 해야 하는 모든 데이터베이스 백업을 사용할 수 있습니다.  AdventureWorks 백업을 다운로드할 수 있습니다 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=49502)합니다.

먼저 Windows에서 SQL Server 또는 Linux의 데이터베이스 백업을 만드는 일반적인 방법 중 하나를 사용 하 여 기존 SQL Server 데이터베이스를 백업 합니다.

Kubernetes 클러스터의 마스터 인스턴스 pod의 SQL Server 컨테이너에 백업 파일을 복사 합니다.

```bash
kubectl cp <path to .bak file> mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n <name of your cluster>
```

예:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-data-pool-master-0:/tmp/ -c mssql-data-pool-data -n clustertest
```

그런 다음 백업 파일을 pod 컨테이너에 복사 되었는지 확인 합니다.

```bash
kubectl exec -it mssql-data-pool-master-0 -n <name of your cluster> -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
root@mssql-data-pool-master-0:/# exit
```

예:

```bash
kubectl exec -it mssql-data-pool-master-0 -n clustertest -c mssql-data-pool-data -- bin/bash
root@mssql-data-pool-master-0:/# ls /tmp
```

마스터 SQL Server 인스턴스에 데이터베이스 백업을 복원 어.  Windows에서 생성 된 데이터베이스 백업을 복원 하는 경우에 파일의 이름을 가져올 해야 합니다.  마스터 인스턴스에 연결 된 Ops Studio에서이 SQL 스크립트를 실행 합니다.

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

예:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![백업 파일 목록](media/restore-database/database-restore-file-list.png)

이제 데이터베이스를 복원이 같은 스크립트를 사용 하 여 데이터베이스 백업에 따라 필요에 따라 이름/경로 대체 합니다.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

이제 하도록 하려는 경우 중요 데이터베이스에 액세스할 수 데이터 풀 데이터 풀 저장 프로시저를 열고 GitHub 리포지토리에서 이러한 스크립트를 실행 하 여 설치 해야 합니다.

실행 된 **높은 값-db configuration\data_pool_ddl_install 합니다. SQL** 스크립트입니다.

- 지원 가능성 저장 프로시저를 설정 합니다.

실행 된 **높은 값-db configuration\supportability 합니다. SQL** 스크립트입니다.
