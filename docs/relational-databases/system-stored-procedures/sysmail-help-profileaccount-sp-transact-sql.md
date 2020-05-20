---
title: sysmail_help_profileaccount_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ea49facab2c91961a49fbb0c4d04ddc30e6253cb
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807532"
---
# <a name="sysmail_help_profileaccount_sp-transact-sql"></a>sysmail_help_profileaccount_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나 이상의 데이터베이스 메일 프로필과 연관된 계정을 나열합니다.  
    
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id`나열할 프로필의 프로필 ID입니다. *profile_id* 은 **int**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'`나열할 프로필의 프로필 이름입니다. *profile_name* 는 **sysname**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @account_id = ] account_id`나열할 계정 ID입니다. *account_id* 은 **int**이며 기본값은 NULL입니다. *Account_id* 및 *account_name* 모두 NULL 이면 프로필의 모든 계정을 나열 합니다.  
  
`[ @account_name = ] 'account_name'`나열할 계정의 이름입니다. *account_name* 는 **sysname**이며 기본값은 NULL입니다. *Account_id* 및 *account_name* 모두 NULL 이면 프로필의 모든 계정을 나열 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 열을 포함한 결과 집합을 반환합니다.  
  
||||  
|-|-|-|  
|열 이름|데이터 형식|Description|  
|**profile_id**|**int**|프로필의 ID입니다.|  
|**profile_name**|**sysname**|프로필의 이름입니다.|  
|**account_id**|**int**|계정의 ID입니다.|  
|**account_name**|**sysname**|계정 이름입니다.|  
|**sequence_number**|**int**|프로필 내 계정의 시퀀스 번호입니다.|  
  
## <a name="remarks"></a>설명  
 *Profile_id* 또는 *profile_name* 지정 되지 않은 경우이 저장 프로시저는 인스턴스의 모든 프로필에 대 한 정보를 반환 합니다.  
  
 **Sysmail_help_profileaccount_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 **1. 이름별로 특정 프로필에 대한 계정 나열**  
  
 다음 예에서는 프로필 이름을 지정하여 `AdventureWorks Administrator` 프로필에 대한 정보를 보여 줍니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **2. 프로필 ID별로 특정 프로필에 대한 계정 나열**  
  
 다음 예에서는 프로필 ID를 지정하여 `AdventureWorks Administrator` 프로필에 대한 정보를 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **3. 모든 프로필에 대한 계정 나열**  
  
 다음 예에서는 인스턴스에 있는 모든 프로필에 대한 계정을 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
