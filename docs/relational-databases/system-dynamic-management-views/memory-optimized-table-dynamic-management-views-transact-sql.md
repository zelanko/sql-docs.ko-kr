---
title: 메모리 액세스에 최적화 된 테이블 동적 관리 뷰 (Transact-sql)
description: SQL Server의 메모리 내 OLTP에 사용 되는 SQL Server 동적 관리 뷰 및 개체 카탈로그 뷰에 대해 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 02/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ccd82fed-1a3f-47de-85c4-1c9bdd80b027
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b99bf0b996b94ebe96033a2d5a25a5e189cd65ca
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546677"
---
# <a name="memory-optimized-table-dynamic-management-views-transact-sql"></a>메모리 액세스에 최적화된 테이블 동적 관리 뷰(Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dmv (동적 관리 뷰)는 메모리 내 OLTP와 함께 사용 됩니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  

:::row:::
    :::column:::
        [dm_db_xtp_checkpoint_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-stats-transact-sql.md)

        [dm_db_xtp_gc_cycle_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-gc-cycle-stats-transact-sql.md)

        [sys.dm_db_xtp_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)

        [sys.dm_db_xtp_merge_requests(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-merge-requests-transact-sql.md)

        [sys.dm_db_xtp_nonclustered_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-nonclustered-index-stats-transact-sql.md)

        [dm_db_xtp_transactions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-transactions-transact-sql.md)

        [dm_xtp_gc_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-stats-transact-sql.md)

        [dm_xtp_transaction_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-transaction-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [dm_db_xtp_checkpoint_files &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)

        [sys.dm_db_xtp_hash_index_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql.md)

        [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)

        [sys.dm_db_xtp_object_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-object-stats-transact-sql.md)

        [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md)

        [dm_xtp_gc_queue_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)

        [dm_xtp_system_memory_consumers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-system-memory-consumers-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="object-catalog-views"></a>개체 카탈로그 뷰

다음 개체 카탈로그 뷰는 메모리 내 OLTP에서 특별히 사용 됩니다.

:::row:::
    :::column:::
        [sys.hash_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)
    :::column-end:::
    :::column:::
        [sys.memory_optimized_tables_internal_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="internal-dmvs"></a>내부 Dmv

내부용으로 제공 되며 직접 설명서를 제공 하지 않는 추가 Dmv가 있습니다. 메모리 최적화 테이블의 영역에서 문서화 되지 않은 Dmv에는 다음이 포함 됩니다.

- sys. dm_xtp_threads
- sys. dm_xtp_transaction_recent_rows

