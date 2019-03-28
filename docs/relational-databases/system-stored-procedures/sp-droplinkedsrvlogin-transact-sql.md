---
title: sp_droplinkedsrvlogin (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 505e75dfab9ea4e2ba44d8ef12f0ba5c7eecbde2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533515"
---
# <a name="spdroplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되고 있는 로컬 서버의 로그인과 연결된 서버의 로그인 간의 기존 매핑을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>인수  
`[ @rmtsrvname = ] 'rmtsrvname'` 연결된 된 서버 이름인는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 매핑이 적용 되 합니다. *rmtsrvname* 됩니다 **sysname**, 기본값은 없습니다. *rmtsrvname* 이미 존재 해야 합니다.  
  
`[ @locallogin = ] 'locallogin'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결된 된 서버에 매핑되는 로컬 서버의 로그인 *rmtsrvname*합니다. *locallogin* 됩니다 **sysname**, 기본값은 없습니다. 에 대 한 매핑이 *locallogin* 하 *rmtsrvname* 이미 존재 해야 합니다. 기본 매핑을 만들어 NULL 인 경우 **sp_addlinkedserver**, 로컬 서버의 모든 로그인을 연결 된 서버의 로그인에 매핑되는 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 로컬 서버에 만든 기본 매핑을 사용 되는 경우는 기존에 대 한 매핑을 로그인을 삭제 합니다 **sp_addlinkedserver** 로그인 대신 연결된 된 서버에 연결 되 면 합니다. 기본 매핑을 변경 하려면 **sp_addlinkedsrvlogin**합니다.  
  
 기본 매핑을 삭제 하는 경우 명시적으로 지정 된 연결된 된 서버에 로그인 매핑을 사용 하 여 로그인만 **sp_addlinkedsrvlogin**, 연결 된 서버에 액세스할 수 있습니다.  
  
 **sp_droplinkedsrvlogin** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>1. 기존 사용자에 대한 로그인 매핑 제거  
 다음 예에서는 연결된 서버 `Mary`에 대한 로컬 서버의 로그인 `Accounts`의 매핑을 제거합니다. 따라서 로그인 `Mary`가 기본 로그인 매핑을 사용합니다.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>2. 기본 로그인 매핑 제거  
 다음 예에서는 원래 `sp_addlinkedserver`를 실행하여 연결된 서버 `Accounts`에 작성된 기본 로그인 매핑을 제거합니다.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
