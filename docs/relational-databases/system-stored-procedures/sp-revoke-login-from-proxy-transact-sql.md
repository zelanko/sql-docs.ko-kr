---
title: sp_revoke_login_from_proxy (Transact SQL) | Microsoft Docs
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
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f1ed813fc63480831eb5e23b109f11cd5ba556
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sprevokeloginfromproxy-transact-sql"></a>sp_revoke_login_from_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보안 주체의 프록시 액세스 권한을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>인수  
 [ **@name=** ] **'***name***'**  
 이름에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 서버 역할 또는 **msdb** 에 대 한 액세스를 제거할 데이터베이스 역할입니다. *이름* 은 **nvarchar (256)** 이며 기본값은 없습니다.  
  
 [ **@proxy_id=** ] *id*  
 액세스 권한을 제거할 프록시의 ID입니다. 어느 *id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *id* 은 **int**, 기본값은 NULL입니다.  
  
 [ **@proxy_name=** ] **'***proxy_name***'**  
 액세스 권한을 제거할 프록시의 이름입니다. 어느 *id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 이 프록시를 참조하는 로그인이 소유한 작업은 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로그인 `terrid`가 프록시 `Catalog application proxy`에 액세스할 수 있는 권한을 취소합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_help_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
