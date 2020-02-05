---
title: 트랜잭션 로그 파일 크기 관리 | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
- manage log size
- log size, manage
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ff886f2eea70b010a2e64513cd561cf7f78d8dee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68084026"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>트랜잭션 로그 파일의 크기 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션 로그 크기 모니터링, 트랜잭션 로그 축소, 트랜잭션 로그 파일에 추가 또는 파일 확장, **tempdb** 트랜잭션 로그 증가율 최적화, 트랜잭션 로그 파일 증가 제어 등을 수행하는 방법에 대해 설명합니다.  

##  <a name="MonitorSpaceUse"></a>로그 공간 사용 모니터링  
[sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)를 사용하여 로그 공간 사용을 모니터링합니다. 이 DMV는 현재 사용된 로그 공간 크기에 대한 정보를 반환하고 트랜잭션 로그 잘림을 수행해야 하는 시기를 나타냅니다. 

로그 파일의 현재 크기 및 최대 크기, 파일의 자동 증가 옵션에 대한 정보를 보기 위해 **sys.database_files**에서 해당 로그 파일의 **size**, **max_size** 및 [growth](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 열을 사용할 수도 있습니다.  
  
> [!IMPORTANT]
> 로그 디스크가 오버로드되지 않도록 하세요. 로그 스토리지가 트랜잭션 로드에 대한 [IOPS](https://wikipedia.org/wiki/IOPS) 및 지연 시간 요구 사항을 견딜 수 있는지 확인하세요. 
  
##  <a name="ShrinkSize"></a> 로그 파일 크기 축소  
 실제 로그 파일의 크기를 줄이려면 로그 파일을 축소해야 합니다. 이는 트랜잭션 로그 파일에 사용되지 않은 공간이 포함되어 있는 경우에 유용합니다. 데이터베이스가 온라인 상태이고 하나 이상의 [가상 로그 파일(VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)에 여유 공간이 있는 경우에만 로그 파일을 축소할 수 있습니다. 경우에 따라 다음에 로그가 잘릴 때까지 로그를 축소하지 못할 수도 있습니다.  
  
> [!NOTE]
> 장기 실행 트랜잭션과 같이 오랜 시간 동안 [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)를 활성 상태로 유지하는 요소가 있으면 로그 축소가 제한되거나 로그를 전혀 축소하지 못할 수 있습니다. 자세한 내용은 [로그 잘림을 지연시킬 수 있는 요소](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)를 참조하세요.  
  
로그 파일을 축소하면 논리 로그 부분이 포함되지 않은 하나 이상의 [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)(*비활성 VLF*)가 제거됩니다. 트랜잭션 로그 파일을 축소하면 비활성 VLF가 로그 파일의 끝에서 제거되어 로그가 대략적인 대상 크기로 줍니다. 

> [!IMPORTANT]
> 트랜잭션 로그를 줄이기 전에 [로그 잘림을 지연시킬 수 있는 요소](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation)를 염두에 두세요. 로그 축소 후 스토리지 공간이 다시 필요하면 트랜잭션 로그가 다시 커지고 로그 확장 작업 중에 성능 오버헤드가 발생합니다. 자세한 내용은 이 항목의 [권장 사항](#Recommendations)을 참조하세요.
  
 **로그 파일 축소(데이터베이스 파일의 축소 없이)**  
  
-   [DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [파일 축소](../../relational-databases/databases/shrink-a-file.md)  
  
 **로그 파일 축소 이벤트 모니터링**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)입니다.  
  
 **로그 공간 모니터링**  
  
-   [sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)  
  
-   [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)(로그 파일 또는 파일의 **size**, **max_size** 및 **growth** 열 참조)  
  
##  <a name="AddOrEnlarge"></a> 로그 파일 추가 또는 확장  
디스크 공간이 충분한 경우 기존의 로그 파일을 확장하거나 일반적으로 다른 디스크에 있는 데이터베이스에 로그 파일을 추가하여 공간을 확보할 수 있습니다. 로그 공간이 부족하고 로그 파일을 보관하는 볼륨에 디스크 공간이 부족한 경우가 아니라면 하나의 트랜잭션 로그 파일로 충분합니다.   
  
-   로그 파일을 데이터베이스에 추가하려면 `ADD LOG FILE` 문의 `ALTER DATABASE` 절을 사용합니다. 로그 파일을 추가하면 로그가 확장될 수 있습니다.  
-   로그 파일을 확대하려면 `MODIFY FILE` 문의 `ALTER DATABASE` 절을 사용하여 `SIZE` 및 `MAXSIZE` 구문을 지정합니다. 자세한 내용은 [ALTER DATABASE &#40;Transact-SQL&#41; 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.  

자세한 내용은 이 항목의 [권장 사항](#Recommendations)을 참조하세요.
    
##  <a name="tempdbOptimize"></a> tempdb 트랜잭션 로그 크기 최적화  
 서버 인스턴스를 다시 시작하면 **tempdb** 데이터베이스의 트랜잭션 로그가 자동 증가 이전의 원래 크기로 다시 조정됩니다. 이 경우 **tempdb** 트랜잭션 로그의 성능이 저하될 수 있습니다. 
 
 서버 인스턴스를 시작하거나 다시 시작한 후에 **tempdb** 트랜잭션 로그의 크기를 늘려 이 오버헤드를 방지할 수 있습니다. 자세한 내용은 [tempdb Database](../../relational-databases/databases/tempdb-database.md)을(를) 참조하세요.  
  
##  <a name="ControlGrowth"></a> 트랜잭션 로그 파일 증가 제어  
 트랜잭션 로그 파일의 증가를 관리하기 위해 [ALTER DATABASE&#40;Transact-SQL&#41; 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 문을 사용합니다. 다음 사항에 유의하세요.  
  
-   현재 파일의 크기(KB, MB, GB 및 TB 단위)를 변경하려면 `SIZE` 옵션을 사용합니다.  
-   증분을 변경하려면 `FILEGROWTH` 옵션을 사용합니다. 값 0은 자동 증가를 사용하지 않고 추가 공간을 허용하지 않음을 나타냅니다.  
-   로그 파일의 최대 크기(KB, MB, GB 및 TB 단위)를 제어하거나 증가를 UNLIMITED로 설정하려면 `MAXSIZE` 옵션을 사용합니다.  

자세한 내용은 이 항목의 [권장 사항](#Recommendations)을 참조하세요.

## <a name="Recommendations"></a> 권장 사항
다음은 트랜잭션 로그 파일 작업 시 일반적으로 권장되는 사항입니다.

-   `FILEGROWTH` 옵션으로 설정된 대로 트랜잭션 로그의 자동 증가(자동 증가) 증분은 워크로드 트랜잭션의 요구를 앞설 수 있도록 커야 합니다. 로그 파일의 파일 증가분이 충분히 커야 자주 확장하는 번거로움을 피할 수 있습니다. 트랜잭션 로그의 크기를 적절히 조정하는 좋은 방법은 다음과 같은 시간 동안 사용된 로그의 양을 모니터링하는 것입니다.
    -  완료될 때까지 로그를 백업할 수 없기 때문에 전체 백업을 실행하는 데 필요한 시간.
    -  가장 큰 인덱스 유지 보수 작업에 필요한 시간.
    -  데이터베이스에서 가장 큰 일괄 처리를 실행하는 데 필요한 시간.

-   **옵션을 사용하여 데이터 및 로그 파일에 대해**자동 증가`FILEGROWTH`를 설정한 경우, 백분율은 계속 증가하는 양이기 때문에 **백분율**보다 **크기**에서 설정하는 것이 확장률을 더 잘 제어할 수 있습니다.
    -  트랜잭션 로그는 [인스턴트 파일 초기화](../../relational-databases/databases/database-instant-file-initialization.md)를 활용할 수 없기 때문에 확장된 로그 증가 시간이 특히 중요합니다. 
    -  모범 사례에서는 트랜잭션 로그에 대해 `FILEGROWTH` 옵션 값을 1,024MB 이상으로 설정하지 않습니다. `FILEGROWTH` 옵션에 대한 기본값은 다음과 같습니다.  
  
      |버전|기본값|  
      |-------------|--------------------|  
      |[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]로 시작|데이터는 64MB입니다. 로그 파일은 64MB입니다.|  
      |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 시작|데이터는 1MB입니다. 로그 파일은 10%입니다.|  
      |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전|데이터는 10%입니다. 로그 파일은 10%입니다.|  

-   작은 확장 증분은 너무 많은 [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)가 생성되어 성능이 저하될 수 있습니다. 주어진 인스턴스의 모든 데이터베이스의 현재 트랜잭션 로그 크기에 대한 최적의 VLF 분포 및 필수 크기를 수행할 필수 성장 증분을 결정하려면 이 [스크립트](https://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)를 참조하세요.

-   큰 확장 증분은 너무 적고 큰 [VLF](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)가 생성되어 이 또한 성능에 영향을 줄 수 있습니다. 주어진 인스턴스의 모든 데이터베이스의 현재 트랜잭션 로그 크기에 대한 최적의 VLF 분포 및 필수 크기를 수행할 필수 성장 증분을 결정하려면 이 [스크립트](https://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs)를 참조하세요. 

-   자동 증가를 사용하는 경우에도 쿼리의 요구 사항을 충족시킬 정도로 빠르게 커질 수 없는 경우 트랜잭션 로그가 꽉 찼다는 메시지를 받을 수 있습니다. 확장 증분 변경에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41; 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)을 참조하세요.

-   트랜잭션 로그 파일이 동일한 파일 그룹의 데이터 파일처럼 [비례 채우기](../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill)를 사용하지 않기 때문에 데이터베이스에 여러 로그 파일을 저장해도 성능이 향상되지 않습니다.  

-   로그 파일은 자동으로 축소되도록 설정할 수 있습니다. 그러나 이것은 **권장되지 않으며** **auto_shrink** 데이터베이스 속성은 기본적으로 FALSE로 설정됩니다. **auto_shrink**를 TRUE로 설정하면 파일 공간의 25% 이상이 사용되지 않을 때만 자동 축소에 의해 파일 크기가 줄어듭니다. 
    -   파일은 파일의 25%만 사용되지 않을 때의 크기 또는 파일의 원래 크기 중 더 큰 크기로 축소됩니다. 
    -   **auto_shrink** 속성의 설정 변경에 대한 자세한 내용은 [데이터베이스의 속성 보기 또는 변경](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md) 또는 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요. 
  
## <a name="see-also"></a>참고 항목  
[BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
[꽉 찬 트랜잭션 로그 문제 해결&#40;SQL Server 오류 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)    
[SQL Server 트랜잭션 로그 아키텍처 및 관리 가이드의 트랜잭션 로그 백업](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)    
[트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[ALTER DATABASE &#40;Transact-SQL&#41; 파일 및 파일 그룹 옵션](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)
