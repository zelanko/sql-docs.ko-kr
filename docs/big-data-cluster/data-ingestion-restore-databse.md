---
title: SQL Server 빅 데이터 클러스터에 데이터베이스 복원 | Microsoft Docs
description: 이 아티클에서 SQL Server 빅 데이터 클러스터의 마스터 인스턴스에 데이터베이스를 복원 하는 방법에 설명 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/09/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: e921948cb5dcd0bda52ed9ebcc07c8a2496611ff
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905053"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>SQL Server 빅 데이터 클러스터 마스터 인스턴스에 데이터베이스를 복원 합니다.

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 마스터 인스턴스를 기존 데이터베이스를 복원 하는 방법을 설명 합니다. 백업, 복사, 사용 및 접근 방식을 복원 하는 것이 좋습니다.

## <a name="backup-your-existing-database"></a>기존 데이터베이스를 백업 합니다.

먼저 Windows에서 SQL Server 또는 Linux에서 기존 SQL Server 데이터베이스를 백업 합니다. TRANSACT-SQL 또는 SQL Server Management Studio (SSMS)와 같은 도구를 사용 하 여 표준 백업 기술을 사용 합니다.

이 문서에서는 AdventureWorks 데이터베이스를 복원 하는 방법을 보여 줍니다. 하지만 모든 데이터베이스 백업을 사용할 수 있습니다. 

> [!TIP]
> AdventureWorks 백업을 다운로드할 수 있습니다 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=49502)합니다.

## <a name="copy-the-backup-file"></a>백업 파일 복사

Kubernetes 클러스터의 마스터 인스턴스 pod의 SQL Server 컨테이너에 백업 파일을 복사 합니다.

```bash
kubectl cp <path to .bak file> mssql-master-pool-0:/tmp -c mssql-server -n <name of your cluster>
```

예:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n clustertest
```

그런 다음 백업 파일을 pod 컨테이너에 복사 되었는지 확인 합니다.

```bash
kubectl exec -it mssql-master-pool-0 -n <name of your cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

예:

```bash
kubectl exec -it mssql-master-pool-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>백업 파일 복원

마스터 SQL Server 인스턴스에 데이터베이스 백업을 복원 어.  Windows에서 생성 된 데이터베이스 백업을 복원 하는 경우에 파일의 이름을 가져올 해야 합니다.  Azure 데이터 Studio에서 마스터 인스턴스에 연결 하 고이 SQL 스크립트를 실행 합니다.

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

예:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![백업 파일 목록](media/restore-database/database-restore-file-list.png)

이제 데이터베이스를 복원 합니다. 다음 스크립트는 예제입니다. 데이터베이스 백업에 따라 필요에 따라 이름/경로 대체 합니다.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>데이터 풀 및 HDFS 액세스 구성

이제 액세스 데이터 풀과 HDFS에 SQL Server 마스터 인스턴스에 대해 데이터 풀 및 저장소 풀 저장 프로시저를 실행 합니다. 새로 복원된 된 데이터베이스에 대해 다음 TRANSACT-SQL 스크립트를 실행 합니다.

```sql
USE AdventureWorks2016CTP3
GO 
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
    CREATE EXTERNAL DATA SOURCE SqlDataPool
    WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');

IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
    CREATE EXTERNAL DATA SOURCE SqlStoragePool
    WITH (LOCATION = 'sqlhdfs://service-mssql-controller:8080');
GO
```

> [!NOTE]
> 이전 버전의 SQL Server에서 복원 되는 데이터베이스에 대해서만 이러한 설치 스크립트를 통해 실행 해야 합니다. SQL Server 마스터 인스턴스에 새 데이터베이스를 만들면 데이터 풀 및 저장소 풀 저장 프로시저를 이미 구성 됩니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 다음 개요를 참조 하세요.

- [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)
