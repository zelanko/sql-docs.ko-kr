---
title: sys.fn_hadr_distributed_ag_database_replica (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 029292526c3714bbfb532301d314cab0d4797590
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysfnhadrdistributedagdatabasereplica-transact-sql"></a>sys.fn_hadr_distributed_ag_database_replica (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  분산형된 가용성 그룹의 데이터베이스에에서 데이터베이스의 로컬 가용성 그룹에 매핑하는 데.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>인수  
 '*lag_Id*'  
 분산형된 가용성 그룹의 식별자가입니다. *lag_Id* 형식이 **uniqueidentifier**합니다.  
  
 '*database_id*'  
 분산형된 가용성 그룹에 있는 데이터베이스의 식별자가입니다. *database_id* 형식이 **uniqueidentifier**합니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 다음 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|로컬 가용성 그룹에서 데이터베이스 ID입니다.|  
  
## <a name="examples"></a>예  
  
### <a name="using-sysfnhadrdistributedagdatabasereplica"></a>Sys.fn_hadr_distributed_ag_database_replica를 사용 하 여  
 다음 예제에서는 분산형된 가용성 그룹에 있는 데이터베이스 ID에 전달합니다. 로컬 가용성 그룹에 연결 된 데이터베이스 ID를 가진 테이블을 반환 합니다.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 함수 &#40;Transact SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [가용성 그룹을 분산 &#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;입니다. TRANSACT-SQL &#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
