---
title: 백업 압축(SQL Server) | Microsoft 문서
description: 제한 사항, 성능에 미치는 영향, 백업 압축 구성, 압축 비율과 같은 SQL Server 백업의 압축에 대해 알아봅니다.
ms.custom: ''
ms.date: 07/08/2020
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], backup compression
- backup compression [SQL Server], about backup compression
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- backing up [SQL Server], backup compression
- backup compression [SQL Server]
ms.assetid: 05bc9c4f-3947-4dd4-b823-db77519bd4d2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 56c2f2cadd998a6daba51b46e46e2c141e1f0f38
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810289"
---
# <a name="backup-compression-sql-server"></a>백업 압축(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 제한 사항, 백업 압축이 성능에 미치는 영향, 백업 압축의 구성 및 압축 비율을 비롯하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업의 압축에 대해 설명합니다.  백업 압축은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise, Standard 및 Developer 버전에서 지원됩니다.  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 모든 버전에서는 압축된 백업을 복원할 수 있습니다. 
 
  
##  <a name="benefits"></a><a name="Benefits"></a> 이점  
  
-   압축된 백업은 동일한 데이터의 압축되지 않은 백업보다 작으므로 일반적으로 백업 압축에 필요한 디바이스 I/O가 더 적고 따라서 백업 속도가 크게 향상됩니다.  
  
     자세한 내용은 이 항목 뒷부분의 [백업 압축이 성능에 미치는 영향](#PerfImpact)을 참조하십시오.  
  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> 제한 사항  
 다음은 압축된 백업에 적용되는 제한 사항입니다.  
  
-   압축된 백업과 압축되지 않은 백업은 미디어 세트에 동시에 존재할 수 없습니다.  
  
-   이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 압축된 백업을 읽을 수 없습니다.  
  
-   NTbackup은 압축된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업과 테이프를 공유할 수 없습니다.  
  
  
##  <a name="performance-impact-of-compressing-backups"></a><a name="PerfImpact"></a> 백업 압축이 성능에 미치는 영향  
 기본적으로 압축하면 CPU 사용량이 크게 늘어나고 압축 프로세스로 사용되는 추가 CPU는 동시 작업에 악영향을 줄 수 있습니다. 따라서 CPU 사용량이[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다. 자세한 내용은 이 항목 뒷부분의 [Resource GovernoR을 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)에 의해 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다.  
  
 백업 I/O 성능을 손쉽게 확인하려면 다음과 같은 성능 카운터를 평가하여 백업 I/O를 디바이스로 격리하거나 디바이스에서 격리하면 됩니다.  
  
-   물리적 디스크 카운터 등의 Windows I/O 성능 카운터  
  
-   **SQLServer:Backup Device** 개체의 [Device Throughput Bytes/sec](../../relational-databases/performance-monitor/sql-server-backup-device-object.md) 카운터  
  
-   **SQLServer:Databases** 개체의 [Backup/Restore Throughput/sec](../../relational-databases/performance-monitor/sql-server-databases-object.md) 카운터  
  
 Windows 카운터에 대한 자세한 내용은 Windows 도움말을 참조하십시오. SQL Server 카운터로 작업하는 방법은 [SQL Server 개체 사용](../../relational-databases/performance-monitor/use-sql-server-objects.md)을 참조하세요.  
  
   
##  <a name="calculate-the-compression-ratio-of-a-compressed-backup"></a><a name="CompressionRatio"></a> 압축된 백업의 압축 비율 계산  
 백업의 압축 비율을 계산하려면 **backupset** 기록 테이블의 **backup_size** 및 [compressed_backup_size](../../relational-databases/system-tables/backupset-transact-sql.md) 열에서 백업의 값을 다음과 같이 사용합니다.  
  
 **backup_size**:**compressed_backup_size**  
  
 예를 들어 3:1 압축 비율은 디스크 공간을 약 66% 절약할 수 있음을 나타냅니다. 이러한 열에 대해 쿼리하려면 다음 Transact-SQL 문을 사용하면 됩니다.  
  
```sql  
SELECT backup_size/compressed_backup_size FROM msdb..backupset;  
```  
  
 압축된 백업의 압축 비율은 압축된 데이터에 따라 달라집니다. 다양한 요소가 결과 압축 비율에 영향을 줄 수 있습니다. 주요 요소는 다음과 같습니다.  
  
-   데이터의 형식입니다.  
  
     문자 데이터는 다른 형식의 데이터보다 압축률이 높습니다.  
  
-   페이지의 행에 포함된 데이터의 일관성  
  
     일반적으로 한 페이지에 필드의 값이 같은 행이 여러 개 있는 경우 이 값에 상당한 압축이 발생할 수 있습니다. 반면 임의의 데이터가 들어 있거나 페이지당 하나의 큰 행만 들어 있는 데이터베이스의 경우 압축된 백업의 크기가 압축되지 않은 백업의 크기와 거의 같습니다.  
  
-   데이터의 암호화 여부  
  
     암호화된 데이터는 암호화되지 않은 데이터보다 압축률이 크게 낮습니다. 예를 들어 Always Encrypted 또는 다른 애플리케이션 수준 암호화를 사용하여 열 수준에서 데이터를 암호화하는 경우 백업을 압축하면 크기가 크게 줄어들지 않을 수 있습니다.

     TDE(투명한 데이터 암호화)로 암호화된 데이터베이스를 압축하는 방법에 대한 자세한 내용은 [TDE로 백업 압축](#backup-compression-with-tde)을 참조하세요.

-   데이터베이스의 압축 여부  
  
     데이터베이스가 압축된 경우 백업을 압축하면 크기가 줄어들더라도 많이 줄어들지 않을 수 있습니다.  

## <a name="backup-compression-with-tde"></a>TDE로 백업 압축

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터, **65536(64KB)보다 큰** `MAXTRANSFERSIZE`를 설정 시 압축 알고리즘이 사용됩니다. 이 알고리즘은 먼저 페이지를 해독하고 압축한 다음 다시 암호화하는 [TDE(투명한 데이터 암호화)](../../relational-databases/security/encryption/transparent-data-encryption.md)로 암호화된 데이터베이스에 최적화되어 있습니다. `MAXTRANSFERSIZE`를 지정하지 않은 경우 또는 `MAXTRANSFERSIZE = 65536`(64KB)을 사용하는 경우 TDE 암호화 데이터베이스를 통해 백업 압축을 수행하면 암호화된 페이지가 바로 압축되어 압축률이 좋지 않을 수 있습니다. 자세한 내용은 [TDE 가능 데이터베이스의 백업 압축](/archive/blogs/sqlcat/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases)을 참조하세요.

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CU5부터 더 이상 이 TDE를 사용하는 최적화된 압축 알고리즘을 사용하도록 `MAXTRANSFERSIZE`를 설정할 필요가 없습니다. 백업 명령에 `WITH COMPRESSION`이 지정되거나 *백업 압축 기본값* 서버 구성이 1로 설정되어 있으면 `MAXTRANSFERSIZE`가 자동으로 128K로 증가하여 최적화된 알고리즘을 사용하도록 설정합니다. 백업 명령에 `MAXTRANSFERSIZE`가 64K를 초과하는 값으로 지정되면 제공된 값이 적용됩니다. 즉, SQL Server는 자동으로 이 값을 줄이지 않고 늘리기만 합니다. `MAXTRANSFERSIZE = 65536`을 사용하여 TDE 암호화 데이터베이스를 백업해야 하는 경우 `WITH NO_COMPRESSION`를 지정하거나 *백업 압축 기본값* 서버 구성이 0으로 설정되어 있어야 합니다.

자세한 내용은 [BACKUP(Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.

##  <a name="allocation-of-space-for-the-backup-file"></a><a name="Allocation"></a> 백업 파일에 대한 공간 할당  
 압축된 백업에 대한 최종 백업 파일의 크기는 데이터의 압축 가능한 정도에 따라 달라지며, 백업 작업이 완료되기 전까지는 크기를 알 수 없습니다.  따라서 기본적으로 압축을 사용하여 데이터베이스를 백업할 때 데이터베이스 엔진은 백업 파일에 대한 사전 할당 알고리즘을 사용합니다. 이 알고리즘을 사용하면 백업 파일의 데이터베이스 크기에 대해 미리 정의된 백분율이 사전 할당됩니다. 백업하는 동안 더 많은 공간이 필요한 경우 데이터베이스 엔진은 파일을 늘립니다. 백업 작업의 마지막에 최종 크기가 할당된 공간보다 작으면 데이터베이스 엔진이 파일을 백업의 실제 최종 크기로 축소합니다.  
  
 백업 파일을 최종 크기에 도달하는 데 필요한 만큼만 늘리도록 허용하려면 추적 플래그 3042를 사용합니다. 추적 플래그 3042를 사용하면 백업 작업에서 기본 백업 압축 사전 할당 알고리즘을 무시합니다. 이 추적 플래그는 압축된 백업에 실제로 필요한 크기만 할당하여 공간에 저장해야 하는 경우 유용합니다. 그러나 이 추적 플래그를 사용하면 약간의 성능 저하가 발생할 수 있습니다(백업 작업 시간이 늘어날 수 있음).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [백업 압축 구성&#40;SQL Server&#41;](../../relational-databases/backup-restore/configure-backup-compression-sql-server.md)  
  
-   [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
-   [Resource Governor를 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [DBCC TRACEON&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
  
-   [DBCC TRACEOFF&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
