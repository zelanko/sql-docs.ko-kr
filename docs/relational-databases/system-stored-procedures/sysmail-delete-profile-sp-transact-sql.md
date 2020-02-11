---
title: sysmail_delete_profile_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profile_sp
- sysmail_delete_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profile_sp
ms.assetid: 71998653-4a02-446d-b6f7-50646a29e8a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9442f4d3637fcb7c891eacbe7546254708918ad3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909205"
---
# <a name="sysmail_delete_profile_sp-transact-sql"></a>sysmail_delete_profile_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일에서 사용하는 메일 프로필을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_delete_profile_sp  { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @profile_id = ] profile_id`삭제할 프로필의 프로필 id입니다. *profile_id* 은 **int**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
`[ @profile_name = ] 'profile_name'`삭제할 프로필의 이름입니다. *profile_name* 는 **sysname**이며 기본값은 NULL입니다. *Profile_id* 또는 *profile_name* 를 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 프로필을 삭제해도 프로필에서 사용하는 계정은 삭제되지 않습니다.  
  
 이 저장 프로시저는 사용자가 프로필에 액세스할 수 있는지 여부에 관계없이 프로필을 삭제합니다. 사용자의 기본 개인 프로필 또는 **msdb** 데이터베이스의 기본 공개 프로필을 제거할 때는 주의 해야 합니다. 기본 프로필을 사용할 수 없는 경우 **sp_send_dbmail** 는 프로필의 이름을 인수로 사용 해야 합니다. 따라서 기본 프로필을 제거 하면 **sp_send_dbmail** 호출이 실패할 수 있습니다. 자세한 내용은 [sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)를 참조 하세요.  
  
 **Sysmail_delete_profile_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks Administrator`라는 프로필을 삭제합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 구성 개체](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
