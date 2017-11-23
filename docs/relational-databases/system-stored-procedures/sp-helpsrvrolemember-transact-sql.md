---
title: sp_helpsrvrolemember (Transact SQL) | Microsoft Docs
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
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c12855ba98604bed198cf365b7da68f458aba12
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고정 서버 역할의 멤버에 대한 정보를 반환합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@srvrolename =** ] **'***역할***'**  
 고정 서버 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 NULL입니다. 경우 *역할*를 지정 하지 않으면 모든 고정된 서버 역할에 대 한 정보를 포함 하는 결과 집합입니다.  
  
 *역할* 다음 값 중 하나일 수 있습니다.  
  
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
|MemberName|**sysname**|서버 역할의 멤버의 이름|  
|MemberSID|**varbinary(85)**|MemberName의 보안 식별자|  
  
## <a name="remarks"></a>주의  
 Sp_helprolemember를 사용 하 여 데이터베이스 역할의 멤버를 표시 합니다.  
  
 모든 로그인은 public의 멤버입니다. sp_helpsrvrolemember 때문에 public 역할을 인식 하지 않으므로 내부적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] public 역할로 구현 하지 않습니다.  
  
 추가 서버 역할에서 제거 된 멤버 참조 또는 [ALTER SERVER role&#40; Transact SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 sp_helpsrvrolemember는 사용자 정의 서버 역할을 인수로 사용 하지 않습니다. 사용자 정의 서버 역할의 멤버를 확인 하려면의 예제를 참조 [ALTER SERVER role&#40; Transact SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sysadmin` 고정 서버 역할의 멤버를 나열합니다.  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_helprole&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
