---
title: sys.remote_data_archive_tables (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19ae2040d65a7e7c8a36cef8f355e8715283c92d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>스트레치 데이터베이스 카탈로그 뷰-sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  로컬 스트레치 사용 테이블에서 데이터를 저장 하는 각 원격 테이블에 대해 한 행을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|스트레치가 활성화 된 로컬 테이블의 개체 ID입니다.|  
|**remote_database_id**|**int**|자동 생성 된 로컬 데이터베이스의 식별자는 원격 합니다.|  
|**remote_table_name**|**sysname**|로컬 스트레치 사용 테이블에 해당 하는 원격 데이터베이스에 있는 테이블의 이름입니다.|  
|**filter_predicate**|**nvarchar(max)**|있는 경우 필터 조건자를 마이그레이션해야 하는 테이블의 행을 식별 하 합니다. 값이 null이면 전체 테이블을 마이그레이션할 수 있습니다.<br /><br /> 자세한 내용은 참조 하십시오. [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 및 [필터 조건자를 사용 하 여 마이그레이션할 행을 선택](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)합니다.|  
|**migration_direction**|**tinyint**|데이터를 현재 마이그레이션 중인 방향입니다. 사용 가능한 값은 다음 합니다.<br/>1 (아웃 바운드)<br/>2 (인바운드)|  
|**migration_direction_desc**|**nvarchar(60)**|설명에 있는 데이터를 현재 마이그레이션 중인 방향입니다. 사용 가능한 값은 다음 합니다.<br/>아웃 바운드 (1)<br/>인바운드 (2)|  
|**is_migration_paused**|**bit**|마이그레이션이 현재 일시 중지 되어 있는지 여부를 나타냅니다.|  
|**is_reconciled**|**bit**| 원격 테이블 및 SQL Server 테이블 동기화 되었는지 여부를 나타냅니다.<br/><br/>때의 값 **is_reconciled** 가 1 (true), 원격 테이블 및 SQL Server 테이블은 동기화 및 원격 데이터를 포함 하는 쿼리를 실행할 수 있습니다.<br/><br/>때의 값 **is_reconciled** 은 0 (false), 원격 테이블 및 SQL Server 테이블 동기화 되어 있습니다. 최근에 마이그레이션된 행을 다시 마이그레이션할 수 있어야 합니다. 원격 Azure 데이터베이스를 복원 하는 경우 또는 원격 테이블에서 수동으로 행을 삭제 하면 발생 합니다. 테이블을 조정 될 때까지 원격 데이터를 포함 하는 쿼리를 실행할 수 없습니다. 테이블을 조정 하려면 실행 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)합니다. |  
  
## <a name="see-also"></a>관련 항목:  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

