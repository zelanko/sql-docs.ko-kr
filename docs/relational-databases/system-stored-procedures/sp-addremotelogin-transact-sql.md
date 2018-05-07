---
title: sp_addremotelogin (Transact SQL) | Microsoft Docs
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
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ec988334611350fdf736b69100b27d79d5374342
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로컬 서버에 새 원격 로그인 ID를 추가합니다. 이렇게 하면 원격 서버에서 원격 프로시저 호출을 연결 및 실행할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 대신 연결된 서버 및 연결된 서버의 저장 프로시저를 사용하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 원격 로그인을 적용할 원격 서버의 이름입니다. *remoteserver* 은 **sysname**, 기본값은 없습니다. 경우에 *remoteserver* 지정 된 모든 사용자에 게 *remoteserver* 로컬 서버에 동일한 이름의 기존 로그인에 매핑됩니다. 서버는 로컬 서버에서 인식할 수 있어야 합니다. 이 특성은 sp_addserver를 사용 하 여 추가 합니다. 때 사용자에 게 *remoteserver* 실행 하는 로컬 서버에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 저장된 프로시저를 실행 하려면 해당 로그인에 일치 하는 로컬 로그인으로 연결 *remoteserver* . *remoteserver* 원격 프로시저 호출을 시작 하는 서버입니다.  
  
 [ @loginame **=** ] **'***로그인***'**  
 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 사용자의 로그인 ID입니다. *login*은 **sysname**이며 기본값은 NULL입니다. *로그인*의 로컬 인스턴스에 이미 있어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 경우 *로그인* 지정 된 모든 사용자에 게 *remoteserver* 특정 로컬 로그인에 매핑됩니다. 때 사용자에 게 *remoteserver* 의 로컬 인스턴스에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결로 원격 저장된 프로시저를 실행 하려면 *로그인*합니다.  
  
 [ @remotename **=** ] **'***remote_name***'**  
 원격 서버에 있는 사용자의 로그인 ID입니다. *remote_name* 은 **sysname**, 기본값은 NULL입니다. *remote_name* 에 존재 해야 *remoteserver*합니다. 경우 *remote_name* 지정 된 특정 사용자 *remote_name* 에 매핑된 *로그인* 로컬 서버에 있습니다. 때 *remote_name* 에 *remoteserver* 의 로컬 인스턴스에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결로 원격 저장된 프로시저를 실행 하려면 *로그인*합니다. 로그인 ID *remote_name* 원격 서버의 로그인 ID와 달라도 *로그인*합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 분산된 쿼리를 실행 하려면 sp_addlinkedsrvlogin을 사용 합니다.  
  
 sp_addremotelogin은 사용자 정의 트랜잭션 내에서는 사용할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 Sysadmin 및 securityadmin 고정 서버 역할의 구성원만 sp_addremotelogin를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-mapping-one-to-one"></a>1. 일 대 일 매핑  
 다음 예에서는 `ACCOUNTS` 원격 서버와 로컬 서버의 사용자 로그인이 동일한 경우에 로컬 이름에 원격 이름을 매핑합니다.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>2. 다 대 일 매핑  
 다음 예에서는 `ACCOUNTS` 원격 서버의 모든 사용자를 `Albert`라는 로컬 로그인 ID에 매핑하는 항목을 작성합니다.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>3. 명시적인 일 대 일 매핑 사용  
 다음 예에서는 `Chris` 원격 서버에 있는 `ACCOUNTS`라는 원격 사용자의 원격 로그인을 `salesmgr`라는 로컬 사용자에 매핑합니다.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver& #40; Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
