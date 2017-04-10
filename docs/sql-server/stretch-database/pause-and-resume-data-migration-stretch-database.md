---
title: "데이터 마이그레이션 일시 중지 및 다시 시작(스트레치 데이터베이스) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/14/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스트레치 데이터베이스, 일시 중지 및 다시 시작"
  - "스트레치 데이터베이스 일시 중지"
  - "스트레치 데이터베이스 다시 시작"
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# 데이터 마이그레이션 일시 중지 및 다시 시작(스트레치 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Azure로의 데이터 마이그레이션을 일시 중지하거나 다시 시작하려면 SQL Server Management Studio에서 **스트레치** 를 선택한 다음 데이터 마이그레이션을 일시 중지하려면 **일시 중지** 를 선택하고 데이터 마이그레이션을 다시 시작하려면 **다시 시작** 을 선택합니다. Transact-SQL을 사용하여 데이터 마이그레이션을 일시 중지하거나 다시 시작할 수도 있습니다.  
  
 로컬 서버의 문제를 해결하거나 사용 가능한 네트워크 대역폭을 최대화하려는 경우 개별 테이블에서 데이터 마이그레이션을 일시 중지합니다.  

## 데이터 마이그레이션 일시 중지  
  
### SQL Server Management Studio를 사용하여 데이터 마이그레이션 일시 중지  
  
1.  SQL Server Management Studio의 개체 탐색기에서 데이터 마이그레이션을 일시 중지할 스트레치 사용 데이터베이스를 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **스트레치**를 선택한 다음 **일시 중지**를 선택합니다.  
  
### Transact-SQL을 사용하여 데이터 마이그레이션 일시 중지  
 다음 명령을 실행합니다.  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## 데이터 마이그레이션 다시 시작  
  
### SQL Server Management Studio를 사용하여 데이터 마이그레이션 다시 시작  
  
1.  SQL Server Management Studio의 개체 탐색기에서 데이터 마이그레이션을 다시 시작할 스트레치 사용 데이터베이스를 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **스트레치**를 선택한 다음 **다시 시작**을 선택합니다.  
  
### Transact-SQL을 사용하여 데이터 마이그레이션 다시 시작  
 다음 명령을 실행합니다.  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## 마이그레이션이 활성 상태인지 또는 일시 중지 상태인지 확인

### SQL Server Management Studio를 사용하여 마이그레이션이 활성 상태인지 또는 일시 중지 상태인지 확인
SQL Server Management Studio에서 **스트레치 데이터베이스 모니터**를 열고 **마이그레이션 상태** 열의 값을 확인합니다. 자세한 내용은 [데이터 마이그레이션 모니터링 및 문제 해결](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)을 참조하세요.

### Transact-SQL을 사용하여 마이그레이션이 활성 상태인지 또는 일시 중지 상태인지 확인
카탈로그 뷰 **sys.remote_data_archive_tables** 및 **is_migration_paused** 열을 쿼리합니다. 자세한 내용은 [sys.remote_data_archive_tables](sys.remote_data_archive_tables%20\(Transact-SQL\).md)를 참조하세요.

## 참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[데이터 마이그레이션 모니터링 및 문제 해결](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  