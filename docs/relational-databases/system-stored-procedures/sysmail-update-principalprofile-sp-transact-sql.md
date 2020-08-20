---
description: sysmail_update_principalprofile_sp(Transact-SQL)
title: sysmail_update_principalprofile_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bba3f6ca7046825f4bdd13e062b67b554b636405
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492824"
---
# <a name="sysmail_update_principalprofile_sp-transact-sql"></a>sysmail_update_principalprofile_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  보안 주체와 프로필 간 연결 정보를 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>인수  
`[ @principal_id = ] principal_id` 변경할 연결의 **msdb** 데이터베이스에 있는 데이터베이스 사용자 또는 역할의 ID입니다. *principal_id* 은 **int**이며 기본값은 NULL입니다. *Principal_id* 또는 *principal_name* 를 지정 해야 합니다.  
  
`[ @principal_name = ] 'principal_name'` 업데이트할 연결의 **msdb** 데이터베이스에 있는 데이터베이스 사용자 또는 역할의 이름입니다. *principal_name* 는 **sysname**이며 기본값은 NULL입니다. *Principal_id* 또는 *principal_name* 를 지정할 수 있습니다.  
  
`[ @profile_id = ] profile_id` 연결을 변경할 프로필의 id입니다. *profile_id* 은 **int**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'` 연결을 변경할 프로필의 이름입니다. *profile_name* 는 **sysname**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @is_default = ] 'is_default'` 이 프로필이 데이터베이스 사용자의 기본 프로필 인지 여부입니다. 데이터베이스 사용자는 하나의 기본 프로필만 가질 수 있습니다. *is_default* 은 **bit**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 지정된 프로필이 데이터베이스 사용자의 기본 프로필인지 여부를 변경합니다. 데이터베이스 사용자는 기본 프라이빗 프로필을 하나만 가질 수 있습니다.  
  
 연결에 대 한 보안 주체 이름이 **public** 이거나 연결의 보안 주체 id가 **0**인 경우이 저장 프로시저는 공용 프로필을 변경 합니다. 기본 공개 프로필은 하나만 있을 수 있습니다.  
  
 ** \@ Is_default** 가 '**1**'이 고 보안 주체가 둘 이상의 프로필과 연결 된 경우 지정 된 프로필이 보안 주체의 기본 프로필이 됩니다. 이전에 기본 프로필이던 프로필은 보안 주체와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
 **Sysmail_update_principalprofile_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 **1. 데이터베이스의 기본 공개 프로필로 프로필 설정**  
  
 다음 예에서는 프로필을 `General Use Profile` **msdb** 데이터베이스의 사용자에 대 한 기본 공개 프로필로 설정 합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **2. 사용자의 기본 개인 프로필로 프로필 설정**  
  
 다음 예에서는 `AdventureWorks Administrator` `ApplicationUser` **msdb** 데이터베이스의 보안 주체에 대 한 기본 프로필로 프로필을 설정 합니다. 프로필은 보안 주체에 이미 연결되어 있어야 합니다. 이전에 기본 프로필이던 프로필은 보안 주체와 계속 연결되어 있긴 하지만 더 이상 기본 프로필이 아닙니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
