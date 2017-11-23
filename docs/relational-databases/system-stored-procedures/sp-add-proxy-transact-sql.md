---
title: sp_add_proxy (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40c2684a017c7b6da34bb945499b04bbff5bc5f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 추가합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
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
 [  **@proxy_name** =] **'***proxy_name***'**  
 만들 프록시의 이름입니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다. 경우는 *proxy_name* NULL 또는 빈 문자열인 경우에 기본 프록시 이름은 *user_name* 제공 합니다.  
  
 [  **@enabled**  =] *is_enabled*  
 프록시 활성화 여부를 지정합니다. *is_enabled* 플래그는 **tinyint**, 기본값은 1입니다. 때 *is_enabled* 은 **0**, 프록시는 사용 되지 않으며 작업 단계에서 사용할 수 없습니다.  
  
 [  **@description** =] **'***설명***'**  
 프록시에 대한 설명입니다. 설명은 **nvarchar (512)**, 기본값은 NULL입니다. 설명을 통해 프록시를 문서화할 수 있으며 그렇지 않을 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 사용되지 않습니다. 그러므로 이 인수는 선택 사항입니다.  
  
 [  **@credential_name**  =] **'***credential_name***'**  
 프록시에 대한 자격 증명의 이름입니다. *credential_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *credential_name* 또는 *credential_id* 지정 해야 합니다.  
  
 [  **@credential_id**  =] *credential_id*  
 프록시에 대한 자격 증명의 ID입니다. *credential_id* 은 **int**, 기본값은 NULL입니다. 어느 *credential_name* 또는 *credential_id* 지정 해야 합니다.  
  
 [  **@proxy_id** =] *id* 출력  
 프록시를 성공적으로 만든 경우 프록시에 할당되는 프록시 ID입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 이 저장된 프로시저를 실행 해야 합니다는 **msdb** 데이터베이스입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하위 시스템 이외의 하위 시스템과 연관된 작업 단계의 보안을 관리합니다. 각 프록시는 보안 자격 증명에 해당됩니다. 프록시에서 원하는 수만큼의 하위 시스템에 액세스할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 보안 역할에서이 프로시저를 실행할 수 있습니다.  
  
 멤버는 **sysadmin** 고정된 보안 역할 모든 프록시를 사용 하는 작업 단계를 만들 수 있습니다. 저장된 프로시저를 사용 하 여 [sp_grant_login_to_proxy &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) 프록시에 다른 로그인 액세스 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 자격 증명 `CatalogApplicationCredential`에 대한 프록시를 만듭니다. 이 코드는 자격 증명이 이미 있는 것으로 가정합니다. 자격 증명에 대 한 자세한 내용은 참조 하세요. [CREATE credential&#40; Transact SQL &#41; ](../../t-sql/statements/create-credential-transact-sql.md).  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
