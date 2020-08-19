---
description: sys. fn_hadr_distributed_ag_replica (Transact-sql)
title: sys. fn_hadr_distributed_ag_replica (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_replica
- sys.fn_hadr_distributed_ag_replica_TSQL
- fn_hadr_distributed_ag_replica
- fn_hadr_distributed_ag_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_replica
ms.assetid: a1e5f9cb-c350-4bb4-a04f-7394f6f25d62
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6b7dc6aacf18415b11f5a32e464a57fbbadadc07
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427775"
---
# <a name="sysfn_hadr_distributed_ag_replica-transact-sql"></a>sys. fn_hadr_distributed_ag_replica (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  분산 된 가용성 그룹의 복제본을 로컬 가용성 그룹에 매핑하는 데 사용 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_hadr_distributed_ag_replica( lag_Id, replica_id )  
```  
  
## <a name="arguments"></a>인수  
 '*lag_Id*'  
 분산 가용성 그룹의 식별자입니다. *lag_Id* 은 **uniqueidentifier**형식입니다.  
  
 '*replica_id*'  
 분산 가용성 그룹에 있는 복제본의 식별자입니다. *replica_id* 은 **uniqueidentifier**형식입니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
 다음 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|로컬 가용성 그룹의 고유 식별자 (GUID)입니다.|  
  
## <a name="examples"></a>예제  
  
### <a name="using-sysfn_hadr_distributed_ag_replica"></a>Sys. fn_hadr_distributed_ag_replica 사용  
 다음 예에서는 지정 된 분산 가용성 그룹 및 복제본과 연결 된 로컬 가용성 그룹 식별자가 포함 된 테이블을 반환 합니다.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @replicaId uniqueidentifier = 'D5517513-04A8-FD82-14C6-E684EC913935'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_replica(@lagId, @replicaId)  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 함수 &#40;Transact-sql&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [분산 가용성 그룹 &#40;AlwaysOn 가용성 그룹&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)  
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
