---
title: sp_helplinkedsrvlogin (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 32d7d0098c5548666b1d2fc77e11f82c2c3fd5fe
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536855"
---
# <a name="sphelplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  분산 쿼리 및 원격 저장 프로시저에 사용되는 지정한 연결된 서버에 대해 정의된 로그인 매핑 정보를 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @rmtsrvname = ] 'rmtsrvname'` 로그인 매핑이 적용 되는 연결 된 서버의 이름이입니다. *rmtsrvname* 됩니다 **sysname**, 기본값은 NULL입니다. NULL인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 로컬 컴퓨터에서 정의된 모든 연결된 서버에 대해 정의된 로그인 매핑을 모두 반환합니다.  
  
`[ @locallogin = ] 'locallogin'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결된 된 서버에 매핑되는 로컬 서버의 로그인 *rmtsrvname*합니다. *locallogin* 됩니다 **sysname**, 기본값은 NULL입니다. NULL에 관한 모든 로그인 매핑 정의 지정 *rmtsrvname* 반환 됩니다. 그렇지 않은 경우 NULL에 대 한 매핑이 *locallogin* 하 *rmtsrvname* 이미 존재 해야 합니다. *locallogin* 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 사용자입니다. Windows 사용자는 직접적인 방법으로든 또는 액세스 권한이 있는 Windows 그룹의 멤버 자격을 이용한 방법으로든 반드시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 보유해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**연결 된 서버**|**sysname**|연결된 서버 이름입니다.|  
|**로컬 로그인**|**sysname**|매핑이 적용되는 로컬 로그인입니다.|  
|**자체 매핑이**|**smallint**|0 = **로컬 로그인** 매핑됩니다 **Remote Login** 에 연결할 때 **연결 된 서버**합니다.<br /><br /> 1 = **local Login** 에 연결할 때 동일한 로그인 및 암호에 매핑됩니다 **연결 된 서버**합니다.|  
|**원격 로그인**|**sysname**|로그인 이름 **LinkedServer** 에 매핑된 **LocalLogin** 때 **IsSelfMapping** 은 0입니다. 하는 경우 **IsSelfMapping** 가 1 이면 **RemoteLogin** NULL입니다.|  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 로그인 매핑을 삭제 하기 전에 **sp_helplinkedsrvlogin** 관련 된 연결 된 서버를 확인 합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 확인하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>1. 모든 연결된 서버에 관한 모든 로그인 매핑 표시  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 로컬 컴퓨터에서 정의된 모든 연결된 서버에 관한 로그인 매핑을 모두 표시합니다.  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>2. 연결된 서버에 관한 모든 로그인 매핑 표시  
 다음 예에서는 `Sales`라는 연결된 서버에 대해 로컬로 정의된 모든 로그인 매핑을 표시합니다.  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>3. 로컬 로그인에 관한 모든 로그인 매핑 표시  
 다음 예에서는 `Mary`라는 로그인에 대해 로컬로 정의된 모든 로그인 매핑을 표시합니다.  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
