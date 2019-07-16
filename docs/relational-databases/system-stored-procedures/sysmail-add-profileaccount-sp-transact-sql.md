---
title: sysmail_add_profileaccount_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11ada827add27ae2186fdcc565b3dd2f99f76452
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017757"
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 프로필에 데이터베이스 메일 계정을 추가합니다. 실행 **sysmail_add_profileaccount_sp** 사용 하 여 데이터베이스 계정을 만든 후 [sysmail_add_account_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)에 데이터베이스 프로필 를사용하여만들어지고[sysmail_add_profile_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id` 계정을 추가할 프로필 id입니다. *profile_id* 됩니다 **int**, 기본값은 NULL입니다. 중 하나는 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'` 계정을 추가할 프로필 이름입니다. *profile_name* 됩니다 **sysname**, 기본값은 NULL입니다. 중 하나는 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
`[ @account_id = ] account_id` 프로필에 추가할 계정 id입니다. *account_id* 됩니다 **int**, 기본값은 NULL입니다. 중 하나는 *account_id* 또는 *account_name* 지정 해야 합니다.  
  
`[ @account_name = ] 'account_name'` 프로필에 추가할 계정의 이름입니다. *account_name* 됩니다 **sysname**, 기본값은 NULL입니다. 중 하나는 *account_id* 또는 *account_name* 지정 해야 합니다.  
  
`[ @sequence_number = ] sequence_number` 프로필 내 계정의 시퀀스 번호입니다. *sequence_number* 됩니다 **int**, 기본값은 없습니다. 시퀀스 번호는 프로필의 계정이 사용되는 순서를 결정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 프로필과 계정 모두 이미 있어야 합니다. 그렇지 않으면 저장 프로시저가 오류를 반환합니다.  
  
 이 저장 프로시저는 지정한 프로필에 이미 연결되어 있는 계정의 시퀀스 번호를 변경하지 않습니다. 계정의 시퀀스 번호를 업데이트 하는 방법에 대 한 자세한 내용은 참조 하세요. [sysmail_update_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)합니다.  
  
 시퀀스 번호는 데이터베이스 메일에서 프로필의 계정을 사용하는 순서를 결정합니다. 새 전자 메일 메시지의 경우 데이터베이스 메일은 시퀀스 번호가 가장 낮은 계정에서 시작합니다. 해당 계정이 실패하면 데이터베이스 메일에서는 시퀀스 번호가 다음으로 높은 계정을 사용하여 메시지가 성공적으로 전송될 때까지 또는 시퀀스 번호가 가장 높은 계정이 실패할 때까지 작업을 계속합니다. 시퀀스 번호가 가장 높은 계정이 실패하면 데이터베이스 메일은 *sysmail_configure_sp* 의 **AccountRetryDelay**매개 변수에서 구성한 기간 동안 메일을 보내려는 시도를 일시 중지했다가 가장 낮은 시퀀스 번호에서 시작하여 다시 메일을 보내려는 시도를 시작합니다. *sysmail_configure_sp* 의 **AccountRetryAttempts**매개 변수를 사용하여 외부 메일 프로세스가 지정한 프로필의 각 계정을 사용하여 전자 메일 메시지를 보내려고 시도하는 횟수를 구성합니다.  
  
 시퀀스 번호가 같은 계정이 둘 이상 있으면 데이터베이스 메일은 지정된 전자 메일 메시지에 대해 해당 계정 중 하나만 사용합니다. 이 경우 데이터베이스 메일에서 항상 특정 시퀀스 번호에 대해 해당 계정이 사용되거나 메시지 간 동일한 계정이 사용되는 것은 아닙니다.  
  
 저장된 프로시저 **sysmail_add_profileaccount_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks Administrator` 프로필의 `Audit Account` 계정에 연결합니다. 감사 계정의 시퀀스 번호는 1입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
