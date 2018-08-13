---
title: sys.dm_tran_active_transactions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_transactions
- sys.dm_tran_active_transactions_TSQL
- dm_tran_active_transactions_TSQL
- dm_tran_active_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_transactions dynamic management view
ms.assetid: 154ad6ae-5455-4ed2-b014-e443abe2c6ee
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 2fb2bca555102181f9f62d52ba51cdd159042f2a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540733"
---
# <a name="sysdmtranactivetransactions-transact-sql"></a>sys.dm_tran_active_transactions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 트랜잭션 정보를 반환합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_tran_active_transactions**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|데이터베이스 수준이 아닌 인스턴스 수준의 트랜잭션 ID입니다. 이 ID는 한 인스턴스 내의 모든 데이터베이스에서 고유하지만 모든 서버 인스턴스에서 고유하지는 않습니다.|  
|NAME|**nvarchar(32)**|트랜잭션 이름입니다. 트랜잭션이 표시된 경우 표시된 이름이 트랜잭션 이름을 덮어쓰며 이를 대체합니다.|  
|transaction_begin_time|**datetime**|트랜잭션이 시작된 시간입니다.|  
|transaction_type|**int**|트랜잭션 유형입니다.<br /><br /> 1 = 읽기/쓰기 트랜잭션<br /><br /> 2 = 읽기 전용 트랜잭션<br /><br /> 3 = 시스템 트랜잭션<br /><br /> 4 = 분산 트랜잭션|  
|transaction_uow|**uniqueidentifier**|분산 트랜잭션의 트랜잭션 UOW(작업 단위) 식별자입니다. MS DTC에서는 UOW 식별자를 사용하여 분산 트랜잭션 작업을 수행합니다.|  
|transaction_state|**int**|0 = 트랜잭션이 아직 완전히 초기화되지 않았습니다.<br /><br /> 1 = 트랜잭션을 초기화했지만 시작하지 않았습니다.<br /><br /> 2 = 트랜잭션이 활성 상태입니다.<br /><br /> 3 = 트랜잭션을 종료했습니다. 이것은 읽기 전용 트랜잭션에 사용됩니다.<br /><br /> 4 = 분산 트랜잭션에서 커밋 프로세스가 시작되었습니다. 이것은 분산 트랜잭션에만 사용됩니다. 분산 트랜잭션이 여전히 활성 상태지만 더 이상은 처리할 수 없습니다.<br /><br /> 5 = 트랜잭션이 준비된 상태이며 해결을 기다리고 있습니다.<br /><br /> 6 = 트랜잭션을 커밋 했습니다.<br /><br /> 7 = 트랜잭션을 롤백하고 있습니다.<br /><br /> 8 = 트랜잭션이 롤백 되었습니다.|  
|transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_state|**int**|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (최초 릴리스- [현재 릴리스](http://go.microsoft.com/fwlink/p/?LinkId=299659)).<br /><br /> 1 = 활성<br /><br /> 2 = 준비됨<br /><br /> 3 = 커밋됨<br /><br /> 4 = 중단됨<br /><br /> 5 = 복구됨|  
|dtc_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_isolation_level|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|filestream_transaction_id|**varbinary(128)**|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (최초 릴리스- [현재 릴리스](http://go.microsoft.com/fwlink/p/?LinkId=299659)).<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_tran_session_transactions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [sys.dm_tran_database_transactions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


