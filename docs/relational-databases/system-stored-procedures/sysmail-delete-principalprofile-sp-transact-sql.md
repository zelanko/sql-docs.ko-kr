---
title: sysmail_delete_principalprofile_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae63fabdca36e70daa6da28daa136a5dfcec8e1f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527785"
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  퍼블릭 또는 프라이빗 데이터베이스 메일 프로필을 사용하는 데이터베이스 사용자 또는 역할의 사용 권한을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @principal_id = ] principal_id` 데이터베이스 사용자 또는 역할의 id를 **msdb** 삭제할 연결에 대 한 데이터베이스입니다. *principal_id* 됩니다 **int**, 기본값은 NULL입니다. 공개 프로필을 개인 프로필로 되도록 보안 주체 ID를 제공 **0** 주체 이름이 나 **'public'** 합니다. 어느 *principal_id* 하거나 *principal_name* 지정 해야 합니다.  
  
`[ @principal_name = ] 'principal_name'` 데이터베이스 사용자 또는 역할의 이름인 합니다 **msdb** 삭제할 연결에 대 한 데이터베이스입니다. *principal_name* 됩니다 **sysname**, 기본값은 NULL입니다. 공개 프로필을 개인 프로필로 되도록 보안 주체 ID를 제공 **0** 주체 이름이 나 **'public'** 합니다. 어느 *principal_id* 하거나 *principal_name* 지정 해야 합니다.  
  
`[ @profile_id = ] profile_id` 삭제할 연결에 대 한 프로필의 ID입니다. *profile_id* 됩니다 **int**, 기본값은 NULL입니다. 어느 *profile_id* 하거나 *profile_name* 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'` 삭제할 연결에 대 한 프로필의 이름이입니다. *profile_name* 됩니다 **sysname**, 기본값은 NULL입니다. 어느 *profile_id* 하거나 *profile_name* 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 공개 프로필을 개인 프로필로 되도록 제공 **'public'** 주체 이름 또는 **0** 보안 주체 id에 대 한 합니다.  
  
 사용자의 기본 프라이빗 프로필이나 기본 퍼블릭 프로필에 대한 사용 권한을 제거할 때는 주의해야 합니다. 사용할 수 있으면 기본 프로필이 없을 **sp_send_dbmail** 인수로 프로필 이름이 필요 합니다. 따라서 기본 프로필을 제거 발생할 수 있습니다에 대 한 호출 **sp_send_dbmail** 실패 합니다. 자세한 내용은 [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)합니다.  
  
 저장된 프로시저 **sysmail_delete_principalprofile_sp** 에 **msdb** 데이터베이스 및 소유 하는 **dbo** 스키마입니다. 현재 데이터베이스에는 없는 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 권한을 실행 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 프로필 간의 연결을 삭제 **AdventureWorks Administrator** 로그인 **ApplicationUser** 에 **msdb** 데이터베이스입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
