---
title: sp_helpsrvrole (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
author: stevestein
ms.author: sstein
ms.openlocfilehash: a632e6923ab3127a363650c63533fa548d1acc12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006122"
---
# <a name="sphelpsrvrole-transact-sql"></a>sp_helpsrvrole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 서버 역할의 목록을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @srvrolename = ] 'role'` 고정된 서버 역할의 이름이입니다. *역할* 됩니다 **sysname**, 기본값은 NULL입니다. *역할* 다음 값 중 하나일 수 있습니다.  
  
|고정 서버 역할|설명|  
|-----------------------|-----------------|  
|sysadmin|시스템 관리자입니다.|  
|securityadmin|보안 관리자입니다.|  
|serveradmin|서버 관리자입니다.|  
|setupadmin|설치 관리자입니다.|  
|processadmin|프로세스 관리자입니다.|  
|diskadmin|디스크 관리자입니다.|  
|dbcreator|데이터베이스 작성자입니다.|  
|bulkadmin|BULK INSERT 문을 실행할 수 있습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|서버 역할의 이름입니다.|  
|설명|**sysname**|서버 역할의 설명|  
  
## <a name="remarks"></a>설명  
 고정 서버 역할은 서버 수준에서 정의되며 서버 수준의 특정 관리 작업을 수행할 사용 권한을 갖습니다. 고정 서버 역할은 추가, 제거, 변경할 수 없습니다.  
  
 추가 하거나 서버 역할에서 제거 된 멤버를 참조 하십시오 [ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)합니다.  
  
 모든 로그인은 public의 멤버입니다. sp_helpsrvrole 때문에 public 역할을 인식 하지 못하는, 내부적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공용 역할로 구현 하지 않습니다.  
  
 sp_helpsrvrole 인수로 사용자 정의 서버 역할을 사용 하지 않습니다. 사용자 정의 서버 역할을 나열 하려면의 예제를 참조 [ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-the-fixed-server-roles"></a>A. 고정 서버 역할 나열  
 다음 쿼리는 고정 서버 역할 목록을 반환합니다.  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>2\. 고정 및 사용자 정의 서버 역할 나열  
 다음 쿼리는 고정 및 사용자 정의 서버 역할 목록을 둘 다 반환합니다.  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>3\. 고정 서버 역할의 설명 반환  
 다음 쿼리는 `diskadmin` 고정 서버 역할의 이름과 설명을 반환합니다.  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [sp_addsrvrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
