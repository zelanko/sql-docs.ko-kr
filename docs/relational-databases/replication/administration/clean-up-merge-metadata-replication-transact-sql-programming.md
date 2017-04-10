---
title: "병합 메타데이터 정리(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "메타데이터 [SQL Server 복제]"
  - "sp_mergemetadataretentioncleanup"
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 병합 메타데이터 정리(복제 Transact-SQL 프로그래밍)
  병합 복제 메타데이터는 게시에 대한 보존 기간 설정에 따라 병합 에이전트에 의해 정기적으로 정리됩니다. 이 게시자 및 구독자에서 발생 하는 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), 및 [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 시스템 테이블입니다. 복제 저장 프로시저를 사용하여 이러한 테이블의 데이터를 프로그래밍 방식으로 정리할 수도 있습니다.  
  
### 병합 메타데이터를 수동으로 정리하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md)합니다.  
  
2.  (선택 사항) 참고에서 제거 된 행 수에서 1 단계는 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), 및 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 시스템 테이블을 각각 반환 되는 **@num_genhistory_rows**, **@num_contents_rows**, 및 **@num_tombstone_rows** 출력 매개 변수입니다.  
  
3.  구독자에서 1~2단계를 반복하여 구독 데이터베이스의 메타데이터를 정리합니다.  
  
## 참고 항목  
 [구독 만료 및 비활성화](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  