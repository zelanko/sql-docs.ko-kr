---
title: sp_grant_login_to_proxy (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: bdfeab5754a2397c01ace2bb9f822fa168eeef6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72005863"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  프록시에 보안 주체 액세스 권한을 부여합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @login_name = ] 'login_name'`액세스 권한을 부여할 로그인 이름입니다. *Login_name* 은 **nvarchar (256)** 이며 기본값은 NULL입니다. Login_name, ** \@fixed_server_role**또는 ** \@msdb_role** 중 하나를 지정 해야 합니다. 그렇지 않으면 저장 프로시저가 실패 합니다. ** \@**  
  
`[ @fixed_server_role = ] 'fixed_server_role'`에 대 한 액세스 권한을 부여할 고정 서버 역할입니다. *Fixed_server_role* 은 **nvarchar (256)** 이며 기본값은 NULL입니다. Login_name, ** \@fixed_server_role**또는 ** \@msdb_role** 중 하나를 지정 해야 합니다. 그렇지 않으면 저장 프로시저가 실패 합니다. ** \@**  
  
`[ @msdb_role = ] 'msdb_role'`에 대 한 액세스 권한을 부여할 **msdb** 데이터베이스의 데이터베이스 역할입니다. *Msdb_role* 은 **nvarchar (256)** 이며 기본값은 NULL입니다. Login_name, ** \@fixed_server_role**또는 ** \@msdb_role** 중 하나를 지정 해야 합니다. 그렇지 않으면 저장 프로시저가 실패 합니다. ** \@**  
  
`[ @proxy_id = ] id`액세스 권한을 부여할 프록시의 식별자입니다. *Id* 는 **int**이며 기본값은 NULL입니다. Proxy_id 또는 ** \@proxy_name** 중 하나를 지정 해야 합니다. 그렇지 않으면 저장 프로시저가 실패 합니다. ** \@**  
  
`[ @proxy_name = ] 'proxy_name'`액세스 권한을 부여할 프록시의 이름입니다. *Proxy_name* 은 **nvarchar (256)** 이며 기본값은 NULL입니다. Proxy_id 또는 ** \@proxy_name** 중 하나를 지정 해야 합니다. 그렇지 않으면 저장 프로시저가 실패 합니다. ** \@**  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_grant_login_to_proxy** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_grant_login_to_proxy**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로그인 `adventure-works\terrid` 에서 프록시 `Catalog application proxy`를 사용할 수 있도록 합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;로그인 &#40;만들기](../../t-sql/statements/create-login-transact-sql.md)   
 [Transact-sql&#41;sp_add_proxy &#40;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [Transact-sql&#41;sp_revoke_login_from_proxy &#40;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
