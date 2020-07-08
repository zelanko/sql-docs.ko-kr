---
title: sys. dm_db_rda_migration_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 1e383b01ce40dbb03f5134bf5374b9b39bc2a99e
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053491"
---
# <a name="stretch-database---sysdm_db_rda_migration_status"></a>Stretch Database dm_db_rda_migration_status
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  로컬 인스턴스의 각 스트레치 사용 테이블에서 마이그레이션된 데이터의 각 일괄 처리에 대해 하나의 행을 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 일괄 처리는 시작 시간과 종료 시간으로 식별 됩니다.  
  
 **dm_db_rda_migration_status** 은 현재 데이터베이스 컨텍스트로 범위가 지정 됩니다. 마이그레이션 상태를 보려는 스트레치 사용 테이블의 데이터베이스 컨텍스트에 있는지 확인 합니다.  
  
 에서는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] **dm_db_rda_migration_status** 의 출력이 200 개 행으로 제한 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|행이 마이그레이션된 테이블의 ID입니다.|  
|**database_id**|**int**|행이 마이그레이션되는 데이터베이스의 ID입니다.|  
|**migrated_rows**|**bigint**|이 일괄 처리로 마이그레이션된 행의 수입니다.|  
|**start_time_utc**|**datetime**|일괄 처리가 시작 된 UTC 시간입니다.|  
|**end_time_utc**|**datetime**|일괄 처리가 완료 된 UTC 시간입니다.|  
|**error_number**|**int**|일괄 처리가 실패 한 경우 발생 한 오류의 오류 번호입니다. 그렇지 않으면 null입니다.|  
|**error_severity**|**int**|일괄 처리가 실패 하는 경우 발생 한 오류의 심각도입니다. 그렇지 않으면 null입니다.|  
|**error_state**|**int**|일괄 처리에 실패 한 경우 발생 한 오류의 상태입니다. 그렇지 않으면 null입니다.<br /><br /> **Error_state** 은 오류가 발생 한 조건 또는 위치를 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
