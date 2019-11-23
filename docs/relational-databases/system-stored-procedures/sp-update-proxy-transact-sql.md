---
title: sp_update_proxy (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ec6c40abd080c86722565762fab3b4f9d30bd0c0
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305310"
---
# <a name="sp_update_proxy-transact-sql"></a>sp_update_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 프록시의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>인수  
변경할 프록시의 프록시 id 번호를 `[ @proxy_id = ] id` 합니다. *Proxy_id* 은 **int**이며 기본값은 NULL입니다.  
  
변경할 프록시의 이름을 `[ @proxy_name = ] 'proxy_name'` 합니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
프록시에 대 한 새 자격 증명의 이름을 `[ @credential_name = ] 'credential_name'` 합니다. *Credential_name* 는 **sysname**이며 기본값은 NULL입니다. *Credential_name* 또는 *credential_id* 를 지정할 수 있습니다.  
  
프록시에 대 한 새 자격 증명의 id 번호를 `[ @credential_id = ] credential_id` 합니다. *Credential_id* 은 **int**이며 기본값은 NULL입니다. *Credential_name* 또는 *credential_id* 를 지정할 수 있습니다.  
  
프록시의 새 이름을 `[ @new_name = ] 'new_name'` 합니다. *New_name* 는 **sysname**이며 기본값은 NULL입니다. 이 프로시저는 제공 된 경우 프록시 이름을 *new_name*로 변경 합니다. 이 인수가 NULL이면 프록시의 이름은 변경되지 않은 상태로 유지됩니다.  
  
`[ @enabled = ] is_enabled`는 프록시가 사용 되는지 여부입니다. *Is_enabled* 플래그는 **tinyint**이며 기본값은 NULL입니다. *Is_enabled* 가 **0**이면 프록시가 사용 되지 않으며 작업 단계에서 사용할 수 없습니다. 이 인수가 NULL이면 프록시의 상태는 변경되지 않은 상태로 유지됩니다.  
  
프록시에 대 한 새 설명을 `[ @description = ] 'description'` 합니다. *설명은* **nvarchar (512)** 이며 기본값은 NULL입니다. 이 인수가 NULL이면 프록시에 대한 설명은 변경되지 않은 상태로 유지됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **\@proxy_name** 또는 **\@proxy_id** 를 지정 해야 합니다. 두 인수가 모두 지정될 경우 두 인수는 같은 프록시를 참조해야 합니다. 그렇지 않으면 저장 프로시저가 실패합니다.  
  
 프록시에 대 한 자격 증명을 변경 하려면 **\@credential_name** 또는 **\@credential_id** 를 지정 해야 합니다. 두 인수를 모두 지정하면 두 인수는 같은 자격 증명을 참조해야 합니다. 그렇지 않으면 저장 프로시저가 실패합니다.  
  
 이 프로시저는 프록시를 변경하지만 프록시에 대한 액세스 권한은 변경하지 않습니다. 프록시에 대 한 액세스를 변경 하려면 **sp_grant_login_to_proxy** 및 **sp_revoke_login_from_proxy**를 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 보안 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 프록시 `Catalog application proxy`에 설정된 값을 `0`으로 설정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 에이전트 저장 프로시저 &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server 에이전트 보안  구현](../../ssms/agent/implement-sql-server-agent-security.md)  
 [ &#40;transact-sql&#41;  sp_add_proxy](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
 [ &#40;transact-sql&#41;  sp_delete_proxy](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
 [ &#40;transact-sql&#41;  sp_grant_login_to_proxy](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)  
 [Transact-sql &#40;sp_revoke_login_from_proxy&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
