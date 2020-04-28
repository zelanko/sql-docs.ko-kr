---
title: sp_helpsrvrolemember (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
author: stevestein
ms.author: sstein
ms.openlocfilehash: ba1cbbfb95dafaa99a33d95b1d92a9e6e5f4e9a2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68010757"
---
# <a name="sp_helpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 서버 역할의 멤버에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @srvrolename = ] 'role'`고정 서버 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 NULL입니다. *Role*을 지정 하지 않으면 모든 고정 서버 역할에 대 한 정보가 결과 집합에 포함 됩니다.  
  
 *role* 은 다음 값 중 하나일 수 있습니다.  
  
|고정 서버 역할|Description|  
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
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|서버 역할의 이름입니다.|  
|MemberName|**sysname**|ServerRole 멤버의 이름입니다.|  
|MemberSID|**varbinary(85)**|MemberName의 보안 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 데이터베이스 역할의 멤버를 표시하려면 sp_helprolemember를 사용합니다.  
  
 모든 로그인은 public의 멤버입니다. 는 내부적으로 public을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할로 구현 하지 않기 때문에 sp_helpsrvrolemember은 public 역할을 인식 하지 못합니다.  
  
 서버 역할에서 멤버를 추가 하거나 제거 하려면 [ALTER SERVER ROLE &#40;transact-sql&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)를 참조 하세요.  
  
 sp_helpsrvrolemember는 사용자 정의 서버 역할을 인수로 사용 하지 않습니다. 사용자 정의 서버 역할의 멤버를 확인 하려면 [ALTER SERVER role &#40;transact-sql&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)의 예제를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sysadmin` 고정 서버 역할의 멤버를 나열합니다.  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_helprole &#40;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [Transact-sql&#41;sp_helprolemember &#40;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
