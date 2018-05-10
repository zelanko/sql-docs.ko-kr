---
title: sys.dm_tran_session_transactions (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4df6afdab47fc0da07412223b394ad0dc77a81f7
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  연결된 트랜잭션 및 세션에 대한 상관 관계 정보를 반환합니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_tran_session_transactions**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|트랜잭션을 실행하고 있는 세션의 ID입니다.|  
|transaction_id|**bigint**|트랜잭션 ID입니다.|  
|transaction_descriptor|**binary(8)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 클라이언트 드라이버와 통신할 때 사용하는 트랜잭션 식별자입니다.|  
|enlist_count|**int**|트랜잭션에서 작동 중인 세션의 활성 요청 수입니다.|  
|is_user_transaction|**bit**|1 = 사용자 요청에 의해 시작된 트랜잭션<br /><br /> 0 = 시스템 트랜잭션|  
|is_local|**bit**|1 = 로컬 트랜잭션<br /><br /> 0 = 분산 트랜잭션 또는 참여한 바운드 세션 트랜잭션|  
|is_enlisted|**bit**|1 = 참여한 분산 트랜잭션<br /><br /> 0 = 참여한 분산 트랜잭션 아님|  
|is_bound|**bit**|1 = 바운드 세션을 통해 세션에서 활성화된 트랜잭션<br /><br /> 0 = 바운드 세션을 통해 세션에서 활성화되지 않은 트랜잭션|  
|open_transaction_count||각 세션에 대해 열린 트랜잭션 수입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="remarks"></a>주의  
 바운드 세션 및 분산 트랜잭션을 통해 둘 이상의 세션에서 트랜잭션을 실행할 수 있습니다. 이 경우 sys.dm_tran_session_transactions는 트랜잭션이 실행되고 있는 각 세션에 대해 하나씩 동일한 transaction_id에 대한 여러 개의 행을 표시합니다.  
  
 MARS(Multiple Active Result Sets)를 사용하여 자동 커밋 모드에서 여러 개의 요청을 실행하면 단일 세션에 둘 이상의 활성 트랜잭션이 있을 수 있습니다. 이 경우 sys.dm_tran_session_transactions는 해당 세션에서 실행되고 있는 각 트랜잭션에 대해 하나씩 동일한 session_id에 대한 여러 개의 행을 표시합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


