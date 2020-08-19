---
description: sys. fn_hadr_distributed_ag_database_replica (Transact-sql)
title: sys. fn_hadr_distributed_ag_database_replica (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f54cfdf987474435b452421620246b6432892a36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419507"
---
# <a name="sysfn_hadr_distributed_ag_database_replica-transact-sql"></a>sys. fn_hadr_distributed_ag_database_replica (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  로컬 가용성 그룹의 데이터베이스에 분산 가용성 그룹의 데이터베이스를 매핑하는 데 사용 됩니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>인수  
 '*lag_Id*'  
 분산 가용성 그룹의 식별자입니다. *lag_Id* 은 **uniqueidentifier**형식입니다.  
  
 '*database_id*'  
 분산 된 가용성 그룹에 있는 데이터베이스의 식별자입니다. *database_id* 은 **uniqueidentifier**형식입니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 다음 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|로컬 가용성 그룹에 있는 데이터베이스의 ID입니다.|  
  
## <a name="examples"></a>예제  
  
### <a name="using-sysfn_hadr_distributed_ag_database_replica"></a>Sys. fn_hadr_distributed_ag_database_replica 사용  
 다음 예에서는 분산형 가용성 그룹의 데이터베이스 ID를 전달 합니다. 로컬 가용성 그룹에 연결 된 데이터베이스 ID를 사용 하 여 테이블을 반환 합니다.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;를 사용 하 여 가용성 그룹 함수 Always On &#40;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹 &#40;분산 가용성 그룹&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
