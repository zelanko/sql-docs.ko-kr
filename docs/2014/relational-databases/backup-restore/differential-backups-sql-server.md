---
title: 차등 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- differential backups
- differential backups, about
ms.assetid: 123bb7af-1367-4bde-bfcb-76d36799b905
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5c057e0d41cb46adef0ec1e01c3406190db900e4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958423"
---
# <a name="differential-backups-sql-server"></a>차등 백업(SQL Server)
  이 백업 및 복원 항목은 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 관련됩니다.  
  
 차등 백업은 가장 최근에 수행한 이전 전체 데이터 백업을 기반으로 합니다. 차등 백업은 전체 백업 이후 변경된 데이터만 캡처합니다. 차등 백업의 기반이 되는 전체 백업을 차등의 *기반* 이라고 합니다. 복사 전용 백업을 제외한 전체 백업은 데이터베이스 백업, 부분 백업 및 파일 백업을 포함한 일련의 차등 백업에 대한 기반으로 사용할 수 있습니다. 파일 차등 백업에 대한 기반 백업은 전체 백업, 파일 백업 또는 부분 백업에 포함될 수 있습니다.  
  
  
##  <a name="benefits"></a><a name="Benefits"></a> 이점  
  
-   차등 백업 만들기는 전체 백업 만들기에 비해 매우 빠를 수 있습니다. 차등 백업은 차등 백업의 기반이 되는 전체 백업 이후 변경된 데이터만 기록합니다. 따라서 데이터 손실의 위험을 줄이면서 빈번한 데이터 백업을 간편하게 수행할 수 있습니다. 하지만 차등 백업을 복원하기 전에 기반을 복원해야 합니다. 따라서 차등 백업에서 복원할 경우 두 개의 백업 파일이 필요하기 때문에 전체 백업에서 복원할 때보다 더 많은 단계가 필요하며 더 오랜 시간이 걸립니다.  
  
-   차등 데이터베이스 백업은 특히 데이터베이스 하위 집합이 나머지 데이터베이스보다 자주 수정되는 경우에 유용합니다. 이런 경우 차등 데이터베이스 백업을 사용하면 전체 데이터베이스 백업의 오버헤드를 발생시키지 않고 자주 백업할 수 있습니다.  
  
-   전체 복구 모델에서 차등 백업을 사용하면 복원해야 하는 로그 백업의 수를 줄일 수 있습니다.  
  
##  <a name="overview-of-differential-backups"></a><a name="Overview"></a> 차등 백업 개요  
 차등 백업은 차등 기반을 만든 시간과 차등 백업을 만든 시간 사이에 변경된 *익스텐트* (실제로 연속하는 8페이지의 컬렉션)의 상태를 캡처합니다. 따라서 특정 차등 백업의 크기는 기반 이후 변경된 데이터의 양에 따라 다릅니다. 대체로 기반이 오래된 것일수록 새 차등 백업의 크기가 커집니다. 일련의 차등 백업에서 자주 업데이트된 익스텐트는 각 차등 백업에 다른 데이터를 포함할 수 있습니다.  
  
 다음 그림에서는 차등 백업의 작동 방식을 보여 줍니다. 이 그림에서는 표시된 24개의 데이터 익스텐트 중 6개가 변경되었으며 차등 백업은 이들 6개의 데이터 익스텐트만 포함합니다. 차등 백업 작업은 각 익스텐트에 대해 하나의 비트가 포함된 비트맵 페이지를 사용합니다. 기반 이후 업데이트된 익스텐트의 경우 비트맵의 해당 비트가 1로 설정됩니다.  
  
 ![차등 비트맵에서 변경된 익스텐트 확인](../../database-engine/media/bnr-how-diff-backups-work.gif "차등 비트맵에서 변경된 익스텐트 확인")  
  
> [!NOTE]  
>  복사 전용 백업은 차등 비트맵을 업데이트하지 않습니다. 따라서 후속 차등 백업에 영향을 주지 않습니다.  
  
 생성된 기반 이후 오래 지나지 않아 수행된 차등 백업은 차등 기반보다 크기가 훨씬 작기 때문에 스토리지 공간과 백업 시간이 절약됩니다. 그러나 시간이 지남에 따라 데이터베이스가 변경되면서 데이터베이스와 지정된 차등 기반 간의 차이가 커집니다. 차등 백업과 해당 기반 사이의 간격이 길수록 차등 백업이 더 커집니다. 즉, 차등 백업의 크기가 결국 차등 기반과 비슷해질 수 있습니다. 차등 백업이 크면 더 빠르고 작은 백업으로서의 장점이 사라집니다.  
  
 차등 백업의 크기가 커질수록 차등 백업을 복원할 때 데이터베이스 복원 시간이 훨씬 길어질 수 있습니다. 따라서 새 전체 백업을 지정된 간격으로 수행하여 데이터의 새 차등 기반을 설정하는 것이 좋습니다. 예를 들어 전체 데이터베이스의 전체 백업(즉, 전체 데이터베이스 백업)을 매주 수행하고 주중에 일련의 정기적인 차등 데이터베이스 백업을 수행할 수 있습니다.  
  
 복원 시 차등 백업을 복원하기 전에 먼저 기반을 복원해야 합니다. 그런 다음 가장 최근의 차등 백업만 복원하면 데이터베이스를 차등 백업이 생성된 시점까지 복구할 수 있습니다. 일반적으로 가장 최근의 전체 백업을 복원한 후 해당 전체 백업을 기반으로 하는 가장 최근의 차등 백업을 복원합니다.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블이 있는 데이터베이스의 차등 백업  
 차등 백업 및 메모리 최적화 테이블이 있는 데이터베이스에 대한 자세한 내용은 [메모리 최적화 테이블이 포함된 데이터베이스 백업](../in-memory-oltp/memory-optimized-tables.md)을 참조하세요.  
  
##  <a name="differential-backups-of-read-only-databases"></a><a name="ReadOnlyDbs"></a> 읽기 전용 데이터베이스의 차등 백업  
 읽기 전용 데이터베이스의 경우 차등 백업과 함께 사용하는 것보다는 전체 백업만 사용하는 것이 관리하기 쉽습니다. 데이터베이스가 읽기 전용일 때는 백업 및 기타 작업을 하더라도 파일에 포함된 메타데이터를 변경할 수 없습니다. 따라서 차등 백업이 시작되는 로그 시퀀스 번호(차등 기반 LSN)와 같이 차등 백업에 필요한 메타데이터는 **master** 데이터베이스에 저장됩니다. 차등 기반은 데이터베이스가 읽기 전용인 경우 수행되며 차등 비트맵은 기반 백업 이후에 실제로 발생되는 변경 내용보다 많은 변경 내용을 나타냅니다. **backupset** 시스템 테이블에 저장된 [differential_base_lsn](/sql/relational-databases/system-tables/backupset-transact-sql) 은 데이터가 실제로 기반 백업 이후에 변경되었는지 여부를 결정하는 데 사용되므로 추가 데이터를 백업에서 읽지만 백업에 쓸 수는 없습니다.  
  
 읽기 전용 데이터베이스를 다시 작성하고 다시 저장하거나 분리 또는 연결하는 경우 차등 기반 정보는 손실됩니다. **master** 데이터베이스가 사용자 데이터베이스와 함께 동기화되지 않으므로 이러한 상황이 발생합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 이 문제를 감지하거나 방지하지 못하므로 이후 모든 차등 백업은 가장 최근의 전체 백업을 기반으로 하지 않게 되고 따라서 결과를 예상할 수 없게 됩니다. 새 차등 기반을 설정하려면 전체 데이터베이스 백업을 만드는 것이 좋습니다.  
  
### <a name="best-practices-for-using-differential-backups-with-a-read-only-database"></a>읽기 전용 데이터베이스에 차등 백업을 사용하기 위한 최상의 방법  
 읽기 전용 데이터베이스의 전체 데이터베이스 백업을 만든 다음 후속 차등 백업을 만들려면 **master** 데이터베이스를 백업합니다.  
  
 **master** 데이터베이스가 손실된 경우 우선 이것을 복원한 후에 사용자 데이터베이스의 차등 백업을 복원합니다.  
  
 나중에 차등 백업을 사용하려는 읽기 전용 데이터베이스를 분리 및 연결하는 경우 가능한 빨리 읽기 전용 데이터베이스와 **master** 데이터베이스의 전체 데이터베이스 백업을 수행합니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 복원&#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [전체 데이터베이스 백업&#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [전체 데이터베이스 복원&#40;전체 복구 모델&#41;](complete-database-restores-full-recovery-model.md)   
 [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](complete-database-restores-simple-recovery-model.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
