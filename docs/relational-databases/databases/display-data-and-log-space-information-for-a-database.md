---
title: 데이터베이스의 데이터 및 로그 공간 정보 표시
ms.custom: seo-lt-2019
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], space
- status information [SQL Server], space
- displaying space information
- disk space [SQL Server], displaying
- databases [SQL Server], space used
- viewing space information
- space allocation [SQL Server], displaying
- data space [SQL Server]
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 289f48e7163afd70d072962e5e35355522c4b95e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055227"
---
# <a name="display-data-and-log-space-information-for-a-database"></a>데이터베이스의 데이터 및 로그 공간 정보 표시
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 데이터베이스에 대한 데이터와 로그 공간 정보를 표시하는 방법에 대해 설명합니다.  

  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 **sp_spaceused** 를 실행할 수 있는 사용 권한은 **public** 역할에 부여됩니다. **db_owner** 고정 데이터베이스 역할의 멤버만 **\@updateusage** 매개 변수를 지정할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-display-data-and-log-space-information-for-a-database"></a>데이터베이스의 데이터 및 로그 공간 정보를 표시하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **보고서**, **표준 보고서**를 차례로 가리킨 다음 **디스크 사용량**을 클릭합니다.  

##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-using-sp_spaceused"></a>sp_spaceused를 사용하여 데이터베이스에 대한 데이터 및 로그 공간 정보를 표시하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 시스템 저장 프로시저를 사용하여 `Vendor` 테이블 및 해당 인덱스에 대한 디스크 공간 정보를 보고합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-querying-sysdatabase_files"></a>sys.database_files를 쿼리하여 데이터베이스에 대한 데이터 및 로그 공간 정보를 표시하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 카탈로그 뷰를 쿼리하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 데이터 및 로그 파일에 대한 특정 정보를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [데이터베이스에 데이터 또는 로그 파일 추가](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [데이터베이스에서 데이터 또는 로그 파일 삭제](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)  
  
  
