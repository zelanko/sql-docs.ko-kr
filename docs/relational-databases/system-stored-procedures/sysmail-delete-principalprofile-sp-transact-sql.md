---
title: sysmail_delete_principalprofile_sp (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 86f9566ce86423939aff22fc37331c5c9db89904
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909216"
---
# <a name="sysmail_delete_principalprofile_sp-transact-sql"></a>sysmail_delete_principalprofile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  퍼블릭 또는 프라이빗 데이터베이스 메일 프로필을 사용하는 데이터베이스 사용자 또는 역할의 사용 권한을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @principal_id = ] principal_id`삭제할 연결의 **msdb** 데이터베이스에 있는 데이터베이스 사용자 또는 역할의 ID입니다. *principal_id* 은 **int**이며 기본값은 NULL입니다. 공개 프로필을 개인 프로필로 만들려면 보안 주체 ID **0** 또는 보안 주체 이름 **' public '** 을 제공 합니다. *Principal_id* 또는 *principal_name* 를 지정 해야 합니다.  
  
`[ @principal_name = ] 'principal_name'`삭제할 연결의 **msdb** 데이터베이스에 있는 데이터베이스 사용자 또는 역할의 이름입니다. *principal_name* 는 **sysname**이며 기본값은 NULL입니다. 공개 프로필을 개인 프로필로 만들려면 보안 주체 ID **0** 또는 보안 주체 이름 **' public '** 을 제공 합니다. *Principal_id* 또는 *principal_name* 를 지정 해야 합니다.  
  
`[ @profile_id = ] profile_id`삭제할 연결에 대 한 프로필의 ID입니다. *profile_id* 은 **int**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'`삭제할 연결에 대 한 프로필의 이름입니다. *profile_name* 는 **sysname**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 공개 프로필을 개인 프로필로 만들려면 보안 주체 이름으로 **' public '** 을 입력 하거나 보안 주체 id로 **0** 을 입력 합니다.  
  
 사용자의 기본 프라이빗 프로필이나 기본 퍼블릭 프로필에 대한 사용 권한을 제거할 때는 주의해야 합니다. 기본 프로필을 사용할 수 없는 경우 **sp_send_dbmail** 는 프로필의 이름을 인수로 사용 해야 합니다. 따라서 기본 프로필을 제거 하면 **sp_send_dbmail** 호출이 실패할 수 있습니다. 자세한 내용은 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)를 참조 하세요.  
  
 **Sysmail_delete_principalprofile_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **msdb** 데이터베이스에서 프로필 **AdventureWorks 관리자** 와 로그인 **applicationuser** 간의 연결을 삭제 하는 방법을 보여 줍니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
