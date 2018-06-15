---
title: sysmail_add_profile_sp (Transact SQL) | Microsoft Docs
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
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16091d14ba4971ae8e07633dd111dd5f5a2facde
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260226"
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 데이터베이스 메일 프로필을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@profile_name** = ] **'***profile_name***'**  
 새 프로필 이름입니다. *profile_name* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@description** =] **'***설명***'**  
 새 프로필에 대한 선택적 설명입니다. *설명* 은 **nvarchar (256)**, 기본값은 없습니다.  
  
 [ **@profile_id** = ] *new_profile_id***OUTPUT**  
 새 프로필의 ID를 반환합니다. *new_profile_id* 은 **int**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 프로필에는 여러 개의 데이터베이스 메일 계정이 있습니다. 데이터베이스 메일 저장 프로시저는 해당 프로시저에서 생성된 프로필 이름이나 프로필 ID로 프로필을 참조할 수 있습니다. 프로필에 계정을 추가 하는 방법에 대 한 자세한 내용은 참조 [sysmail_add_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)합니다.  
  
 저장된 프로시저와 함께 프로필 이름과 설명을 변경할 수 있습니다 **sysmail_update_profile_sp**프로필 id 프로필의 수명 기간 동안 일정 하 게 유지 하는 반면, 합니다.  
  
 프로필 이름은 Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 고유해야 합니다. 그렇지 않으면 저장 프로시저가 오류를 반환합니다.  
  
 저장된 프로시저 **sysmail_add_profile_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 **A. 새 프로필 만들기**  
  
 다음 예에서는 `AdventureWorks Administrator`라는 새 데이터베이스 메일 프로필을 만듭니다.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. 새 프로필 작성 및 변수에 프로필 저장**  
  
 다음 예에서는 `AdventureWorks Administrator`라는 새 데이터베이스 메일 프로필을 만듭니다. 이 예에서는 프로필 ID를 `@profileId` 변수에 저장하고 새 프로필의 프로필 ID를 포함하는 결과 집합을 반환합니다.  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
