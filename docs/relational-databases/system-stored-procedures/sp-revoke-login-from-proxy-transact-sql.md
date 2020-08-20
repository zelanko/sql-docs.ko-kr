---
description: sp_revoke_login_from_proxy(Transact-SQL)
title: sp_revoke_login_from_proxy (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 39857bce8c0fc50c1773709d70e7e477b669b282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473861"
---
# <a name="sp_revoke_login_from_proxy-transact-sql"></a>sp_revoke_login_from_proxy(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  보안 주체의 프록시 액세스 권한을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]액세스 권한을 제거할 로그인, 서버 역할 또는 **msdb** 데이터베이스 역할의 이름입니다. *name* 은 **nvarchar (256)** 이며 기본값은 없습니다.  
  
`[ @proxy_id = ] id` 액세스 권한을 제거할 프록시의 id입니다. *Id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *Id* 는 **int**이며 기본값은 NULL입니다.  
  
`[ @proxy_name = ] 'proxy_name'` 액세스 권한을 제거할 프록시의 이름입니다. *Id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 이 프록시를 참조하는 로그인이 소유한 작업은 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 로그인 `terrid`가 프록시 `Catalog application proxy`에 액세스할 수 있는 권한을 취소합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_grant_login_to_proxy &#40;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [Transact-sql&#41;sp_help_proxy &#40;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
