---
description: sysmail_update_profile_sp(Transact-SQL)
title: sysmail_update_profile_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 78a123514e990499f191cbc6742870647adebc5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454756"
---
# <a name="sysmail_update_profile_sp-transact-sql"></a>sysmail_update_profile_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 메일 프로필의 설명이나 이름을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id` 업데이트할 프로필 id입니다. *profile_id* 은 **int**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 중 하나 이상을 지정 해야 합니다. 둘 다 지정하면 프로시저에서 프로필의 이름을 변경합니다.  
  
`[ @profile_name = ] 'profile_name'` 업데이트할 프로필의 이름 또는 프로필의 새 이름입니다. *profile_name* 는 **sysname**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 중 하나 이상을 지정 해야 합니다. 둘 다 지정하면 프로시저에서 프로필의 이름을 변경합니다.  
  
`[ @description = ] 'description'` 프로필에 대 한 새 설명입니다. *description* 은 **nvarchar (256)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 프로필 ID와 프로필 이름을 둘 다 지정하면 프로시저가 프로필 이름을 제공된 이름으로 변경하고 프로필에 대한 설명을 업데이트합니다. 이 인수 중 하나만 제공할 경우 프로시저는 프로필에 대한 설명을 업데이트합니다.  
  
 **Sysmail_update_profile_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 **1. 프로필 설명 변경**  
  
 다음 예에서는 `AdventureWorks Administrator` **msdb** 데이터베이스에 있는 라는 프로필에 대 한 설명을 변경 합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **2. 프로필의 이름과 설명 변경**  
  
 다음 예에서는 프로필 ID가 `750`인 프로필의 이름과 설명을 변경합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
