---
description: sysmail_add_principalprofile_sp(Transact-SQL)
title: sysmail_add_principalprofile_sp (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6092ba1de12d71ff50facbafd7fed04aed9d9fd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547243"
---
# <a name="sysmail_add_principalprofile_sp-transact-sql"></a>sysmail_add_principalprofile_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 메일 프로필을 사용 하는 msdb 데이터베이스 보안 주체에 대 한 사용 권한을 부여 합니다. 데이터베이스 보안 주체는 SQL Server 인증 사용자, Windows 사용자 또는 Windows 그룹에 매핑되어야 합니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @principal_id = ] principal_id` 연결에 대 한 **msdb** 데이터베이스에 있는 데이터베이스 사용자 또는 역할의 ID입니다. *principal_id* 은 **int**이며 기본값은 NULL입니다. *Principal_id* 또는 *principal_name* 를 지정 해야 합니다. 0 *principal_id* 하면 **0** 이 프로필은 공개 프로필이 되며 데이터베이스의 모든 보안 주체에 게 액세스 권한을 부여 합니다.  
  
`[ @principal_name = ] 'principal_name'` 연결에 대 한 **msdb** 데이터베이스에 있는 데이터베이스 사용자 또는 역할의 이름입니다. *principal_name* 는 **sysname**이며 기본값은 NULL입니다. *Principal_id* 또는 *principal_name* 를 지정 해야 합니다. **' Public '** *principal_name* 이 프로필을 공개 프로필로 만들어 데이터베이스의 모든 보안 주체에 대 한 액세스 권한을 부여 합니다.  
  
`[ @profile_id = ] profile_id` 연결에 대 한 프로필의 id입니다. *profile_id* 은 **int**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'` 연결에 대 한 프로필의 이름입니다. *profile_name* 는 **sysname**이며 기본값은 없습니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @is_default = ] is_default` 이 프로필이 보안 주체의 기본 프로필 인지 여부를 지정 합니다. 보안 주체는 하나의 기본 프로필을 가져야 합니다. *is_default* 은 **bit**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 프로필을 공용으로 설정 하려면 ** \@ principal_id** **0** 또는 **public** ** \@ principal_name** 를 지정 합니다. 공용 프로필은 **msdb** 데이터베이스의 모든 사용자가 사용할 수 있지만 **sp_send_dbmail**를 실행 하려면 사용자가 **DatabaseMailUserRole** 의 멤버 여야 합니다.  
  
 데이터베이스 사용자는 하나의 기본 프로필만 가질 수 있습니다. ** \@ Is_default** '**1**'이 고 사용자가 이미 하나 이상의 프로필에 연결 된 경우 지정 된 프로필이 사용자의 기본 프로필이 됩니다. 이전에 기본 프로필이던 프로필은 사용자와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
 ** \@ Is_default** 가 '**0**'이 고 다른 연결이 없는 경우 저장 프로시저에서 오류를 반환 합니다.  
  
 **Sysmail_add_principalprofile_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 **1. 연결 생성 및 기본 프로필 설정**  
  
 다음 예에서는 라는 프로필과 `AdventureWorks Administrator Profile` **msdb** 데이터베이스 사용자 간의 연결을 만듭니다 `ApplicationUser` . 이 프로필은 해당 사용자의 기본 프로필입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **2. 프로필을 기본 공개 프로필로 사용**  
  
 다음 예에서는 프로필을 `AdventureWorks Public Profile` **msdb** 데이터베이스의 사용자에 대 한 기본 공개 프로필로 만듭니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
