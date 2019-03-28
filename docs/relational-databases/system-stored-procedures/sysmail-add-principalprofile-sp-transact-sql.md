---
title: sysmail_add_principalprofile_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf12b97028d3d98f7d5cc5ab034db95411d913dc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528505"
---
# <a name="sysmailaddprincipalprofilesp-transact-sql"></a>sysmail_add_principalprofile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 프로필을 사용하도록 데이터베이스 사용자 또는 역할의 사용 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @principal_id = ] principal_id` 데이터베이스 사용자 또는 역할의 ID를 **msdb** 데이터베이스 연결에 대 한 합니다. *principal_id* 됩니다 **int**, 기본값은 NULL입니다. 어느 *principal_id* 하거나 *principal_name* 지정 해야 합니다. A *principal_id* 의 **0** 이 프로필은 공개 프로필이 데이터베이스의 모든 보안 주체에 액세스 권한을 부여 합니다.  
  
`[ @principal_name = ] 'principal_name'` 데이터베이스 사용자 또는 역할의 이름을 합니다 **msdb** 데이터베이스 연결에 대 한 합니다. *principal_name* 됩니다 **sysname**, 기본값은 NULL입니다. 어느 *principal_id* 하거나 *principal_name* 지정 해야 합니다. A *principal_name* 의 **'public'** 이 프로필은 공개 프로필이 데이터베이스의 모든 보안 주체에 액세스 권한을 부여 합니다.  
  
`[ @profile_id = ] profile_id` 연결에 대 한 프로필의 id입니다. *profile_id* 됩니다 **int**, 기본값은 NULL입니다. 어느 *profile_id* 하거나 *profile_name* 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'` 연결에 대 한 프로필의 이름입니다. *profile_name* 됩니다 **sysname**, 기본값은 없습니다. 어느 *profile_id* 하거나 *profile_name* 지정 해야 합니다.  
  
`[ @is_default = ] is_default` 이 프로필이 보안 주체의 기본 프로필 인지 여부를 지정 합니다. 보안 주체는 하나의 기본 프로필을 가져야 합니다. *is_default* 됩니다 **비트**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 프로필을 공개 하려면를 지정 된 **@principal_id** 의 **0** 또는 **@principal_name** 의 **공용**합니다. 공개 프로필은 모든 사용자에 게 제공 합니다 **msdb** 데이터베이스, 사용자는 또한의 멤버 여야 하지만 **DatabaseMailUserRole** 실행할 **sp_send_dbmail**합니다.  
  
 데이터베이스 사용자는 하나의 기본 프로필만 가질 수 있습니다. 때 **@is_default** 는 '**1**' 사용자가 이미 하나 이상의 프로필을 사용 하 여 연결 지정된 된 프로필에는 사용자에 대 한 기본 프로필이 됩니다. 이전에 기본 프로필이던 프로필은 사용자와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
 때 **@is_default** 는 '**0**' 및 다른 연결이 없을, 저장된 프로시저는 오류를 반환 합니다.  
  
 저장된 프로시저 **sysmail_add_principalprofile_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 연결 생성 및 기본 프로필 설정**  
  
 다음 예제에서는 라는 프로필 간의 연결을 만듭니다 `AdventureWorks Administrator Profile` 하며 **msdb** 데이터베이스 사용자 `ApplicationUser`합니다. 이 프로필은 해당 사용자의 기본 프로필입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. 프로필을 기본 공개 프로필로**  
  
 다음 예에서는 프로필 `AdventureWorks Public Profile` 사용자에 대 한 기본 공개 프로필을 **msdb** 데이터베이스입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
