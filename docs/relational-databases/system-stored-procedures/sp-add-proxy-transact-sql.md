---
title: sp_add_proxy (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 247c834abfbc47485628702bf4cd87c7662c44a8
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494275"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_name = ] 'proxy_name'` 만들 프록시의 이름입니다. 합니다 *proxy_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 경우는 *proxy_name* 가 NULL 이거나 빈 문자열인 경우 기본 프록시 이름 합니다 *user_name* 제공 합니다.  
  
`[ @enabled = ] is_enabled` 프록시 사용 되는지 여부를 지정 합니다. 합니다 *is_enabled* 플래그가 **tinyint**, 기본값은 1 사용 하 여 합니다. 때 *is_enabled* 됩니다 **0**, 프록시를 사용 하지 않는 및 작업 단계에서 사용할 수 없습니다.  
  
`[ @description = ] 'description'` 프록시의 설명입니다. 설명이 **nvarchar(512)**, 기본값은 NULL입니다. 설명을 통해 프록시를 문서화할 수 있으며 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 사용되지 않습니다. 그러므로 이 인수는 선택 사항입니다.  
  
`[ @credential_name = ] 'credential_name'` 프록시에 대 한 자격 증명의 이름입니다. 합니다 *credential_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 어느 *credential_name* 하거나 *credential_id* 지정 해야 합니다.  
  
`[ @credential_id = ] credential_id` 프록시에 대 한 자격 증명의 id. 합니다 *credential_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 어느 *credential_name* 하거나 *credential_id* 지정 해야 합니다.  
  
`[ @proxy_id = ] id OUTPUT` 성공적으로 생성 된 프록시에 할당 하는 프록시 id.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 이 저장된 프로시저 실행 해야 합니다 **msdb** 데이터베이스입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하위 시스템 이외의 하위 시스템과 연관된 작업 단계의 보안을 관리합니다. 각 프록시는 보안 자격 증명에 해당됩니다. 프록시에서 원하는 수만큼의 하위 시스템에 액세스할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 보안 역할에서이 프로시저를 실행할 수 있습니다.  
  
 멤버는 **sysadmin** 고정된 보안 역할에서 프록시를 사용 하는 작업 단계를 만들 수 있습니다. 저장된 프로시저를 사용 하 여 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) 프록시에 다른 로그인 액세스를 부여 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 자격 증명 `CatalogApplicationCredential`에 대한 프록시를 만듭니다. 이 코드는 자격 증명이 이미 있는 것으로 가정합니다. 자격 증명에 대 한 자세한 내용은 참조 하세요. [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
