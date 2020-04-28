---
title: sys. remote_data_archive_tables (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 65e42e6303b467abd38ddadb6be0c0d0fece46e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68018195"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_tables"></a>Stretch Database 카탈로그 뷰-sys. remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스트레치 사용 로컬 테이블의 데이터를 저장 하는 각 원격 테이블에 대해 하나의 행을 포함 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|스트레치 사용 로컬 테이블의 개체 ID입니다.|  
|**remote_database_id**|**int**|원격 데이터베이스의 자동 생성 된 로컬 식별자입니다.|  
|**remote_table_name**|**sysname**|스트레치 사용 로컬 테이블에 해당 하는 원격 데이터베이스의 테이블 이름입니다.|  
|**filter_predicate**|**nvarchar(max)**|마이그레이션할 테이블의 행을 식별 하는 필터 조건자 (있는 경우)입니다. 값이 null이면 전체 테이블을 마이그레이션할 수 있습니다.<br /><br /> 자세한 내용은 [테이블에 대 한 Stretch Database 사용](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 및 [필터 조건자를 사용 하 여 마이그레이션할 행 선택](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조 하세요.|  
|**migration_direction**|**tinyint**|데이터를 현재 마이그레이션하는 방향입니다. 사용 가능한 값은 다음과 같습니다.<br/>1 (아웃 바운드)<br/>2 (인바운드)|  
|**migration_direction_desc**|**nvarchar(60)**|데이터를 현재 마이그레이션하는 방향에 대 한 설명입니다. 사용 가능한 값은 다음과 같습니다.<br/>아웃 바운드 (1)<br/>인바운드 (2)|  
|**is_migration_paused**|**bit**|마이그레이션이 현재 일시 중지 되었는지 여부를 나타냅니다.|  
|**is_reconciled**|**bit**| 원격 테이블과 SQL Server 테이블이 동기화 되어 있는지 여부를 나타냅니다.<br/><br/>**Is_reconciled** 값이 1 (true) 이면 원격 테이블과 SQL Server 테이블이 동기화 된 것 이며 원격 데이터를 포함 하는 쿼리를 실행할 수 있습니다.<br/><br/>**Is_reconciled** 값이 0 (false) 이면 원격 테이블과 SQL Server 테이블이 동기화 되지 않습니다. 최근 마이그레이션된 행을 다시 마이그레이션해야 합니다. 이는 원격 Azure 데이터베이스를 복원 하거나 원격 테이블에서 수동으로 행을 삭제할 때 발생 합니다. 테이블을 조정할 때 까지는 원격 데이터를 포함 하는 쿼리를 실행할 수 없습니다. 테이블을 조정 하려면 [sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)를 실행 합니다. |  
  
## <a name="see-also"></a>참고 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

