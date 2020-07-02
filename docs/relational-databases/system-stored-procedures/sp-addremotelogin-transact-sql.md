---
title: sp_addremotelogin (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b4a3586625fa0a20d59ca0222ea1abbde6a6fef5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716429"
---
# <a name="sp_addremotelogin-transact-sql"></a>sp_addremotelogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  로컬 서버에 새 원격 로그인 ID를 추가합니다. 이렇게 하면 원격 서버에서 원격 프로시저 호출을 연결 및 실행할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 대신 연결된 서버 및 연결된 서버의 저장 프로시저를 사용하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @remoteserver **=** ] **'**_remoteserver_**'**  
 원격 로그인을 적용할 원격 서버의 이름입니다. *remoteserver* 는 **sysname**이며 기본값은 없습니다. *Remoteserver* 만 지정 하면 *remoteserver* 의 모든 사용자가 로컬 서버에 있는 동일한 이름의 기존 로그인에 매핑됩니다. 서버는 로컬 서버에서 인식할 수 있어야 합니다. 서버는 sp_addserver를 사용하여 추가합니다. *Remoteserver* 의 사용자가 원격 저장 프로시저를 실행 하기 위해를 실행 하는 로컬 서버에 연결 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *remoteserver*에서 자체 로그인과 일치 하는 로컬 로그인으로 연결 합니다. *remoteserver* 는 원격 프로시저 호출을 시작 하는 서버입니다.  
  
 [ @loginame **=** ] **'**_로그인_**'**  
 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 사용자의 로그인 ID입니다. *login*은 **sysname**이며 기본값은 NULL입니다. *로그인*은의 로컬 인스턴스에 이미 존재 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *Login* 을 지정 하면 *remoteserver* 의 모든 사용자가 해당 하는 특정 로컬 로그인에 매핑됩니다. *Remoteserver* 의 사용자가의 로컬 인스턴스에 연결 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 저장 프로시저를 실행 하는 경우 *로그인*으로 연결 합니다.  
  
 [ @remotename **=** ] **'**_remote_name_**'**  
 원격 서버에 있는 사용자의 로그인 ID입니다. *remote_name* 는 **sysname**이며 기본값은 NULL입니다. *remoteserver*에 *remote_name* 있어야 합니다. *Remote_name* 지정 하면 특정 사용자 *remote_name* 로컬 서버의 *로그인* 에 매핑됩니다. *Remoteserver* 에 대 한 *remote_name* 의 로컬 인스턴스에 연결 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 저장 프로시저를 실행 하면 *로그인*으로 연결 됩니다. *Remote_name* 의 로그인 id는 원격 서버 *로그인*의 로그인 id와 다를 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 분산 쿼리를 실행하려면 sp_addlinkedsrvlogin을 사용하십시오.  
  
 sp_addremotelogin은 사용자 정의 트랜잭션 내부에서 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 및 securityadmin 고정 서버 역할의 멤버만이 sp_addremotelogin을 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-mapping-one-to-one"></a>A. 일 대 일 매핑  
 다음 예에서는 `ACCOUNTS` 원격 서버와 로컬 서버의 사용자 로그인이 동일한 경우에 로컬 이름에 원격 이름을 매핑합니다.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>B. 다 대 일 매핑  
 다음 예에서는 `ACCOUNTS` 원격 서버의 모든 사용자를 `Albert`라는 로컬 로그인 ID에 매핑하는 항목을 작성합니다.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. 명시적인 일 대 일 매핑 사용  
 다음 예에서는 `Chris` 원격 서버에 있는 `ACCOUNTS`라는 원격 사용자의 원격 로그인을 `salesmgr`라는 로컬 사용자에 매핑합니다.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addlinkedsrvlogin &#40;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Transact-sql&#41;sp_addlogin &#40;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [Transact-sql&#41;sp_addserver &#40;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Transact-sql&#41;sp_dropremotelogin &#40;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Transact-sql&#41;sp_helpremotelogin &#40;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Transact-sql&#41;sp_helpserver &#40;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Transact-sql&#41;sp_remoteoption &#40;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [Transact-sql&#41;sp_revokelogin &#40;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
