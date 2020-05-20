---
title: sp_helprole (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprole_TSQL
- sp_helprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprole
ms.assetid: b023103f-ccf3-44e2-b418-4be9bdd49f4a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 674da069c1c47c9e577327e9482add64353de881
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832632"
---
# <a name="sp_helprole-transact-sql"></a>sp_helprole(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스의 역할에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helprole [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'`현재 데이터베이스에 있는 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 NULL입니다. 현재 데이터베이스에 *역할이* 있어야 합니다. *Role* 을 지정 하지 않으면 현재 데이터베이스의 모든 역할에 대 한 정보가 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**RoleName**|**sysname**|현재 데이터베이스의 역할 이름입니다.|  
|**RoleId**|**smallint**|**RoleName**의 ID입니다.|  
|**IsAppRole**|**int**|0 = **RoleName** 가 응용 프로그램 역할이 아닙니다.<br /><br /> 1 = **RoleName** 는 응용 프로그램 역할입니다.|  
  
## <a name="remarks"></a>설명  
 역할과 연결 된 사용 권한을 보려면 **sp_helprotect**를 사용 합니다. 데이터베이스 역할의 멤버를 보려면 **sp_helprolemember**를 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 쿼리는 현재 데이터베이스의 모든 역할을 반환합니다.  
  
```  
EXEC sp_helprole  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [서버 수준 역할](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Transact-sql&#41;sp_addapprole &#40;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [Transact-sql&#41;sp_addrole &#40;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [Transact-sql&#41;sp_droprole &#40;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [Transact-sql&#41;sp_helprolemember &#40;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Transact-sql&#41;sp_helpsrvrolemember &#40;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
