---
title: sp_migrate_user_to_contained (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7761a5602e1700949b8ae072342cd65927a24b9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843981"
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑된 사용자를 암호를 포함하는 포함된 데이터베이스 사용자로 변환합니다. 포함된 데이터베이스에서는 이 프로시저를 사용하여 데이터베이스가 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 종속성을 제거하십시오. **sp_migrate_user_to_contained** 원래에서 사용자를 분리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에는 포함된 된 데이터베이스에 대 한 암호, 기본 언어 등의 설정을 별도로 관리할 수 있습니다. **sp_migrate_user_to_contained** 포함된 된 데이터베이스의 다른 인스턴스로 이동 하기 전에 사용할 수는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 현재 종속성을 제거 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 로그인 합니다.  
  
 **참고** 이 프로시저는 포함 된 데이터베이스 에서만 사용 됩니다. 자세한 내용은 [Contained Databases](../../relational-databases/databases/contained-databases.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>인수  
 [ **@username =** ] **N'***사용자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인에 매핑된 현재 포함된 데이터베이스의 사용자 이름입니다. 값이 **sysname**, 기본값은 **NULL**합니다.  
  
 [ **@rename =** ] **N'***copy_login_name***'** | **N'***keep_name***'**  
 사용 하 여 로그인 기반 데이터베이스 사용자 로그인 이름 대신 다른 사용자 이름이 *keep_name* 마이그레이션하는 동안 데이터베이스 사용자 이름을 유지 합니다. 사용 하 여 *copy_login_name* 사용자 대신 로그인의 이름으로 새 포함 된 데이터베이스 사용자를 만들려고 합니다. 로그인 기반 데이터베이스 사용자의 사용자 이름이 로그인 이름과 같으면 두 옵션 모두 이름을 변경하지 않고 포함된 데이터베이스 사용자를 만듭니다.  
  
 [ **@disablelogin =** ] **N'***disable_login***'** | **N'***do_not_disable_login***'**  
 *disable_login* master 데이터베이스의 로그인을 사용 하지 않도록 설정 합니다. 로그인은 사용 하지 않도록 설정 하는 경우에 연결 하려면 연결으로 포함 된 데이터베이스 이름을 제공 해야 합니다 **초기 카탈로그** 연결 문자열의 일부로.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_migrate_user_to_contained** 속성 또는 로그인의 권한을 관계 없이 암호를 사용 하 여 포함된 된 데이터베이스 사용자를 만듭니다. 로그인 비활성화 된 경우 또는 사용자가 거부 한 경우 프로시저가 성공할 수 있습니다 예를 들어 합니다 **연결** 데이터베이스에 대 한 사용 권한.  
  
 **sp_migrate_user_to_contained** 는 다음 제한 사항이 있습니다.  
  
-   사용자 이름은 아직 데이터베이스에 없는 이름이어야 합니다.  
  
-   dbo, guest 등의 기본 제공 사용자는 변환할 수 없습니다.  
  
-   사용자 지정할 수 없습니다는 **EXECUTE AS** 서명 된 저장된 프로시저의 절.  
  
-   사용자를 포함 하는 저장된 프로시저를 소유할 수 없습니다는 **EXECUTE AS OWNER** 절.  
  
-   **sp_migrate_user_to_contained** 시스템 데이터베이스에서 사용할 수 없습니다.  
  
## <a name="security"></a>보안  
 사용자를 마이그레이션할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 모든 관리자 로그인을 해제하거나 삭제하지 않도록 주의하십시오. 로그인을 모두 삭제 되는 경우 참조 [SQL Server 시스템 관리자는 잠겨 있는 경우에 Connect](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)합니다.  
  
 경우는 **BUILTIN\Administrators** 로그인이 있는 관리자가 사용 하 여 해당 응용 프로그램을 시작 하 여 연결할 수는 **관리자 권한으로 실행** 옵션입니다.  
  
### <a name="permissions"></a>사용 권한  
 **CONTROL SERVER** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-migrating-a-single-user"></a>1. 단일 사용자 마이그레이션  
 다음 예에서는 `Barry`라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 암호를 포함하는 포함된 데이터베이스 사용자로 마이그레이션합니다. 이 예에서는 사용자 이름이 변경되지 않도록 유지하고 로그인을 사용 가능한 상태로 유지합니다.  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>2. 로그인을 포함하는 모든 데이터베이스 사용자를 로그인을 포함하지 않는 포함된 데이터베이스 사용자로 마이그레이션  
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
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)  
  
  
