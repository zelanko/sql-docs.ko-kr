---
title: sys.remote_data_archive_tables (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3633612e6aa674a5cd7513c6a84ce1d77ca46a4d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689193"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>카탈로그 뷰-Stretch Database sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  로컬 스트레치 사용 테이블에서 데이터를 저장 하는 각 원격 테이블에 대해 하나의 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|로컬 스트레치 사용 테이블의 개체 ID입니다.|  
|**remote_database_id**|**int**|자동으로 생성 된 로컬 식별자 원격 데이터베이스의 합니다.|  
|**remote_table_name**|**sysname**|로컬 스트레치 사용 테이블에 해당 하는 원격 데이터베이스에서 테이블의 이름입니다.|  
|**filter_predicate**|**nvarchar(max)**|마이그레이션할 테이블의 행 식별 하는 경우 필터 조건자를 합니다. 값이 null이면 전체 테이블을 마이그레이션할 수 있습니다.<br /><br /> 자세한 내용은 참조 하세요. [테이블에 대해 Stretch Database 사용 하도록 설정](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 하 고 [필터 조건자를 사용 하 여 마이그레이션할 행 선택](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)합니다.|  
|**migration_direction**|**tinyint**|데이터를 현재 마이그레이션 중인 방향입니다. 사용 가능한 값은 다음과 같습니다.<br/>1 (아웃 바운드)<br/>2 (인바운드)|  
|**migration_direction_desc**|**nvarchar(60)**|데이터를 현재 마이그레이션 중인 방향 설명입니다. 사용 가능한 값은 다음과 같습니다.<br/>아웃 바운드 (1)<br/>인바운드 (2)|  
|**is_migration_paused**|**bit**|마이그레이션이 현재 일시 중지 여부를 나타냅니다.|  
|**is_reconciled**|**bit**| 원격 테이블 및 SQL Server 테이블에 동기화 여부를 나타냅니다.<br/><br/>경우 값 **is_reconciled** 가 1 (true), 원격 테이블 및 SQL Server 테이블은 동기화 및 원격 데이터를 포함 하는 쿼리를 실행할 수 있습니다.<br/><br/>경우 값 **is_reconciled** 0(false) 이면 원격 테이블 및 SQL Server 테이블에서 동기화 됩니다. 최근에 마이그레이션된 행 다시 마이그레이션할 수 있어야 합니다. 이 원격 Azure 데이터베이스를 복원 하거나 원격 테이블에서 수동으로 행을 삭제 하면 발생 합니다. 테이블을 조정 될 때까지 원격 데이터를 포함 하는 쿼리를 실행할 수 없습니다. 테이블을 조정 하려는 실행 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)합니다. |  
  
## <a name="see-also"></a>관련 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

