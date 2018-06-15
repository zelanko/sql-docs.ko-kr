---
title: sys.dm_db_xtp_object_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_object_stats_TSQL
- sys.dm_db_xtp_object_stats
- dm_db_xtp_object_stats
- sys.dm_db_xtp_object_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_object_stats dynamic management view
ms.assetid: 07300b59-3cab-4d3e-8138-5ea8f584f88f
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5b6faed35e58044263ea6563a43fd85ada94bbae
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464849"
---
# <a name="sysdmdbxtpobjectstats-transact-sql"></a>sys.dm_db_xtp_object_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  마지막 데이터베이스 다시 시작 이후 각 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 개체에서 수행된 작업의 영향을 받는 행 수를 보고합니다. 트랜잭션이 커밋되거나 롤백되는지 여부에 관계없이 작업이 실행될 때 통계가 업데이트됩니다.  
  
 sys.dm_db_xtp_object_stats를 사용하면 가장 많이 변경되는 메모리 최적화 테이블을 식별할 수 있습니다. 각 인덱스가 성능에 영향을 미치므로, 사용되지 않는 또는 거의 사용되지 않는 인덱스를 제거하도록 결정할 수 있습니다. 해시 인덱스가 있으면 버킷 수를 주기적으로 다시 평가해야 합니다. 자세한 내용은 [Determining the Correct Bucket Count for Hash Indexes](http://msdn.microsoft.com/library/6d1ac280-87db-4bd8-ad43-54353647d8b5)을 참조하세요.  
  
 sys.dm_db_xtp_object_stats를 사용하면 응용 프로그램 성능에 영향을 줄 수 있는 쓰기-쓰기 충돌이 발생하는 메모리 최적화 테이블을 식별할 수 있습니다. 예를 들어 트랜잭션 다시 시도 논리가 있을 경우 동일한 문을 두 번 이상 실행해야 할 수 있습니다. 또한 이 정보를 사용해서 쓰기-쓰기 오류 처리가 필요한 테이블(및 비즈니스 논리)을 식별할 수 있습니다.  
  
 이 뷰에는 데이터베이스에 있는 각 메모리 액세스에 최적화된 테이블의 열이 포함됩니다.  
  
 자세한 내용은 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|개체의 ID입니다.|  
|row_insert_attempts|**bigint**|마지막 데이터베이스 다시 시작 이후 커밋된 트랜잭션 및 중단된 트랜잭션 모두에 의해 테이블에 삽입된 행 수입니다.|  
|row_update_attempts|**bigint**|마지막 데이터베이스 다시 시작 이후 커밋된 트랜잭션 및 중단된 트랜잭션 모두에 의해 테이블에서 업데이트된 행 수입니다.|  
|row_delete_attempts|**bigint**|마지막 데이터베이스 다시 시작 이후 커밋된 트랜잭션 및 중단된 트랜잭션 모두에 의해 테이블에서 삭제된 행 수입니다.|  
|write_conflicts|**bigint**|마지막 데이터베이스 다시 시작 이후 발생한 쓰기 충돌 수입니다.|  
|unique_constraint_violations|**bigint**|마지막 데이터베이스 다시 시작 이후 발생한 UNIQUE 제약 조건 위반 수입니다.|  
|object_address|**varbinary(8)**|내부적으로만 사용됩니다.|  
  
## <a name="permissions"></a>Permissions  
 현재 데이터베이스에 대해 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 액세스에 최적화 된 테이블 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
