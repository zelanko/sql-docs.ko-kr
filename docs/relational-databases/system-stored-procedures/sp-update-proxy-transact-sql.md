---
title: sp_update_proxy (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 402bdaa7ad89675cfaefec39cc8e36312e78d359
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy(Transact-SQL)
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
 [ **@proxy_id**= ] *id*  
 변경할 프록시의 프록시 ID입니다. *proxy_id* 은 **int**, 기본값은 NULL입니다.  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 변경할 프록시의 이름입니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ **@credential_name** =] **'***credential_name***'**  
 프록시에 대한 새 자격 증명의 이름입니다. *credential_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *credential_name* 또는 *credential_id* 지정할 수 있습니다.  
  
 [ **@credential_id** = ] *credential_id*  
 프록시에 대한 새 자격 증명의 ID입니다. *credential_id* 은 **int**, 기본값은 NULL입니다. 어느 *credential_name* 또는 *credential_id* 지정할 수 있습니다.  
  
 [ **@new_name**= ] **'***new_name***'**  
 프록시의 새 이름입니다. *new_name* 은 **sysname**, 기본값은 NULL입니다. 프로시저가 변경 프록시의 이름을 제공 하면 *new_name*합니다. 이 인수가 NULL이면 프록시의 이름은 변경되지 않은 상태로 유지됩니다.  
  
 [ **@enabled** =] *is_enabled*  
 프록시 설정 여부입니다. *is_enabled* 플래그는 **tinyint**, 기본값은 NULL입니다. 때 *is_enabled* 은 **0**, 프록시는 사용 되지 않으며 작업 단계에서 사용할 수 없습니다. 이 인수가 NULL이면 프록시의 상태는 변경되지 않은 상태로 유지됩니다.  
  
 [ **@description**= ] **'***description***'**  
 프록시에 대한 새로운 설명입니다. *설명* 은 **nvarchar (512)**, 기본값은 NULL입니다. 이 인수가 NULL이면 프록시에 대한 설명은 변경되지 않은 상태로 유지됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 어느 **@proxy_name** 또는 **@proxy_id** 지정 해야 합니다. 두 인수가 모두 지정될 경우 두 인수는 같은 프록시를 참조해야 합니다. 그렇지 않으면 저장 프로시저가 실패합니다.  
  
 어느 **@credential_name** 또는 **@credential_id** 프록시에 대 한 자격 증명을 변경 하려면 반드시 지정 해야 합니다. 두 인수를 모두 지정하면 두 인수는 같은 자격 증명을 참조해야 합니다. 그렇지 않으면 저장 프로시저가 실패합니다.  
  
 이 프로시저는 프록시를 변경하지만 프록시에 대한 액세스 권한은 변경하지 않습니다. 사용 하 여 프록시에 대 한 액세스를 변경 하려면 **sp_grant_login_to_proxy** 및 **sp_revoke_login_from_proxy**합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 보안 역할에서이 프로시저를 실행할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server 에이전트 보안 구현](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
