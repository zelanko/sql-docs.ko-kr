---
title: 부분적으로 포함된 데이터베이스로 마이그레이션 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e535935da5c99668e39ab4f84eb98ccd5bab064
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528685"
---
# <a name="migrate-to-a-partially-contained-database"></a>Migrate to a Partially Contained Database
  이 항목에서는 부분적으로 포함된 데이터베이스 모델 변경을 준비하는 방법에 대해 설명한 다음 마이그레이션 단계를 제공합니다.  
  
 **항목 내용**  
  
-   [데이터베이스 마이그레이션 준비](#prepare)  
  
-   [포함된 데이터베이스 사용](#enable)  
  
-   [데이터베이스를 부분적으로 포함된 데이터베이스로 변환](#convert)  
  
-   [포함된 데이터베이스 사용자로 사용자 마이그레이션](#users)  
  
##  <a name="prepare"></a> 데이터베이스 마이그레이션 준비  
 데이터베이스를 부분적으로 포함된 데이터베이스 모델로 마이그레이션하려고 할 때 다음 항목을 검토합니다.  
  
-   부분적으로 포함된 데이터베이스 모델을 이해해야 합니다. 자세한 내용은 [Contained Databases](contained-databases.md)을 참조하세요.  
  
-   부분적으로 포함된 데이터베이스에서만 발생할 수 있는 위험을 이해해야 합니다. 자세한 내용은 [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md)를 참조하세요.  
  
-   포함된 데이터베이스는 복제, 변경 데이터 캡처 또는 변경 내용 추적 기능을 지원하지 않습니다. 데이터베이스에서 이러한 기능을 사용하지 않는지 확인합니다.  
  
-   부분적으로 포함된 데이터베이스에 대해 수정된 데이터베이스 기능 목록을 검토합니다. 자세한 내용은 [수정된 기능&#40;포함된 데이터베이스&#41;](modified-features-contained-database.md)을 참조하세요.  
  
-   데이터베이스에 포함되지 않은 개체 또는 기능을 찾으려면 [sys.dm_db_uncontained_entities&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql)를 쿼리합니다. 자세한 내용은 다음을 참조하십시오.  
  
-   **database_uncontained_usage** XEvent를 모니터링하여 포함되지 않은 기능이 사용되는 경우를 확인합니다.  
  
##  <a name="enable"></a> 포함된 데이터베이스 사용  
 포함된 데이터베이스를 만들려면 먼저 포함된 데이터베이스가 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에서 사용 가능하도록 설정되어야 합니다.  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>Transact-SQL을 사용하여 포함된 데이터베이스 설정  
 다음 예에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에서 포함된 데이터베이스를 사용 가능하도록 설정합니다.  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>SQL Server Management Studio를 사용하여 포함된 데이터베이스 설정  
 다음 예에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에서 포함된 데이터베이스를 사용 가능하도록 설정합니다.  
  
1.  개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **고급** 페이지의 **포함** 섹션에서 **포함된 데이터베이스 사용** 옵션을 **True**로 설정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> 데이터베이스를 부분적으로 포함된 데이터베이스로 변환  
 **CONTAINMENT** 옵션을 변경하여 데이터베이스를 포함된 데이터베이스로 변환합니다.  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>Transact-SQL을 사용하여 데이터베이스를 부분적으로 포함된 데이터베이스로 변환  
 다음 예에서는 이름이 `Accounting` 인 데이터베이스를 부분적으로 포함된 데이터베이스로 변환합니다.  
  
```sql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>Management Studio를 사용하여 데이터베이스를 부분적으로 포함된 데이터베이스로 변환  
 다음 예에서는 데이터베이스를 부분적으로 포함된 데이터베이스로 변환합니다.  
  
1.  개체 탐색기에서 **데이터베이스**를 확장하고, 변환할 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **옵션** 페이지에서 **포함 유형** 옵션을 **부분**으로 변경합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="users"></a> 포함된 데이터베이스 사용자로 사용자 마이그레이션  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 기반으로 하는 모든 사용자를 암호를 가진 포함된 데이터베이스 사용자로 마이그레이션합니다. 이 예에서는 활성화되지 않은 로그인을 제외합니다. 이 예는 포함된 데이터베이스에서 실행해야 합니다.  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [Contained Databases](contained-databases.md)   
 [sp_migrate_user_to_contained&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql)   
 [sys.dm_db_uncontained_entities&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql)  
  
  
