---
title: 고스트 정리 프로세스 가이드 | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ghost cleanup
- ghost records
- ghost clean up process
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86121ab464175e303ff1d143d8dd64527c22258c
ms.sourcegitcommit: 6fe7b5e8818bd0d94fce693c560d63cc6883d76f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34758063"
---
# <a name="ghost-cleanup-process-guide"></a>고스트 정리 프로세스 가이드

고스트 정리 프로세스는 삭제 표시가 된 페이지에서 레코드를 삭제하는 단일 스레드 백그라운드 프로세스입니다. 다음 문서에서는 이러한 프로세스의 개요를 보여 줍니다.

## <a name="ghost-records"></a>삭제할 레코드

인덱스 페이지의 리프 수준에서 삭제된 레코드는 물리적으로 페이지에서 제거되지 않습니다. 대신 레코드에는 '삭제할' 즉, *고스트*로 표시됩니다. 즉, 행은 페이지에 남아 있지만 행 머리글에서 약간 변경되어 행이 실제로 고스트(삭제할) 레코드임을 나타냅니다. 이는 삭제 작업 도중 성능을 최적화하기 위함입니다. 고스트는 행 수준의 잠금에 필요하지만 행의 이전 버전을 유지해야 할 경우 스냅숏 격리에도 필요합니다.

## <a name="ghost-record-cleanup-task"></a>삭제할 레코드 정리 작업

삭제 즉, *고스트* 표시가 되어 있는 레코드는 백그라운드 고스트 정리 프로세스에 의해 정리됩니다. 이 백그라운드 프로세스는 삭제 트랜잭션이 커밋된 후 실행되며 물리적으로 페이지에서 삭제할 레코드를 제거합니다. 고스트 정리 프로세스는 일정 간격(SQL Server 2012 이상의 경우 5초마다, SQL Server 2008/2008R2의 경우 10초마다)으로 자동으로 실행되며 모든 페이지에 삭제할 레코드 표시가 되어 있는지 확인합니다. 표시가 있는 경우 매번 실행될 때마다 최대 10페이지씩 터치하면서 삭제 즉, *고스트* 표시가 있는 레코드로 이동하여 삭제합니다.

레코드가 삭제될 때 데이터베이스는 삭제될 항목이 있는 것으로 표시되며, 고스트 정리 프로세스는 해당 데이터베이스를 검사만 합니다. 또한 모든 삭제할 레코드가 삭제되면 고스트 정리 프로세스는 데이터베이스를 '삭제할 레코드 없음'으로 표시하며, 다음 번 실행 시 이 데이터베이스는 건너뜁니다. 이 프로세스는 또한 공유 잠금을 사용할 수 없는 모든 데이터베이스를 건너뛰며, 다음 번 실행 시 다시 시도합니다.

아래 쿼리는 단일 데이터베이스에 얼마나 많은 삭제할 레코드가 있는지 식별할 수 있습니다. 

 ```sql
 SELECT sum(ghost_record_count) total_ghost_records, db_name(database_id) 
 FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL)
 group by database_id
 order by total_ghost_records desc
```

## <a name="disable-the-ghost-cleanup"></a>고스트 정리를 사용 안 함

많은 삭제가 있는 고부하 시스템에서 고스트 정리 프로세스는 버퍼 풀에 페이지를 유지하고 IO를 생성하는 것에서 성능 문제를 일으킬 수 있습니다. 추적 플래그 661을 사용하여 이 프로세스를 사용하지 않을 수 있습니다. 이에 대한 자세한 정보는 [고성능 워크로드를 실행하는 경우 SQL Server에 대한 옵션 튜닝](https://support.microsoft.com/help/920093/tuning-options-for-sql-server-when-running-in-high-performance-workloa)을 참조합니다. 그러나 프로세스를 사용하지 않도록 설정함으로써 성능에 미치는 영향이 있습니다.

고스트 정리 프로세스를 사용하지 않도록 설정하면 데이터베이스가 불필요하게 커져 결국 성능 문제를 일으킬 수 있습니다. 고스트 정리 프로세스는 고스트로 표시된 레코드를 제거하므로 이 프로세스를 사용하지 않으면 페이지에 이런 레코드를 그래도 남겨 놓아 SQL Server가 이 공간을 재사용하지 못하게 합니다. 이렇게 하면 SQL Server가 대신 새 페이지에 데이터를 강제로 추가하여 그 결과 데이터베이스 파일이 확장되고 [페이지 분할](indexes/specify-fill-factor-for-an-index.md)을 일으킬 수 있습니다. 페이지 분할은 실행 계획을 만들 때 및 검사 작업을 수행하는 경우 성능 문제로 이어집니다. 

고스트 정리 프로세스가 사용할 수 없도록 설정되면 삭제할 레코드를 제거하기 위해 일부 작업을 수행해야 합니다. 한 옵션은 인덱스 리빌드를 실행하여 데이터를 페이지 주변으로 이동하는 것입니다. 다른 옵션은 수동으로 [sp_clean_db_free_space](system-stored-procedures/sp-clean-db-free-space-transact-sql.md)(모든 데이터베이스 데이터 파일 정리하기 위해) 또는 [sp_clean_db_file_free_space](system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)(단일 데이터베이스 데이터 파일을 정리하기 위해)를 실행하여 삭제할 레코드를 삭제하는 것입니다.

 >[!warning]
 > 고스트 정리 프로세스를 사용하지 않도록 설정하는 것은 일반적으로 권장되지 않습니다. 그래도 이렇게 하는 것은 프로덕션 환경에서 영구적으로 구현되기 전에 제어된 환경에서 철저히 테스트돼야 합니다.


## <a name="next-steps"></a>다음 단계  
[고스트 정리 프로세스를 사용하지 않도록 설정](https://support.microsoft.com/en-us/help/920093/tuning-options-for-sql-server-when-running-in-high-performance-workloa)
<br>[단일 데이터베이스 파일에서 삭제할 레코드 제거](system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)
<br>[모든 데이터베이스 데이터 파일에서 삭제할 레코드 제거](system-stored-procedures/sp-clean-db-free-space-transact-sql.md)


