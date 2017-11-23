---
title: sp_grant_login_to_proxy (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1d3fb0ea64fc6e6545c5eb5754853d667ff4110
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spgrantlogintoproxy-transact-sql"></a>sp_grant_login_to_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  프록시에 보안 주체 액세스 권한을 부여합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>인수  
 [  **@login_name**  =] **'***login_name***'**  
 액세스 권한을 부여할 로그인 이름입니다. *login_name* 은 **nvarchar (256)**, 기본값은 NULL입니다. 중 하나  **@login_name** ,  **@fixed_server_role** , 또는  **@msdb_role**  지정 해야 합니다 또는 저장된 프로시저가 실패 합니다.  
  
 [  **@fixed_server_role** =] **'***fixed_server_role***'**  
 액세스 권한을 부여할 고정 서버 역할입니다. *fixed_server_role* 은 **nvarchar (256)**, 기본값은 NULL입니다. 중 하나  **@login_name** ,  **@fixed_server_role** , 또는  **@msdb_role**  지정 해야 합니다 또는 저장된 프로시저가 실패 합니다.  
  
 [  **@msdb_role** =] '*msdb_role*'  
 데이터베이스 역할에는 **msdb** 데이터베이스에 대 한 액세스 권한을 부여할 수 있습니다. *msdb_role* 은 **nvarchar (256)**, 기본값은 NULL입니다. 중 하나  **@login_name** ,  **@fixed_server_role** , 또는  **@msdb_role**  지정 해야 합니다 또는 저장된 프로시저가 실패 합니다.  
  
 [  **@proxy_id** =] *id*  
 액세스 권한을 부여할 프록시의 식별자입니다. *id* 은 **int**, 기본값은 NULL입니다. 중 하나  **@proxy_id**  또는  **@proxy_name**  지정 해야 합니다 또는 저장된 프로시저가 실패 합니다.  
  
 [  **@proxy_name** =] **'***proxy_name***'**  
 액세스 권한을 부여하려는 프록시 이름입니다. *proxy_name* 은 **nvarchar (256)**, 기본값은 NULL입니다. 중 하나  **@proxy_id**  또는  **@proxy_name**  지정 해야 합니다 또는 저장된 프로시저가 실패 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_grant_login_to_proxy** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 실행 될 수 있습니다 **sp_grant_login_to_proxy**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 로그인 `adventure-works\terrid` 프록시 `Catalog application proxy`합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
