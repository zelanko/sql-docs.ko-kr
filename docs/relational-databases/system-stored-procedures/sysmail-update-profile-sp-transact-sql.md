---
title: sysmail_update_profile_sp (TRANSACT-SQL) | Microsoft Docs
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
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f16d17779ed6c60ef91b89503f69259eb2093d74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailupdateprofilesp-transact-sql"></a>sysmail_update_profile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 프로필의 설명이나 이름을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@profile_id** = ] *profile_id*  
 업데이트할 프로필 ID입니다. *profile_id* 은 **int**, 기본값은 NULL입니다. 중 하나 이상을 *profile_id* 또는 *profile_name* 지정 해야 합니다. 둘 다 지정하면 프로시저에서 프로필의 이름을 변경합니다.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 업데이트할 프로필의 이름 또는 프로필의 새 이름입니다. *profile_name* 은 **sysname**, 기본값은 NULL입니다. 중 하나 이상을 *profile_id* 또는 *profile_name* 지정 해야 합니다. 둘 다 지정하면 프로시저에서 프로필의 이름을 변경합니다.  
  
 [ **@description** =] **'***설명***'**  
 프로필에 대한 새 설명입니다. *설명* 은 **nvarchar (256)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 프로필 ID와 프로필 이름을 둘 다 지정하면 프로시저가 프로필 이름을 제공된 이름으로 변경하고 프로필에 대한 설명을 업데이트합니다. 이 인수 중 하나만 제공할 경우 프로시저는 프로필에 대한 설명을 업데이트합니다.  
  
 저장된 프로시저 **sysmail_update_profile_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 프로필 설명 변경**  
  
 다음 예제에서는 명명 된 프로필에 대 한 설명을 변경 `AdventureWorks Administrator` 에 **msdb** 데이터베이스입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **B. 이름 및 프로필 설명 변경**  
  
 다음 예에서는 프로필 ID가 `750`인 프로필의 이름과 설명을 변경합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
