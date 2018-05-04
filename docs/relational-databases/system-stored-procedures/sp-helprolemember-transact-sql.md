---
title: sp_helprolemember (Transact SQL) | Microsoft Docs
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
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 32f524ebffe83bca1e21a4c0a50967951454c676
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelprolemember-transact-sql"></a>sp_helprolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 있는 역할의 직접 멤버에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@rolename =** ] **'** *역할* **'**  
 현재 데이터베이스에 있는 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 NULL입니다. *역할* 현재 데이터베이스에 존재 해야 합니다. 경우 *역할* 를 지정 하지 않으면 현재 데이터베이스에서 하나 이상의 멤버를 포함 하는 모든 역할이 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|현재 데이터베이스의 역할 이름입니다.|  
|**MemberName**|**sysname**|멤버 이름 **DbRole 합니다.**|  
|**MemberSID**|**varbinary(85)**|보안 식별자 **MemberName 합니다.**|  
  
## <a name="remarks"></a>주의  
 데이터베이스에 있는 경우 중첩 된 역할이 **MemberName** 역할의 이름일 수 있습니다. **sp_helprolemember** 중첩 된 역할을 통해 얻은 멤버 자격이 표시 되지 않습니다. 예를 들어, User1이 Role1의 멤버이고 Role1이 Role2의 멤버인 경우 `EXEC sp_helprolemember 'Role2'`에서는 Role1을 반환하고 Role1의 멤버는 반환하지 않습니다(이 예제에서는 User1). 중첩 된 멤버 자격을 반환 하려면 실행 해야 **sp_helprolemember** 중첩 된 각 역할에 대해 반복적으로 합니다.  
  
 사용 하 여 **sp_helpsrvrolemember** 고정된 서버 역할의 멤버를 표시 합니다.  
  
 사용 하 여 [IS_ROLEMEMBER &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/is-rolemember-transact-sql.md) 지정 된 사용자 역할 구성원 자격을 확인 합니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Sales` 역할의 멤버를 표시합니다.  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember& #40; Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
