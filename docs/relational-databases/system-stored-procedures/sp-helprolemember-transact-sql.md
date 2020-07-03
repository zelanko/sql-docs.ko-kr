---
title: sp_helprolemember (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a6007f595555843c783718fecfb6adbe2d74103c
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891635"
---
# <a name="sp_helprolemember-transact-sql"></a>sp_helprolemember(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에 있는 역할의 직접 멤버에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] ' role '`현재 데이터베이스에 있는 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 NULL입니다. 현재 데이터베이스에 *역할이* 있어야 합니다. *Role* 을 지정 하지 않으면 현재 데이터베이스의 멤버가 하나 이상 포함 된 모든 역할이 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|현재 데이터베이스의 역할 이름입니다.|  
|**MemberName**|**sysname**|DbRole의 멤버 이름입니다 **.**|  
|**MemberSID**|**varbinary(85)**|MemberName의 보안 식별자 **입니다.**|  
  
## <a name="remarks"></a>설명  
 데이터베이스에 중첩 된 역할이 포함 된 경우 **MemberName** 는 역할의 이름일 수 있습니다. **sp_helprolemember** 에는 중첩 된 역할을 통해 얻은 멤버 자격이 표시 되지 않습니다. 예를 들어, User1이 Role1의 멤버이고 Role1이 Role2의 멤버인 경우 `EXEC sp_helprolemember 'Role2'`에서는 Role1을 반환하고 Role1의 멤버는 반환하지 않습니다(이 예제에서는 User1). 중첩 된 멤버 자격을 반환 하려면 중첩 된 각 역할에 대해 **sp_helprolemember** 를 반복적으로 실행 해야 합니다.  
  
 **Sp_helpsrvrolemember** 를 사용 하 여 고정 서버 역할의 멤버를 표시할 수 있습니다.  
  
 [Transact-sql&#41;&#40;IS_ROLEMEMBER](../../t-sql/functions/is-rolemember-transact-sql.md) 을 사용 하 여 지정 된 사용자에 대 한 역할 멤버 자격을 확인 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Sales` 역할의 멤버를 표시합니다.  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addrolemember &#40;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_droprolemember &#40;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [Transact-sql&#41;sp_helprole &#40;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [Transact-sql&#41;sp_helpsrvrolemember &#40;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
