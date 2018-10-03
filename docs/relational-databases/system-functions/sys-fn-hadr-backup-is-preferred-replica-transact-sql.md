---
title: sys.fn_hadr_backup_is_preferred_replica (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_backup_is_preferred_replica_TSQL
- sys.fn_hadr_backup_is_preferred_replica
- fn_hadr_backup_is_preferred_replica_TSQL
- fn_hadr_backup_is_preferred_replica
dev_langs:
- TSQL
helpviewer_keywords:
- backup on secondary replicas
- active secondary replicas [SQL Server], backup on secondary replicas
- sys.fn_hadr_backup_is_preferred_replica function
ms.assetid: 61b9be77-e2f6-4da1-b2ae-a62cbe226145
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6bba59d680a9f7ba1595808eed27762670aab97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597668"
---
# <a name="sysfnhadrbackupispreferredreplica--transact-sql"></a>sys.fn_hadr_backup_is_preferred_replica (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  현재 복제본이 기본 백업 복제본인지 확인하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>인수  
 '*dbname*'  
 백업할 데이터베이스의 이름입니다. *dbname* 은 sysname 형식입니다.  
  
## <a name="returns"></a>반환 값  
 현재 인스턴스의 데이터베이스가 기본 복제본에 있으면 1을 반환하고, 그렇지 않으면 0을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 백업 스크립트에서 이 함수를 사용하여 현재 데이터베이스가 백업용 기본 복제본에 있는지 여부를 확인할 수 있습니다. 모든 가용성 복제본에서 스크립트를 실행할 수 있습니다. 이러한 각 작업은 동일한 데이터를 조사하여 실행해야 하는 작업을 확인하므로 예약된 작업 중 하나만이 실제로 백업 단계로 진행됩니다. 예제 코드는 다음과 비슷할 수 있습니다.  
  
```  
If sys.fn_hadr_backup_is_preferred_replica( @dbname ) <> 1   
BEGIN  
-- If this is not the preferred replica, exit (probably without error).  
END  
-- If this is the preferred replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>예  
  
### <a name="a-using-sysfnhadrbackupispreferredreplica"></a>1. sys.fn_hadr_backup_is_preferred_replica 사용  
 다음 예에서는 현재 데이터베이스가 기본 백업 복제본인 경우 1을 반환합니다.  
  
```  
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [Always On 가용성 그룹 함수 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [활성 보조: 보조 복제본에 백업 &#40;Always On 가용성 그룹&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)[Always On 가용성 그룹 카탈로그 뷰 &#40;TRANSACT-SQL    &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
