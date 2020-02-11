---
title: sp_add_proxy (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 4aa4120db7b45cb0b3a7d7a10bb53931b8300d9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088486"
---
# <a name="sp_add_proxy-transact-sql"></a>sp_add_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @proxy_name = ] 'proxy_name'`만들 프록시의 이름입니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다. *PROXY_NAME* NULL 또는 빈 문자열인 경우 프록시 이름은 기본적으로 제공 되는 *user_name* 로 설정 됩니다.  
  
`[ @enabled = ] is_enabled`프록시가 사용 되는지 여부를 지정 합니다. *Is_enabled* 플래그는 **tinyint**이며 기본값은 1입니다. *Is_enabled* 가 **0**이면 프록시가 사용 되지 않으며 작업 단계에서 사용할 수 없습니다.  
  
`[ @description = ] 'description'`프록시에 대 한 설명입니다. 설명은 **nvarchar (512)** 이며 기본값은 NULL입니다. 설명을 통해 프록시를 문서화할 수 있으며 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 사용되지 않습니다. 그러므로 이 인수는 선택 사항입니다.  
  
`[ @credential_name = ] 'credential_name'`프록시에 대 한 자격 증명의 이름입니다. *Credential_name* 는 **sysname**이며 기본값은 NULL입니다. *Credential_name* 또는 *credential_id* 를 지정 해야 합니다.  
  
`[ @credential_id = ] credential_id`프록시에 대 한 자격 증명의 id입니다. *Credential_id* 은 **int**이며 기본값은 NULL입니다. *Credential_name* 또는 *credential_id* 를 지정 해야 합니다.  
  
`[ @proxy_id = ] id OUTPUT`성공적으로 만들어진 경우 프록시에 할당 된 프록시 id 번호입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하위 시스템 이외의 하위 시스템과 연관된 작업 단계의 보안을 관리합니다. 각 프록시는 보안 자격 증명에 해당됩니다. 프록시에서 원하는 수만큼의 하위 시스템에 액세스할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 보안 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
 **Sysadmin** 고정 보안 역할의 멤버는 프록시를 사용 하는 작업 단계를 만들 수 있습니다. 저장 프로시저 [sp_grant_login_to_proxy &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) 사용 하 여 다른 로그인에 프록시에 대 한 액세스 권한을 부여 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 자격 증명 `CatalogApplicationCredential`에 대한 프록시를 만듭니다. 이 코드는 자격 증명이 이미 있는 것으로 가정합니다. 자격 증명에 대 한 자세한 내용은 [CREATE CREDENTIAL &#40;transact-sql&#41;](../../t-sql/statements/create-credential-transact-sql.md)를 참조 하세요.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [Transact-sql&#41;sp_grant_login_to_proxy &#40;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [Transact-sql&#41;sp_revoke_login_from_proxy &#40;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
