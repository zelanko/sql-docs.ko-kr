---
description: 데이터베이스 이름 바꾸기
title: 데이터베이스 이름 바꾸기 | Microsoft 문서
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b81e565875074e3ba3fc08dd85f27b9c077ebb08
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92005512"
---
# <a name="rename-a-database"></a>데이터베이스 이름 바꾸기

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 사용자 정의 데이터베이스 또는 Azure SQL Database의 이름을 바꾸는 방법을 설명합니다. 데이터베이스 이름에는 식별자 규칙에서 허용하는 모든 문자를 사용할 수 있습니다.  
  
## <a name="in-this-topic"></a>항목 내용
  
- 시작하기 전에  
  
     [제한 사항](#limitations-and-restrictions)  
  
     [보안](#security)  
  
- 데이터베이스의 이름을 바꾸려면:  
  
     [SQL Server Management Studio](#rename-a-database-using-sql-server-management-studio)  
  
     [Transact-SQL](#rename-a-database-using-transact-sql)  
  
- **Follow Up:**  [After renaming a database](#backup-after-renaming-a-database)  

> [!NOTE]
> Azure Synapse Analytics 또는 병렬 데이터 웨어하우스에서 데이터베이스의 이름을 바꾸려면 [RENAME(Transact-SQL)](../../t-sql/statements/rename-transact-sql.md) 문을 사용합니다.
  
## <a name="before-you-begin"></a>시작하기 전에
  
### <a name="limitations-and-restrictions"></a>제한 사항  
  
- 시스템 데이터베이스 이름은 바꿀 수 없습니다.
- 다른 사용자가 데이터베이스에 액세스하는 동안에는 데이터베이스 이름을 바꿀 수 없습니다. 
  - SQL Server에서는 단일 사용자 모드로 데이터베이스를 설정하여 열려 있는 모든 연결을 닫을 수 있습니다. 자세한 내용은 [단일 사용자 모드로 데이터베이스 설정](../../relational-databases/databases/set-a-database-to-single-user-mode.md)을 참조하세요.
  - Azure SQL Database에서는 이름을 바꿀 데이터베이스에 연결된 사용자가 없는지 확인해야 합니다.
  
### <a name="security"></a>보안  
  
#### <a name="permissions"></a>사용 권한

데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
## <a name="rename-a-database-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 데이터베이스 이름 바꾸기

다음 단계를 수행하면 SQL Server Management Studio를 사용하여 SQL Server 또는 Azure SQL Database의 이름을 바꿀 수 있습니다.

  
1. **개체 탐색기** 에서 SQL 인스턴스에 연결합니다.  
  
2. 데이터베이스에 대한 열린 연결이 없는지 확인하세요. SQL Server를 사용하는 경우 [데이터베이스를 단일 사용자 모드로 설정](../../relational-databases/databases/set-a-database-to-single-user-mode.md)하여 열려 있는 모든 연결을 닫고 데이터베이스 이름을 변경하는 동안 다른 사용자가 연결하지 못하도록 할 수 있습니다.  
  
3. 개체 탐색기에서 **데이터베이스** 를 확장하고, 이름을 바꿀 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음, **이름 바꾸기** 를 클릭합니다.  
  
4. 새 데이터베이스 이름을 입력하고 **확인** 을 클릭합니다.  
  
5. 경우에 따라 데이터베이스가 기본 데이터베이스인 경우 [이름을 바꾼 후 기본 데이터베이스 다시 설정](#reset-your-default-database-after-rename)을 참조하세요.

## <a name="rename-a-database-using-transact-sql"></a>Transact-SQL을 사용하여 데이터베이스 이름 변경하기  
  
### <a name="to-rename-a-sql-server-database-by-placing-it-in-single-user-mode"></a>SQL Server 데이터베이스를 단일 사용자 모드로 전환하여 이름을 바꾸려면

데이터베이스를 단일 사용자 모드로 설정하는 단계를 포함해 다음 단계를 수행하여 SQL Server Management Studio에서 T-SQL을 사용하여 SQL Server 데이터베이스의 이름을 바꿉니다. 그런 다음, 데이터베이스를 다시 다중 사용자 모드로 변경합니다.
  
1. 인스턴스의 `master` 데이터베이스에 연결합니다.  
2. 쿼리 창을 엽니다.  
3. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 `MyTestDatabase` 데이터베이스의 이름을 `MyTestDatabaseCopy`로 변경합니다.
  
   ```sql
   USE master;  
   GO  
   ALTER DATABASE MyTestDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   GO
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   GO  
   ALTER DATABASE MyTestDatabaseCopy SET MULTI_USER
   GO
   ```  

4. 경우에 따라 데이터베이스가 기본 데이터베이스인 경우 [이름을 바꾼 후 기본 데이터베이스 다시 설정](#reset-your-default-database-after-rename)을 참조하세요.

### <a name="to-rename-an-azure-sql-database-database"></a>Azure SQL Database 데이터베이스의 이름을 바꾸려면

다음 단계를 수행하여 SQL Server Management Studio에서 T-SQL을 사용하여 Azure SQL Database의 이름을 바꿉니다.
  
1. 인스턴스의 `master` 데이터베이스에 연결합니다.  
2. 쿼리 창을 엽니다.
3. 데이터베이스를 사용 중인 사용자가 없는지 확인합니다.
4. 다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 다음 예에서는 `MyTestDatabase` 데이터베이스의 이름을 `MyTestDatabaseCopy`로 변경합니다.
  
   ```sql
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   ```  

## <a name="backup-after-renaming-a-database"></a>데이터베이스의 이름을 바꾼 후 백업  

SQL Server에서 데이터베이스의 이름을 바꾼 후 `master` 데이터베이스를 백업합니다. Azure SQL Database에서는 백업이 자동으로 발생하므로 수동으로 백업할 필요가 없습니다.  
  
## <a name="reset-your-default-database-after-rename"></a>이름을 바꾼 후 기본 데이터베이스 다시 설정

이름을 바꿀 데이터베이스가 기본 데이터베이스로 설정되어 있으면 다음 명령을 사용하여 기본값을 이름이 바뀐 데이터베이스로 다시 설정합니다.


```sql
USE [master]
GO
ALTER LOGIN [your-login] WITH DEFAULT_DATABASE=[new-database-name]
GO
```


## <a name="see-also"></a>참고 항목

- [ALTER DATABASE(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)
- [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)  
