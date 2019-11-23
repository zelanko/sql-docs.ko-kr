---
title: sysmail_delete_account_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_account_sp
- sysmail_delete_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_account_sp
ms.assetid: 2adcac78-4a4a-407e-9666-1d9c43c73cc2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4b6adc5f6c02eae49a5f5e2598c6b02e5b00534e
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211268"
---
# <a name="sysmail_delete_account_sp-transact-sql"></a>sysmail_delete_account_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  데이터베이스 메일 SMTP 계정을 삭제합니다. 데이터베이스 메일 구성 마법사를 사용하여 계정을 삭제할 수도 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_account_sp { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }   
```  
  
## <a name="arguments"></a>인수  
삭제할 계정의 ID 번호를 `[ @account_id = ] account_id` 합니다. *account_id* 는 **int**이며 기본값은 없습니다. *Account_id* 또는 *account_name* 를 지정 해야 합니다.  
  
삭제할 계정의 이름을 `[ @account_name = ] 'account_name'` 합니다. *account_name* 는 **sysname**이며 기본값은 없습니다. *Account_id* 또는 *account_name* 를 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 이 프로시저는 프로필의 계정 사용 여부에 관계없이 지정된 계정을 삭제합니다. 계정이 없는 프로필은 전자 메일을 보낼 수 없습니다.  
  
 **Sysmail_delete_account_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks Administrator`라는 데이터베이스 메일 계정을 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정을 만듭니다](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [ &#40;transact-sql&#41;  sysmail_add_account_sp](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)  
 [ &#40;transact-sql&#41;  sysmail_delete_profile_sp](../../relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql.md)  
 [ &#40;transact-sql&#41;  sysmail_delete_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql.md)  
 [ &#40;transact-sql&#41;  sysmail_help_account_sp](../../relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql.md)  
 [ &#40;transact-sql&#41;  sysmail_help_profile_sp](../../relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql.md)  
 [ &#40;transact-sql&#41;  sysmail_help_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql.md)  
 [Transact-sql &#40;sysmail_update_profileaccount_sp&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)  
  
  
