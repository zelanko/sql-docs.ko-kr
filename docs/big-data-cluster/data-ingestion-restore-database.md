---
title: 데이터베이스 복원
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 마스터 인스턴스에 데이터베이스를 복원하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bad1a62752dd75e181d30c28485e1c9b707aa888
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69652235"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>SQL Server 빅 데이터 클러스터 마스터 인스턴스에 데이터베이스 복원

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 마스터 인스턴스로 기존 데이터베이스를 복원하는 방법을 설명합니다. 백업, 복사 및 복원 방법을 사용하는 것이 좋습니다.

## <a name="backup-your-existing-database"></a>기존 데이터베이스 백업

먼저 Windows 또는 Linux의 SQL Server에서 기존 SQL Server 데이터베이스를 백업합니다. SSMS(SQL Server Management Studio)와 같은 도구나 Transact-SQL과 함께 표준 백업 방법을 사용합니다.

이 문서에서는 AdventureWorks 데이터베이스를 복원하는 방법을 보여 주지만, 모든 데이터베이스 백업을 사용할 수 있습니다. 

> [!TIP]
> AdventureWorks 백업은 [여기](https://www.microsoft.com/download/details.aspx?id=49502)에서 다운로드할 수 있습니다.

## <a name="copy-the-backup-file"></a>백업 파일 복사

Kubernetes 클러스터의 마스터 인스턴스 Pod에 있는 SQL Server 컨테이너에 백업 파일을 복사합니다.

```bash
kubectl cp <path to .bak file> master-0:/tmp -c mssql-server -n <name of your big data cluster>
```

예제:

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n clustertest
```

백업 파일이 Pod 컨테이너에 복사되었는지 확인합니다.

```bash
kubectl exec -it master-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

예제:

```bash
kubectl exec -it master-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>백업 파일 복원

다음으로, 데이터베이스 백업을 SQL Server 마스터 인스턴스로 복원합니다.  Windows에서 만든 데이터베이스 백업을 복원하는 경우 파일 이름을 가져와야 합니다.  Azure Data Studio에서 마스터 인스턴스에 연결하고 다음 SQL 스크립트를 실행합니다.

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

예제:

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![백업 파일 목록](media/restore-database/database-restore-file-list.png)

이제 데이터베이스를 복원합니다. 다음 스크립트는 예제입니다. 데이터베이스 백업에 따라 필요한 경우 이름/경로를 바꿉니다.

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>데이터 풀 및 HDFS 액세스 구성

이제 SQL Server 마스터 인스턴스가 데이터 풀과 HDFS에 액세스하도록 데이터 풀 및 스토리지 풀 저장 프로시저를 실행합니다. 새로 복원된 데이터베이스에 대해 다음 Transact-SQL 스크립트를 실행합니다.

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> 이전 버전의 SQL Server에서 복원된 데이터베이스에 대해서만 이러한 설정 스크립트를 실행해야 합니다. SQL Server 마스터 인스턴스에서 새 데이터베이스를 만드는 경우 데이터 풀 및 스토리지 풀 저장 프로시저가 이미 구성되어 있습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 다음 개요를 참조하세요.

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)
