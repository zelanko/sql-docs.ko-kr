---
title: 가속 데이터베이스 복구 | Microsoft Docs
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
ms.reviewer: kfarlee
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8fea43ea41bc3e65fa0a6b36c7557322431e95fd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75245258"
---
# <a name="manage-accelerated-database-recovery"></a>가속 데이터베이스 복구 관리

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="enabling-and-controlling-adr"></a>ADR 사용 설정 및 제어

ADR은 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]기본적으로 해제되어 있으며 DDL 구문을 사용하여 제어할 수 있습니다.
```sql
ALTER DATABASE [DB] SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
[(PERSISTENT_VERSION_STORE_FILEGROUP = { filegroup name }) ];

```

이 구문을 사용하여 기능 설정 여부를 제어하고 *PVS(영구 버전 저장소)* 데이터의 특정 파일 그룹을 지정합니다. 파일 그룹을 지정하지 않으면 PVS가 기본 파일 그룹에 저장됩니다.

## <a name="managing-the-persistent-version-store-filegroup"></a>영구 버전 저장소 파일 그룹 관리
ADR 기능은 서로 다른 버전의 데이터 요소를 사용하여 PVS에 유지되는 버전의 변경 내용을 기반으로 합니다.
PVS가 있는 위치와 PVS의 데이터 크기를 관리하는 방법에 대한 고려 사항이 있습니다.

### <a name="to-enable-adr-without-specifying-a-filegroup"></a>파일 그룹을 지정하지 않고 ADR을 사용하도록 설정하려면

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON;
GO
```

이 경우 pvs 파일 그룹을 지정하지 않으면 `PRIMARY` 파일 그룹에 PVS 데이터가 저장됩니다.

### <a name="to-enable-adr-and-specify-that-the-pvs-should-be-stored-in-the-versionstorefg-filegroup"></a>ADR을 사용하도록 설정하고 PVS를 [VersionStoreFG] 파일 그룹에 저장하도록 지정하려면

이 스크립트를 실행하기 전에 파일 그룹을 만듭니다.

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
(PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
```

### <a name="to-disable-the-adr-feature"></a>ADR 기능을 사용하지 않도록 설정하려면

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
GO
```

ADR 기능을 사용하지 않도록 설정된 후에도 논리적 되돌리기를 위해 시스템에 필요한 버전은 영구 버전 저장소에 저장됩니다.

### <a name="change-the-location-of-the-pvs-to-a-different-filegroup"></a>PVS의 위치를 다른 파일 그룹으로 변경

여러 가지 이유로 PVS의 위치를 다른 파일 그룹으로 이동해야 할 수 있습니다. 예를 들어 PVS에 더 많은 공간이 필요하거나 더 빠른 스토리지를 사용해야 할 수 있습니다.

PVS의 위치를 변경하는 과정은 세 단계로 진행됩니다.

1. ADR 기능을 끕니다.

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
   GO
   ```

2. PVS에 저장된 모든 버전을 해제할 수 있을 때까지 기다립니다.

   영구 버전 저장소의 새 위치를 사용하여 ADR을 설정하려면 먼저 모든 버전 정보가 이전 PVS 위치에서 제거되었는지 확인해야 합니다. 정리가 강제로 이루어지도록 하려면 다음 명령을 실행합니다.

   ```sql
   EXEC sys.sp_persistent_version_cleanup [database name]
   ```

   `sys.sp_persistent_version_cleanup` 저장 프로시저는 동기적입니다. 즉, 모든 버전 정보가 현재 PVS에서 정리될 때까지 완료되지 않습니다.  완료되면 DMV `sys.dm_persistent_version_store_stats`를 쿼리하고 `persistent_version_store_size_kb`의 값을 검사하여 버전 정보가 실제로 제거되었는지 확인할 수 있습니다.

   ```sql
   SELECT DB_Name(database_id), persistent_version_store_size_kb 
   FROM sys.dm_tran_persistent_version_store_stats where database_id = [MyDatabaseID]
   ```

   persistent_version_store_size_kb의 값이 0이면 ADR 기능을 다시 사용하도록 설정하여 새 파일 그룹에 배치되도록 PVS를 구성합니다.

1. PVS의 새 위치를 지정하는 ADR 설정

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
   (PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
   ```

## <a name="troubleshooting"></a>문제 해결

`sys.dm_tran_persistent_version_store_stats`를 쿼리하여 PVS 크기를 확인합니다.

`% of DB` 크기를 확인합니다. 또한 일반적인 크기와의 차이를 확인합니다.

PVS는 기준선보다 훨씬 크거나 데이터베이스 크기의 50%에 가까운 경우 큰 것으로 간주됩니다. 

1. `oldest_active_transaction_id`를 검색하고 트랜잭션 ID를 기준으로 `sys.dm_tran_database_transactions`를 쿼리하여 이 트랜잭션이 매우 긴 시간 동안 활성 상태인지 여부를 확인합니다.

   활성 트랜잭션이 PVS를 정리하는 것을 방지합니다.

1. 데이터베이스가 가용성 그룹의 일부인 경우 `secondary_low_water_mark`를 확인합니다. 이는 `low_water_mark_for_ghosts`에 의해 보고된 `sys.dm_hadr_database_replica_states`와 동일합니다. `sys.dm_hadr_database_replica_states`를 쿼리하여 복제본 중 하나가 이 값을 보유하고 있는지 확인합니다. 이 경우 pvs 정리도 방지됩니다.
1. `min_transaction_timestamp`(또는 `online_index_min_transaction_timestamp`)를 확인하고 이를 기반으로 `sys.dm_tran_active_snapshot_database_transactions` 열에 대한 `transaction_sequence_num`를 확인하여 PVS 정리를 보유한 이전 스냅숏 트랜잭션이 있는 세션을 찾습니다.
1. 위의 사항이 적용되지 않는 경우에는 중단된 트랜잭션이 정리를 보유하고 있음을 의미합니다. `aborted_version_cleaner_last_start_time` 및 `aborted_version_cleaner_last_end_time`의 마지막 시간을 확인하여 중단된 트랜잭션 정리가 완료되었는지 확인합니다. `oldest_aborted_transaction_id`는 중단된 트랜잭션 정리가 완료된 후 더 높은 수준으로 이동해야 합니다.
1. 중단된 트랜잭션이 최근에 성공적으로 완료되지 않은 경우 `VersionCleaner` 문제를 보고하는 메시지에 대한 오류 로그를 확인합니다.
