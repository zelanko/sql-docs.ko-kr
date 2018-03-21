---
title: "메모리 액세스에 최적화된 테이블이 포함된 데이터베이스 백업 | Microsoft 문서"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc74c48c5eba25fa502f207b2dc5bd3c17615c42
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블이 포함된 데이터베이스 백업
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  메모리 액세스에 최적화된 테이블은 일반적인 데이터베이스 백업의 일부로 백업됩니다. 디스크 기반 테이블의 경우 저장소 손상을 검색하기 위해 데이터베이스 백업의 일부로 데이터 및 델타 파일 쌍의 CHECKSUM 유효성이 검사됩니다.  
  
> [!NOTE]  
>  백업하는 동안 메모리 최적화 파일 그룹에 있는 하나 이상의 파일에서 CHECKSUM 오류가 발견되면 백업 작업이 실패합니다. 이 경우 확인된 마지막 정상 백업에서 데이터베이스를 복원해야 합니다.  
>   
>  백업이 없는 경우 메모리 최적화 테이블 및 디스크 기반 테이블에서 데이터를 내보낼 수 있으며, 데이터베이스를 삭제하고 다시 만든 뒤 다시 로드할 수 있습니다.  
  
 메모리 최적화 테이블이 하나 이상인 데이터베이스의 전체 백업은 디스크 기반 테이블의 할당된 저장소(있는 경우), 활성 트랜잭션 로그, 메모리 최적화 테이블의 데이터 및 델타 파일 쌍(검사점 파일 쌍이라고도 함)으로 구성됩니다. 그러나 [메모리 최적화 테이블에 대한 내구성](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)에 설명된 대로 메모리 최적화 테이블에서 사용하는 저장소는 메모리 내의 해당 크기보다 훨씬 클 수 있으며, 이는 데이터베이스 백업의 크기에 영향을 미칩니다.  
  
## <a name="full-database-backup"></a>전체 데이터베이스 백업  
 디스크 기반 테이블의 백업 방식은 동일하므로, 여기서는 메모리 최적화 지속형 테이블이 포함된 데이터베이스의 백업에 대해 중점적으로 설명합니다. 메모리 최적화 파일 그룹의 검사점 파일 쌍은 다양한 상태에 있을 수 있습니다. 아래의 표에서는 백업되는 파일의 부분에 대해 설명합니다.  
  
|검사점 파일 쌍 상태|백업|  
|--------------------------------|------------|  
|PRECREATED|파일 메타데이터만|  
|UNDER CONSTRUCTION|파일 메타데이터만|  
|ACTIVE|파일 메타데이터와 사용된 바이트|  
|MERGE TARGET|파일 메타데이터만|  
|WAITING FOR LOG TRUNCATION|파일 메타데이터와 사용된 바이트|  
  
 검사점 파일 쌍의 상태에 대한 설명은 [sys.dm_db_xtp_checkpoint_files&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) 및 해당 열 state_desc를 참조하세요.  
  
 메모리 최적화 테이블이 하나 이상 포함된 데이터베이스 백업의 크기는 일반적으로 메모리 내의 백업 크기보다는 크지만 디스크상 저장소보다는 작습니다. 삭제된 행의 수를 비롯한 여러 요인에 따라 백업이 더 커질 수도 있습니다.  
  
### <a name="estimating-size-of-full-database-backup"></a>전체 데이터베이스 백업의 크기 예측  
  
> [!IMPORTANT]  
>  메모리 내 OLTP에 대한 백업 크기를 추정하려면 BackupSizeInBytes 값을 사용하지 않는 것이 좋습니다.  
  
 첫 번째 작업 시나리오는 대부분 삽입에 해당합니다. 이 시나리오에서 대부분의 데이터 파일은 활성 상태이고 완전히 로드되며 삭제된 행은 거의 없습니다. 데이터베이스 백업의 크기는 메모리 내의 데이터 크기와 비슷합니다.  
  
 두 번째 작업 시나리오에서는 삽입, 삭제 및 업데이트 작업을 많이 수행합니다. 최악의 경우 각 검사점 파일 쌍은 삭제된 행을 고려한 후 50% 로드됩니다. 따라서 데이터베이스 백업의 크기는 적어도 메모리 내 데이터 크기의 2배입니다.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블이 있는 데이터베이스의 차등 백업  
 메모리 최적화 테이블의 저장소는 [메모리 최적화 테이블에 대한 내구성](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)에 설명된 대로 데이터 및 델타 파일로 구성되어 있습니다. 메모리 최적화 테이블이 있는 데이터베이스의 차등 백업에는 다음 데이터가 포함됩니다.  
  
-   메모리 최적화 테이블이 있어도 디스크를 기반으로 테이블을 저장하는 파일 차등 백업은 영향을 받지 않습니다.  
  
-   활성 트랜잭션 로그는 전체 데이터베이스 백업에서 동일합니다.  
  
-   메모리 최적화 데이터 파일 그룹의 경우 차등 백업은 전체 데이터베이스 백업과 동일한 알고리즘을 사용하여 백업 데이터 및 델타 파일을 식별하지만, 그 후에 다음과 같이 하위 집합을 필터링합니다.  
  
    -   데이터 파일은 새로 삽입되는 행을 포함하며, 가득 찬 데이터 파일은 닫혀 읽기 전용으로 표시됩니다. 데이터 파일은 마지막 전체 데이터베이스 백업 후 닫힌 경우에만 백업됩니다. 차등 백업에서는 마지막 전체 데이터베이스 백업 이후로 삽입된 행을 포함하는 데이터 파일만 백업합니다. 단, 업데이트 및 삭제 시나리오는 예외입니다. 이러한 시나리오에서는 삽입된 행 중 일부가 이미 가비지 수집용으로 표시되었거나 이미 가비지 수집되었을 수 있기 때문입니다.  
  
    -   델타 파일은 삭제된 데이터 행에 대한 참조를 저장합니다. 향후의 트랜잭션에서 행을 삭제할 수 있으므로 델타 파일은 언제든지 수정 가능하며 절대로 닫히지 않습니다. 델타 파일은 항상 백업됩니다. 델타 파일은 일반적으로 10% 미만의 저장소를 사용하므로 차등 백업의 크기에 미치는 영향이 최소화됩니다.  
  
 메모리 최적화 테이블이 데이터베이스 크기의 상당 부분을 차지하는 경우 차등 백업으로 데이터베이스 백업의 크기를 대폭 줄일 수 있습니다. 일반적인 OLTP 작업의 경우 차등 백업이 전체 데이터베이스 백업보다 상당히 작습니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 테이블의 백업, 복원 및 복구](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
