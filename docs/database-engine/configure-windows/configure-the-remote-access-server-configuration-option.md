---
title: "remote access 서버 구성 옵션 구성 | Microsoft Docs"
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote servers [SQL Server], stored procedure execution
ms.assetid: f5de748d-1c55-4714-9661-38fe62e5095f
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 5736d22a7ce8bf9c1269677c6d5df02b1b1282d8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/11/2017

---
# <a name="configure-the-remote-access-server-configuration-option"></a>remote access 서버 구성 옵션 구성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 항목은 "원격 액세스" 기능에 대한 내용입니다. 이 구성 옵션은 잘 알려지지 않고 사용되지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통신 기능이며 사용되지 않을 가능성이 높습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하는 데 문제가 있어 이 페이지에 도달한 경우 대신, 다음 항목 중 하나를 참조하세요.  
  
-   [자습서: 데이터베이스 엔진 시작](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
-   [SQL Server로 로그인](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
-   [시스템 관리자가 잠겨 있는 경우 SQL Server에 연결](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
-   [등록된 서버에 연결&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/connect-to-a-registered-server-sql-server-management-studio.md)  
  
-   [SQL Server Management Studio에서 SQL Server 구성 요소로 연결](http://msdn.microsoft.com/library/5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e)  
  
-   [sqlcmd를 사용하여 데이터베이스 엔진에 연결](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)  
  
-   [SQL Server 데이터베이스 엔진에 대한 연결 문제를 해결하는 방법](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
 프로그래머는 다음 항목에 관심이 가질 수 있습니다.  
  
-   [방법: ASP.NET 2.0에서 SQL 인증을 사용하여 SQL Server에 연결](https://msdn.microsoft.com/library/ff648340.aspx)  
  
-   [SQL Server 인스턴스에 연결](https://msdn.microsoft.com/library/ms162132.aspx)  
  
-   [방법: SQL Server 데이터베이스에 대한 연결 만들기](https://msdn.microsoft.com/library/s4yys16a.aspx)  
  
 **이 항목의 본문은 여기에서 시작됩니다.**  
  
 이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] remote access [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **remote access** 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되고 있는 로컬 또는 원격 서버에서 저장 프로시저 실행을 제어할 수 있습니다. 이 옵션의 기본값은 1이며 원격 서버에서 로컬 저장 프로시저를 실행하거나 로컬 서버에서 원격 저장 프로시저를 실행할 권한을 부여합니다. 원격 서버에서 로컬 저장 프로시저를 실행할 수 없거나 로컬 서버에서 원격 저장 프로시저를 실행할 수 없게 하려면 옵션을 0으로 설정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 대신 사용하세요. <br />원격 액세스가 사용하도록 설정되지 않으면 네 부분으로 이루어진 이름 지정(예: `EXEC SQL01.TestDB.dbo.proc_test;` 구문)을 사용할 경우 연결된 서버에서 저장 프로시저를 실행하지 못합니다. 대신 `EXECUTE ... AT` 구문(예: `EXEC(N'TestDB.dbo.proc_test') AT [SQL01];`)을 사용하세요.
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **remote access 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [remote access 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   **remote access** 옵션은 [sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)를 사용하여 추가한 서버에만 적용되며 이전 버전과의 호환성을 위해 포함되었습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-remote-access-option"></a>remote access 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **연결** 노드를 클릭합니다.  
  
3.  **원격 서버 연결**에서 **이 서버에 대한 원격 연결 허용** 확인란을 선택하거나 선택을 취소합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-remote-access-option"></a>remote access 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 `remote access` 옵션의 값을 `0`(으)로 설정하는 방법을 보여 줍니다.  
  
```tsql  
EXEC sp_configure 'remote access', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: remote access 옵션을 구성한 후  
 이 설정은 SQL Server를 다시 시작할 때까지 적용되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

