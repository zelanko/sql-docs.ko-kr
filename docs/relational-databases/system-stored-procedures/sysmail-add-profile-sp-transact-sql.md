---
title: sysmail_add_profile_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2ae569ea3623c81e99bac6dd5a163393c07c0301
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891010"
---
# <a name="sysmail_add_profile_sp-transact-sql"></a>sysmail_add_profile_sp(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  새 데이터베이스 메일 프로필을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_name = ] 'profile\_name'`새 프로필의 이름입니다. *profile_name* 는 **sysname**이며 기본값은 없습니다.  
 
   > [!NOTE]
   > Azure SQL Managed Instance SQL 에이전트를 사용 하는 프로필 이름을 호출 해야 합니다 **AzureManagedInstance_dbmail_profile**
  
`[ @description = ] 'description'`새 프로필에 대 한 선택적 설명입니다. *description* 은 **nvarchar (256)** 이며 기본값은 없습니다.  
  
`[ @profile_id = ] _new\_profile\_id OUTPUT`새 프로필의 ID를 반환 합니다. *new_profile_id* 은 **int**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 프로필에는 여러 개의 데이터베이스 메일 계정이 있습니다. 데이터베이스 메일 저장 프로시저는 해당 프로시저에서 생성된 프로필 이름이나 프로필 ID로 프로필을 참조할 수 있습니다. 프로필에 계정을 추가 하는 방법에 대 한 자세한 내용은 [sysmail_add_profileaccount_sp &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)을 참조 하십시오.  
  
 프로필 이름 및 설명 **sysmail_update_profile_sp**저장 프로시저를 사용 하 여 변경할 수 있지만 프로필 id는 프로필 수명 동안 일정 하 게 유지 됩니다.  
  
 프로필 이름은 Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 고유해야 합니다. 그렇지 않으면 저장 프로시저가 오류를 반환합니다.  
  
 **Sysmail_add_profile_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 **1. 새 프로필 작성**  
  
 다음 예에서는 `AdventureWorks Administrator`라는 새 데이터베이스 메일 프로필을 만듭니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **2. 새 프로필 작성 및 변수에 프로필 저장**  
  
 다음 예에서는 `AdventureWorks Administrator`라는 새 데이터베이스 메일 프로필을 만듭니다. 이 예에서는 프로필 ID를 `@profileId` 변수에 저장하고 새 프로필의 프로필 ID를 포함하는 결과 집합을 반환합니다.  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
