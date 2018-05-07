---
title: sp_dropremotelogin (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4565f5a3005a556d24777a220ff020816f01a346
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 로컬 서버에 대해 원격 저장 프로시저를 실행할 때 사용되는 로컬 로그인에 매핑된 원격 로그인을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 대신 연결된 서버 및 연결된 서버의 저장 프로시저를 사용하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@remoteserver =** ] **'***remoteserver***'**  
 제거할 원격 로그인에 매핑된 원격 서버의 이름입니다. *remoteserver* 은 **sysname**, 기본값은 없습니다. *remoteserver* 이미 존재 해야 합니다.  
  
 [ **@loginame =** ] **'***login***'**  
 원격 서버와 연결된 로컬 서버의 선택적 로그인 이름입니다. *login*은 **sysname**이며 기본값은 NULL입니다. *로그인* 지정 된 경우 이미 존재 해야 합니다.  
  
 [  **@remotename =** ] **'***remote_name***'**  
 에 매핑된 원격 로그인의 선택적 이름 *로그인* 원격 서버에서 로그인 할 때입니다. *remote_name* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 경우에 *remoteserver* 지정 된, 로컬 서버에서 해당 원격 서버에 대 한 원격 로그인을 모두 제거 됩니다. 경우 *로그인* 에서 지정 된 모든 원격 로그인 이기도 *remoteserver* 는 특정에 매핑된 로컬 로그인은 로컬 서버에서 제거 됩니다. 경우 *remote_name* 도 지정 되어 해당 원격 사용자에 대 한 원격 로그인만 *remoteserver* 로컬 서버에서 제거 됩니다.  
  
 로컬 서버 사용자를 추가 하려면 사용 하 여 **sp_addlogin**합니다. 사용 하 여 로컬 서버 사용자를 제거 하려면 **sp_droplogin**합니다.  
  
 원격 로그인은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하는 경우에만 필요합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0 이상 버전에서는 연결된 서버의 로그인을 사용합니다. 사용 하 여 **sp_addlinkedsrvlogin** 및 **sp_droplinkedsrvlogin** 추가 하 고 연결 된 서버 로그인을 제거 합니다.  
  
 **sp_dropremotelogin** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **sysadmin** 또는 **securityadmin** 고정 서버 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>1. 원격 서버에 대한 모든 원격 로그인 삭제  
 다음 예에서는 `ACCOUNTS`라는 원격 서버의 항목을 제거하여 로컬 서버의 로그인과 원격 서버의 원격 로그인 간의 모든 매핑을 제거합니다.  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>2. 로그인 매핑 삭제  
 다음 예에서는 `ACCOUNTS` 원격 서버에서 `Albert` 로컬 로그인으로의 원격 로그인 매핑에 사용된 항목을 제거합니다.  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>3. 원격 사용자 삭제  
 다음 예에서는 `Chris` 로컬 로그인에 매핑된 `ACCOUNTS` 원격 서버에서 `salesmgr` 원격 로그인에 대한 로그인을 제거합니다.  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
