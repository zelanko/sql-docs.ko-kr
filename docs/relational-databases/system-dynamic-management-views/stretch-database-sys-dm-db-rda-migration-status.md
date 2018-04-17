---
title: sys.dm_db_rda_migration_status (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2dd2c4a1ab5595f47ce10f720d1e7159e3347bcf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>스트레치 데이터베이스-sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  로컬 인스턴스에서 각 스트레치 사용 테이블에서 마이그레이션된 데이터의 각 일괄 처리에 대 한 하나의 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 일괄 처리의 시작 시간과 종료 시간으로 식별 됩니다.  
  
 **sys.dm_db_rda_migration_status** 범위는 현재 데이터베이스 컨텍스트를 지정 합니다. 스트레치 사용 테이블 마이그레이션 상태를 확인 하려는 데이터베이스 컨텍스트에서 있는지 확인 합니다.  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 출력 **sys.dm_db_rda_migration_status** 200 개의 행으로 제한 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|행 마이그레이션된 테이블의 ID입니다.|  
|**database_id**|**int**|행 마이그레이션된 데이터베이스의 ID입니다.|  
|**migrated_rows**|**bigint**|행 수가이 일괄 처리에서 마이그레이션.|  
|**start_time_utc**|**datetime**|일괄 처리가 시작 된 UTC 시간입니다.|  
|**end_time_utc**|**datetime**|일괄 처리가 완료 된 UTC 시간입니다.|  
|**error_number**|**int**|일괄 처리에 실패 하면;에 발생 한 오류의 오류 번호 그렇지 않으면 null입니다.|  
|**error_severity**|**int**|일괄 처리에 실패 하면;에 발생 한 오류의 심각도 그렇지 않으면 null입니다.|  
|**error_state**|**int**|일괄 처리에 실패 하면;에 발생 한 오류의 상태 그렇지 않으면 null입니다.<br /><br /> **error_state** 조건 또는 오류가 발생 하는 위치를 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
