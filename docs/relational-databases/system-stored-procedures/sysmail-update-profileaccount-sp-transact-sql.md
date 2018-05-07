---
title: sysmail_update_profileaccount_sp (TRANSACT-SQL) | Microsoft Docs
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
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee2f44070644e305163e6a7ae38eea9a81ba9fa1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 프로필 내에서 계정의 시퀀스 번호를 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>인수  
 [ **@profile_id** = ] *profile_id*  
 업데이트할 프로필의 ID입니다. *profile_id* 은 **int**, 기본값은 NULL입니다. 중 하나는 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 업데이트할 프로필의 이름입니다. *profile_name* 은 **sysname**, 기본값은 NULL입니다. 중 하나는 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@account_id** = ] *account_id*  
 업데이트할 계정 ID입니다. *account_id* 은 **int**, 기본값은 NULL입니다. 중 하나는 *account_id* 또는 *account_name* 지정 해야 합니다.  
  
 [ **@account_name** =] **'***account_name***'**  
 업데이트할 계정 이름입니다. *account_name* 은 **sysname**, 기본값은 NULL입니다. 중 하나는 *account_id* 또는 *account_name* 지정 해야 합니다.  
  
 [ **@sequence_number** =] *sequence_number*  
 계정의 새 시퀀스 번호입니다. *sequence_number* 은 **int**, 기본값은 없습니다. 시퀀스 번호는 프로필의 계정이 사용되는 순서를 결정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 지정된 계정과 프로필이 연관되어 있지 않으면 오류를 반환합니다.  
  
 시퀀스 번호는 데이터베이스 메일에서 프로필의 계정을 사용하는 순서를 결정합니다. 새 전자 메일 메시지의 경우 데이터베이스 메일은 시퀀스 번호가 가장 낮은 계정에서 시작합니다. 해당 계정이 실패하면 데이터베이스 메일에서는 시퀀스 번호가 다음으로 높은 계정을 사용하여 메시지가 성공적으로 전송될 때까지 또는 시퀀스 번호가 가장 높은 계정이 실패할 때까지 작업을 계속합니다. 시퀀스 번호가 가장 높은 계정이 실패하면 전자 메일 메시지가 실패합니다.  
  
 시퀀스 번호가 같은 계정이 둘 이상 있으면 데이터베이스 메일은 지정된 전자 메일 메시지에 대해 해당 계정 중 하나만 사용합니다. 이 경우 데이터베이스 메일에서 항상 특정 시퀀스 번호에 대해 해당 계정이 사용되거나 메시지 간 동일한 계정이 사용되는 것은 아닙니다.  
  
 저장된 프로시저 **sysmail_update_profileaccount_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 계정의 시퀀스 번호를 변경 하는 다음 예제 `Admin-BackupServer` 프로필 내 `AdventureWorks Administrator` 에 **msdb** 데이터베이스입니다. 이 코드를 실행하면 계정의 시퀀스 번호는 `3`이 되고 처음 두 계정이 실패하면 해당 계정이 시도된다는 의미입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
