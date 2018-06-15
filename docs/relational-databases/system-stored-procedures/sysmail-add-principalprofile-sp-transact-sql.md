---
title: sysmail_add_principalprofile_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d5eda99649aa5f27cc199a2a4676c0f79d36c80
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261492"
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
 [ **@principal_id** = ] *principal_id*  
 데이터베이스 사용자 또는 역할의 ID는 **msdb** 연결에 대 한 데이터베이스입니다. *principal_id* 은 **int**, 기본값은 NULL입니다. 어느 *principal_id* 또는 *principal_name* 지정 해야 합니다. A *principal_id* 의 **0** 이면이 프로필은 공개 프로필이 데이터베이스의 모든 보안 주체에 대 한 액세스를 부여 합니다.  
  
 [ **@principal_name** =] **'***principal_name***'**  
 데이터베이스 사용자 또는 역할의 이름에서 **msdb** 연결에 대 한 데이터베이스입니다. *principal_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *principal_id* 또는 *principal_name* 지정 해야 합니다. A *principal_name* 의 **'public'** 이면이 프로필은 공개 프로필이 데이터베이스의 모든 보안 주체에 대 한 액세스를 부여 합니다.  
  
 [ **@profile_id** = ] *profile_id*  
 연결에 대한 프로필의 ID입니다. *profile_id* 은 **int**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 연결에 대한 프로필의 이름입니다. *profile_name* 은 **sysname**, 기본값은 없습니다. 어느 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@is_default** =] *is_default*  
 해당 프로필이 해당 보안 주체에 대한 기본 프로필인지 여부를 지정합니다. 보안 주체는 하나의 기본 프로필을 가져야 합니다. *is_default* 은 **비트**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 프로필을 공개 하려면 지정 된 **@principal_id** 의 **0** 또는 **@principal_name** 의 **공용**합니다. 공개 프로필은 모든 사용자에 게 사용할 수는 **msdb** 데이터베이스 사용자의 멤버 여야 합니다. 하지만 **DatabaseMailUserRole** 실행할 **sp_send_dbmail**합니다.  
  
 데이터베이스 사용자는 하나의 기본 프로필만 가질 수 있습니다. 때 **@is_default** 은 '**1**' 및 사용자가 이미 있는 연결 된 하나 이상의 프로필, 지정된 된 프로필에서 사용자에 대 한 기본 프로필이 됩니다. 이전에 기본 프로필이던 프로필은 사용자와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
 때 **@is_default** 은 '**0**'와 다른 연결이 없을, 저장된 프로시저가 오류를 반환 합니다.  
  
 저장된 프로시저 **sysmail_add_principalprofile_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 연결 생성 및 기본 프로필 설정**  
  
 다음 예에서는 라는 프로필 간 연결 `AdventureWorks Administrator Profile` 및 **msdb** 데이터베이스 사용자 `ApplicationUser`합니다. 이 프로필은 해당 사용자의 기본 프로필입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. 프로필을 기본 공개 프로필로**  
  
 다음 예에서는 프로필 `AdventureWorks Public Profile` 사용자에 대 한 기본 공개 프로필은 **msdb** 데이터베이스입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
