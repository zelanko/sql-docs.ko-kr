---
title: sp_srvrolepermission (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_srvrolepermission_TSQL
- sp_srvrolepermission
dev_langs:
- TSQL
helpviewer_keywords:
- sp_srvrolepermission
ms.assetid: 5709667f-e3e4-48a2-93ec-af5e22a2ac58
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a4ed3adb1fe62d3ad23a58bca3a1dedce86dabee
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033121"
---
# <a name="spsrvrolepermission-transact-sql"></a>sp_srvrolepermission(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  고정 서버 역할의 사용 권한을 표시합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>인수  
 [  **@srvrolename =** ] **'***역할***'**  
 사용 권한을 반환할 고정 서버 역할의 이름입니다. *역할* 됩니다 **sysname**, 기본값은 NULL입니다. 역할을 지정하지 않으면 모든 고정 서버 역할의 사용 권한이 반환됩니다. *역할* 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**sysadmin**|시스템 관리자입니다.|  
|**securityadmin**|보안 관리자입니다.|  
|**serveradmin**|서버 관리자입니다.|  
|**setupadmin**|설치 관리자입니다.|  
|**processadmin**|프로세스 관리자입니다.|  
|**diskadmin**|디스크 관리자입니다.|  
|**dbcreator**|데이터베이스 작성자입니다.|  
|**bulkadmin**|BULK INSERT 문을 실행할 수 있습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**서버 역할**|**sysname**|고정 서버 역할의 이름입니다.|  
|**사용 권한**|**sysname**|와 관련 된 권한은 **ServerRole**|  
  
## <a name="remarks"></a>Remarks  
 실행할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 고정 서버 역할의 멤버가 수행할 수 있는 기타 특수 작업 등의 사용 권한이 나열됩니다. 가 고정된 서버 역할의 목록을 표시 하려면 실행 **sp_helpsrvrole**합니다.  
  
 합니다 **sysadmin** 고정된 서버 역할에 다른 모든 고정된 서버 역할의 권한이 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 쿼리는 `sysadmin` 고정 서버 역할과 관련된 사용 권한을 반환합니다.  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
