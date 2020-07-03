---
title: sp_srvrolepermission (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
ms.openlocfilehash: 930b5ae195ab917faf5425bd2084314a633318b3
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893031"
---
# <a name="sp_srvrolepermission-transact-sql"></a>sp_srvrolepermission(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  고정 서버 역할의 사용 권한을 표시합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>인수  
`[ @srvrolename = ] 'role'`사용 권한이 반환 되는 고정 서버 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 NULL입니다. 역할을 지정하지 않으면 모든 고정 서버 역할의 사용 권한이 반환됩니다. *role* 은 다음 값 중 하나를 사용할 수 있습니다.  
  
|값|설명|  
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
|**ServerRole**|**sysname**|고정 서버 역할의 이름입니다.|  
|**사용 권한**|**sysname**|**ServerRole** 와 연결 된 권한|  
  
## <a name="remarks"></a>설명  
 실행할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 고정 서버 역할의 멤버가 수행할 수 있는 기타 특수 작업 등의 사용 권한이 나열됩니다. 고정 서버 역할 목록을 표시 하려면 **sp_helpsrvrole**를 실행 합니다.  
  
 **Sysadmin** 고정 서버 역할에는 다른 모든 고정 서버 역할의 사용 권한이 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 쿼리는 `sysadmin` 고정 서버 역할과 관련된 사용 권한을 반환합니다.  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addsrvrolemember &#40;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_dropsrvrolemember &#40;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_helpsrvrole &#40;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
