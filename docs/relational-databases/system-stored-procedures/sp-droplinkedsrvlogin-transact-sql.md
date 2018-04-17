---
title: sp_droplinkedsrvlogin (Transact SQL) | Microsoft Docs
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
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f72982ca6d4490bf7d9bc3324d3760da7783752
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
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
 [  **@rmtsrvname =** ] **'***rmtsrvname***'**  
 연결된 된 서버 이름인 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 매핑이 적용 되 합니다. *rmtsrvname* 은 **sysname**, 기본값은 없습니다. *rmtsrvname* 이미 존재 해야 합니다.  
  
 [  **@locallogin =** ] **'***locallogin***'**  
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결된 된 서버에 매핑되는 로컬 서버의 로그인 *rmtsrvname*합니다. *locallogin* 은 **sysname**, 기본값은 없습니다. 에 대 한 매핑을 *locallogin* 를 *rmtsrvname* 이미 존재 해야 합니다. 기본 매핑은 만든 NULL 인 경우 **sp_addlinkedserver**, 로컬 서버의 모든 로그인을 연결 된 서버의 로그인에 매핑되는 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 로컬 서버에에서 만든 기본 매핑을 사용 되는 경우는 기존에 대 한 매핑이 로그인을 삭제, **sp_addlinkedserver** 해당 로그인을 대신 하 여 연결된 된 서버에 연결할 때. 기본 매핑을 변경 하려면 **sp_addlinkedsrvlogin**합니다.  
  
 기본 매핑을 삭제 되 면 명시적으로 지정 된 연결된 된 서버에 로그인 매핑을 사용 하 여 로그인만 **sp_addlinkedsrvlogin**, 연결 된 서버에 액세스할 수 있습니다.  
  
 **sp_droplinkedsrvlogin** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
