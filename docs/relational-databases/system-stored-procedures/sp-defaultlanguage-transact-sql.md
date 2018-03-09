---
title: sp_defaultlanguage (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfd63d6dddf3cc553ffee62dffbacff891d1991c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 기본 언어를 변경합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>인수  
 [  **@loginame =** ] **'***로그인***'**  
 로그인 이름입니다. *로그인* 은 **sysname**, 기본값은 없습니다. *로그인* 기존 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 이나 Windows 사용자 또는 그룹입니다.  
  
 [  **@language =** ] **'***언어***'**  
 로그인의 기본 언어입니다. *언어* 은 **sysname**, 기본값은 NULL입니다. *언어* 서버에서 유효한 언어 여야 합니다. 경우 *언어* 를 지정 하지 않으면 *언어* 서버의 기본 언어;로 설정 된 기본 언어에 의해 정의 됩니다는 **sp_configure** 구성 변수 **기본 언어**합니다. 서버의 기본 언어를 변경해도 기존 로그인의 기본 언어는 변경되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_defaultlanguage** 추가 옵션을 지 원하는 ALTER LOGIN을 호출 합니다. 다른 로그인 기본값을 변경 하는 방법에 대 한 정보를 참조 하세요. [ALTER login&#40; Transact SQL &#41; ](../../t-sql/statements/alter-login-transact-sql.md).  
  
 SET LANGUAGE 문을 사용하여 현재 세션의 언어를 변경할 수 있습니다. 사용 된 @@LANGUAGE 함수를 현재 언어 설정을 표시 합니다.  
  
 로그인의 기본 언어가 서버에서 삭제된 경우에는 서버의 기본 언어가 로그인의 기본 언어로 사용됩니다. **sp_defaultlanguage** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
 서버에 설치 된 언어에 대 한 정보에 표시 됩니다는 **sys.syslanguages** 카탈로그 뷰에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ALTER LOGIN`을 사용하여 `Fathima` 로그인의 기본 언어를 아랍어로 변경합니다. 이것은 기본적으로 사용되는 방법입니다.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys.syslanguages&#40; Transact SQL &#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
