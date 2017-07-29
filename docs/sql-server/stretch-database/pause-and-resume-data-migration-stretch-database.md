---
title: "데이터 마이그레이션 일시 중지 및 다시 시작(Stretch Database) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, pausing and resuming
- pausing Stretch Database
- resuming Stretch Database
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 0fef9c7f912cb824b3f1fcf8653a82fa99a35561
ms.openlocfilehash: a291fd543d572fc621e7b59e968e7ca69d79552e
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="pause-and-resume-data-migration-stretch-database"></a>데이터 마이그레이션 일시 중지 및 다시 시작(Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Azure로의 데이터 마이그레이션을 일시 중지하거나 다시 시작하려면 SQL Server Management Studio에서 **스트레치** 를 선택한 다음 데이터 마이그레이션을 일시 중지하려면 **일시 중지** 를 선택하고 데이터 마이그레이션을 다시 시작하려면 **다시 시작** 을 선택합니다. Transact-SQL을 사용하여 데이터 마이그레이션을 일시 중지하거나 다시 시작할 수도 있습니다.  
  
 로컬 서버의 문제를 해결하거나 사용 가능한 네트워크 대역폭을 최대화하려는 경우 개별 테이블에서 데이터 마이그레이션을 일시 중지합니다.  

## <a name="pause-data-migration"></a>데이터 마이그레이션 일시 중지  
  
### <a name="use-sql-server-management-studio-to-pause-data-migration"></a>SQL Server Management Studio를 사용하여 데이터 마이그레이션 일시 중지  
  
1.  SQL Server Management Studio의 개체 탐색기에서 데이터 마이그레이션을 일시 중지할 스트레치 사용 데이터베이스를 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **스트레치**를 선택한 다음 **일시 중지**를 선택합니다.  
  
### <a name="use-transact-sql-to-pause-data-migration"></a>Transact-SQL을 사용하여 데이터 마이그레이션 일시 중지  
 다음 명령을 실행합니다.  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## <a name="resume-data-migration"></a>데이터 마이그레이션 다시 시작  
  
### <a name="use-sql-server-management-studio-to-resume-data-migration"></a>SQL Server Management Studio를 사용하여 데이터 마이그레이션 다시 시작  
  
1.  SQL Server Management Studio의 개체 탐색기에서 데이터 마이그레이션을 다시 시작할 스트레치 사용 데이터베이스를 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **스트레치**를 선택한 다음 **다시 시작**을 선택합니다.  
  
### <a name="use-transact-sql-to-resume-data-migration"></a>Transact-SQL을 사용하여 데이터 마이그레이션 다시 시작  
 다음 명령을 실행합니다.  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## <a name="check-whether-migration-is-active-or-paused"></a>마이그레이션이 활성 상태인지 또는 일시 중지 상태인지 확인

### <a name="use-sql-server-management-studio-to-check-whether-migration-is-active-or-paused"></a>SQL Server Management Studio를 사용하여 마이그레이션이 활성 상태인지 또는 일시 중지 상태인지 확인
SQL Server Management Studio에서 **Stretch Database 모니터** 를 열고 **마이그레이션 상태** 열의 값을 확인합니다. 자세한 내용은 [데이터 마이그레이션 모니터링 및 문제 해결](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)을 참조하세요.

### <a name="use-transact-sql-to-check-whether-migration-is-active-or-paused"></a>Transact-SQL을 사용하여 마이그레이션이 활성 상태인지 또는 일시 중지 상태인지 확인
카탈로그 뷰 **sys.remote_data_archive_tables** 및 **is_migration_paused** 열을 쿼리합니다. 자세한 내용은 [sys.remote_data_archive_tables](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)를 참조하세요.

## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[데이터 마이그레이션 모니터링 및 문제 해결](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  

