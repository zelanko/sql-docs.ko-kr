---
title: 분리된 사용자 문제 해결(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38a33b34b64cf285e94f66c547b2309b8daf1ae8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167643"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>분리된 사용자 문제 해결(SQL Server)
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그인하려면 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 사용자에게 있어야 합니다. 이 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 사용자 연결이 허용되는지 여부를 확인하는 인증 프로세스에서 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 인스턴스에서 로그인에 표시 되는 **sys.server_principals** 카탈로그 뷰 및 **sys.syslogins** 호환성 보기.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑된 데이터베이스 사용자를 사용하여 개별 데이터베이스에 액세스합니다. 이 규칙에는 두 가지 예외가 있습니다.  
  
-   게스트 계정  
  
     게스트 계정은 데이터베이스에서 사용 가능한 경우 데이터베이스 사용자에 매핑되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 게스트 사용자로 데이터베이스에 액세스할 수 있도록 하는 계정입니다.  
  
-   Microsoft Windows 그룹 멤버 자격  
  
     Windows 사용자로부터 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 해당 Windows 사용자가 Windows 그룹의 멤버인 동시에 데이터베이스의 사용자인 경우 데이터베이스에 액세스할 수 있습니다.  
  
 데이터베이스 사용자로의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 매핑에 대한 정보는 데이터베이스 내에 저장됩니다. 데이터베이스 사용자 이름과 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 SID가 여기에 포함됩니다. 이 데이터베이스 사용자의 사용 권한은 데이터베이스에서 권한 부여에 사용됩니다.  
  
 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 인스턴스에서 정의되지 않았거나 잘못 정의되어 있는 데이터베이스 사용자는 이 인스턴스에 로그인할 수 없습니다. 이러한 사용자는 해당 서버 인스턴스에 있는 데이터베이스의 *분리된 사용자* 라고 합니다. 데이터베이스 사용자는 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 삭제되면 분리될 수 있습니다. 데이터베이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스에 복원되거나 연결된 후에도 데이터베이스 사용자가 분리될 수 있습니다. 데이터베이스 사용자가 새 서버 인스턴스에 없는 SID로 매핑되는 경우 사용자가 분리될 수 있습니다.  
  
> [!NOTE]  
>  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 나타나는 없기 해당 데이터베이스 사용자를 하지 않는 한 데이터베이스 로그인에 액세스할 수 없습니다 **게스트** 해당 데이터베이스에서 사용 하도록 설정 됩니다. 데이터베이스 사용자 계정을 만드는 방법에 대 한 자세한 내용은 [사용자 만들기 &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)합니다.  
  
## <a name="to-detect-orphaned-users"></a>분리된 사용자를 검색하려면  
 분리된 사용자를 검색하려면 다음 Transact-SQL 문을 실행합니다.  
  
```  
USE <database_name>;  
GO;   
sp_change_users_login @Action='Report';  
GO;  
```  
  
 현재 데이터베이스에 있으며 어떤 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에도 연결되지 않은 사용자와 이에 해당되는 SID(보안 ID)가 나열됩니다. 자세한 내용은 [sp_change_users_login &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)합니다.  
  
> [!NOTE]  
>  **sp_change_users_login** 와 함께 사용할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows에서 생성 된 로그인입니다.  
  
## <a name="to-resolve-an-orphaned-user"></a>분리된 사용자를 확인하려면  
 분리된 사용자를 확인하려면 다음 절차를 수행합니다.  
  
1.  다음 명령을 다시 지정 하는 서버 로그인 계정을 연결 *< login_name >* 에서 지정한 데이터베이스 사용자를 사용 하 여 *< database_user >* 합니다.  
  
    ```  
    USE <database_name>;  
    GO  
    sp_change_users_login @Action='update_one', @UserNamePattern='<database_user>', @LoginName='<login_name>';  
    GO  
  
    ```  
  
     자세한 내용은 [sp_change_users_login &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)합니다.  
  
2.  앞 단계에서 코드를 실행한 다음 사용자는 데이터베이스에 액세스할 수 있습니다. 사용자 한 다음 암호를 변경할 수의 *< login_name >* 를 사용 하 여 로그인 합니다 **sp_password** 저장 프로시저를 다음과 같이:  
  
    ```  
    USE master   
    GO  
    sp_password @old=NULL, @new='password', @loginame='<login_name>';  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  ALTER ANY LOGIN 사용 권한이 있는 로그인으로만 다른 사용자의 로그인 암호를 변경할 수 있습니다. 그러나 **sysadmin** 역할의 멤버만 **sysadmin** 역할 멤버의 암호를 수정할 수 있습니다.  
  
    > [!NOTE]  
    >  **sp_password** 에 사용할 수 없습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정입니다. Windows 네트워크 계정을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 사용자는 Windows에 의해 인증되므로 암호는 Windows에서만 변경할 수 있습니다.  
  
     자세한 내용은 [sp_password &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [sp_change_users_login&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)   
 [sp_addlogin&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_grantlogin&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-grantlogin-transact-sql)   
 [sp_password&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)   
 [sys.sysusers&#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)   
 [sys.syslogins &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)  
  
  
