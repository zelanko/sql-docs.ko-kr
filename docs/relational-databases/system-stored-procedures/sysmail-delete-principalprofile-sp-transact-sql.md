---
title: sysmail_delete_principalprofile_sp (TRANSACT-SQL) | Microsoft Docs
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
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a0ac22fd71b80aa973d3e114a76e1f1bd192fc1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  공개 또는 개인 데이터베이스 메일 프로필을 사용하는 데이터베이스 사용자 또는 역할의 사용 권한을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>인수  
 [ **@principal_id** = ] *principal_id*  
 데이터베이스 사용자 또는 역할의 id는 **msdb** 삭제할 연결에 대 한 데이터베이스입니다. *principal_id* 은 **int**, 기본값은 NULL입니다. 공개 프로필을 개인 프로필로 하려면 보안 주체 ID를 제공 **0** 또는 사용자 이름 **'public'**합니다. 어느 *principal_id* 또는 *principal_name* 지정 해야 합니다.  
  
 [ **@principal_name** =] **'***principal_name***'**  
 데이터베이스 사용자 또는 역할의 이름인는 **msdb** 삭제할 연결에 대 한 데이터베이스입니다. *principal_name* 은 **sysname**, 기본값은 NULL입니다. 공개 프로필을 개인 프로필로 하려면 보안 주체 ID를 제공 **0** 또는 사용자 이름 **'public'**합니다. 어느 *principal_id* 또는 *principal_name* 지정 해야 합니다.  
  
 [ **@profile_id** = ] *profile_id*  
 삭제할 연결에 대한 프로필의 ID입니다. *profile_id* 은 **int**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 삭제할 연결에 대한 프로필의 이름입니다. *profile_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *profile_id* 또는 *profile_name* 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 공개 프로필을 개인 프로필로 되도록 제공 **'public'** 계정 이름 또는 **0** 보안 주체 id에 대 한 합니다.  
  
 사용자의 기본 개인 프로필이나 기본 공개 프로필에 대한 사용 권한을 제거할 때는 주의해야 합니다. 사용 가능한 기본 프로필이 없을 경우 **sp_send_dbmail** 는 인수로 프로필의 이름이 필요 합니다. 따라서 제거는 기본 프로필이 않을 수에 대 한 호출 **sp_send_dbmail** 실패 합니다. 자세한 내용은 참조 [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)합니다.  
  
 저장된 프로시저 **sysmail_delete_principalprofile_sp** 에 **msdb** 데이터베이스에 있으며가 소유 하 고는 **dbo** 스키마입니다. 현재 데이터베이스 없는 경우 세 부분으로 이루어진 이름으로 프로시저를 실행 해야 **msdb**합니다.  
  
## <a name="permissions"></a>Permissions  
 실행의 구성원에 게이 프로시저 기본값에 대 한 권한을 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 프로필 간의 연결 삭제 **AdventureWorks Administrator** 및 로그인 **ApplicationUser** 에 **msdb** 데이터베이스입니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [데이터베이스 메일 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
