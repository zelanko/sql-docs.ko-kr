---
title: "default language 서버 구성 옵션 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: default language option
ms.assetid: c08c26d8-5a62-487e-a4ee-4c529e4f9287
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2e75839ae9482c3f5c5ee1baa8607e51b63c048e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-the-default-language-server-configuration-option"></a>default language 서버 구성 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 기본 언어 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **기본 언어** 옵션을 사용하면 새로 만드는 모든 로그인의 기본 언어를 지정할 수 있습니다. 기본 언어를 설정하려면 원하는 언어의 **langid** 값을 지정합니다. **sys.syslanguages** 호환성 뷰를 쿼리하여 **langid** 값을 얻을 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **기본 언어 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [기본 언어 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   로그인의 기본 언어는 CREATE LOGIN 또는 ALTER LOGIN를 사용하여 재정의할 수 있습니다. 세션의 기본 언어는 ODBC(Open Database Connectivity) 또는 OLE DB API를 사용하여 각 세션 단위로 덮어쓰지 않는 한 해당 세션의 로그인 언어입니다. **sys.syslanguages** 에서 정의한 언어 ID(0-32)에만 [기본 언어](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 옵션을 설정할 수 있습니다. 포함된 데이터베이스를 사용할 때는 CREATE DATABASE 또는 ALTER DATABASE를 사용하여 데이터베이스에 대해, 그리고 CREATE USER 또는 ALTER USER를 사용하여 포함된 데이터베이스 사용자에 대해 기본 언어를 설정할 수 있습니다. 포함된 데이터베이스에서 기본 언어를 설정하면 **langid** 값, 언어 이름 또는 **sys.syslanguages**에 나열된 언어 별칭이 허용됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-default-language-option"></a>기본 언어 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **일반 설정** 노드를 클릭합니다.  
  
3.  **사용자의 기본 언어** 목록에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시스템 메시지를 표시하는 데 사용할 언어를 선택합니다.  
  
     기본 언어는 한국어(Korean)입니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-default-language-option"></a>기본 언어 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 `default language` 옵션을 프랑스어(`2`)로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'default language', 2 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 기본 언어 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
