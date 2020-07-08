---
title: 확장 저장 프로시저 (Transact-sql)
titleSuffix: SQL Server Stretch Database
ms.custom: seo-dt-2019
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9f1266fb9967dc429160377bcc1b42d227be5222
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052913"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database 확장 저장 프로시저 (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

 이 섹션에서는 Stretch Database와 관련 된 확장 저장 프로시저에 대해 설명 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) 로컬 스트레치 사용 데이터베이스와 원격 Azure 데이터베이스 간의 인증 된 연결을 제거 합니다.

[sys. sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) 복원이 필요한 경우 원격 Azure 데이터베이스의 전체 복원을 보장 하기 위해 SQL Server 준비 테이블에 유지 되는 마이그레이션된 데이터의 시간을 가져옵니다.
  
 [sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 스트레치를 사용 하도록 설정 된 로컬 데이터베이스와 원격 데이터베이스 간의 인증 된 연결을 복원 합니다.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 원격 Azure 테이블에 저장 된 일괄 처리 ID를 사용 하 여 가장 최근에 마이그레이션된 데이터의 스트레치 사용 SQL Server 테이블에 저장 된 일괄 처리 ID를 조정 합니다. 
 
[sys. sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) 원격 Azure 테이블의 열을 스트레치 사용 SQL Server 테이블의 열로 조정 합니다.
 
 [sys. sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) 원격 테이블의 인덱스를 조정 하는 스키마 태스크를 큐에 대기 시킵니다.
 
 [sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 현재 스트레치 사용 데이터베이스 및 해당 테이블에 대 한 쿼리가 로컬 및 원격 데이터 (기본값) 또는 로컬 데이터만 반환할지 여부를 지정 합니다.
 
 [sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) 복원 해야 하는 경우 원격 Azure 데이터베이스를 전체 복원할 수 있도록 SQL Server 준비 테이블에 유지 되는 마이그레이션된 데이터의 시간을 설정 합니다.
 
 [sys. sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) SQL Server에서 원격 Azure 서버로의 연결을 테스트 하 고 데이터 마이그레이션을 방해할 수 있는 문제를 보고 합니다.
 
## <a name="see-also"></a>참고 항목  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
