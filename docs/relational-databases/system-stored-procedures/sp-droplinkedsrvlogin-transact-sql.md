---
title: sp_droplinkedsrvlogin (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3f6df8ac0be9a6bfc8798697ec01e7e5a2c8e3d3
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85859843"
---
# <a name="sp_droplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되고 있는 로컬 서버의 로그인과 연결된 서버의 로그인 간의 기존 매핑을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>인수  
`[ @rmtsrvname = ] 'rmtsrvname'`로그인 매핑이 적용 되는 연결 된 서버의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *rmtsrvname* 는 **sysname**이며 기본값은 없습니다. *rmtsrvname* 가 이미 있어야 합니다.  
  
`[ @locallogin = ] 'locallogin'`연결 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 *rmtsrvname*에 대 한 매핑이 있는 로컬 서버의 로그인입니다. *locallogin* 은 **sysname**이며 기본값은 없습니다. *Rmtsrvname* 에 대 한 *locallogin* 에 대 한 매핑이 이미 존재 해야 합니다. NULL 인 경우 로컬 서버의 모든 로그인을 연결 된 서버의 로그인에 매핑하는 **sp_addlinkedserver**에서 만든 기본 매핑이 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 로그인에 대 한 기존 매핑을 삭제 하면 로컬 서버는 해당 로그인을 대신 하 여 연결 된 서버에 연결할 때 **sp_addlinkedserver** 에서 만든 기본 매핑을 사용 합니다. 기본 매핑을 변경 하려면 **sp_addlinkedsrvlogin**을 사용 합니다.  
  
 기본 매핑만 삭제 된 경우에는 **sp_addlinkedsrvlogin**를 사용 하 여 연결 된 서버에 대 한 로그인 매핑이 명시적으로 지정 된 로그인만 연결 된 서버에 액세스할 수 있습니다.  
  
 **sp_droplinkedsrvlogin** 은 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>A. 기존 사용자에 대한 로그인 매핑 제거  
 다음 예에서는 연결된 서버 `Mary`에 대한 로컬 서버의 로그인 `Accounts`의 매핑을 제거합니다. 따라서 로그인 `Mary`가 기본 로그인 매핑을 사용합니다.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. 기본 로그인 매핑 제거  
 다음 예에서는 원래 `sp_addlinkedserver`를 실행하여 연결된 서버 `Accounts`에 작성된 기본 로그인 매핑을 제거합니다.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addlinkedserver &#40;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Transact-sql&#41;sp_addlinkedsrvlogin &#40;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
