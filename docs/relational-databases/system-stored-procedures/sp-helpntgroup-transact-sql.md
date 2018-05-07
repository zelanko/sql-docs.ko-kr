---
title: sp_helpntgroup (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpntgroup
- sp_helpntgroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpntgroup
ms.assetid: 02b4f7c1-480a-436c-8bae-7a2488be45d2
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d47be90ed518d818dfc731121215935f30bf9a1f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpntgroup-transact-sql"></a>sp_helpntgroup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 계정이 있는 Windows 그룹에 대한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpntgroup [ [ @ntname= ] 'name' ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@ntname =** ] **'***name***'**  
 Windows 그룹의 이름입니다. *이름* 은 **sysname**, 기본값은 NULL입니다. *이름* 현재 데이터베이스에 액세스할 수 있는 유효한 Windows 그룹 이어야 합니다. 경우 *이름* 을 지정 하지 않으면 현재 데이터베이스에 액세스할 수 있는 모든 Windows 그룹이 출력에 포함 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**NTGroupName**|**sysname**|Windows 그룹의 이름입니다.|  
|**NTGroupId**|**smallint**|그룹 ID(식별자)입니다.|  
|**SID**|**varbinary(85)**|보안 식별자 (SID) **NTGroupName**합니다.|  
|**HasDbAccess**|**int**|1 = Windows 그룹이 데이터베이스에 대한 액세스 권한을 갖고 있습니다.|  
  
## <a name="remarks"></a>주의  
 목록을 보려면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 데이터베이스의 역할을 사용 하 여 **sp_helprole**합니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에 대한 액세스 권한이 있는 Windows 그룹 목록을 인쇄합니다.  
  
```  
EXEC sp_helpntgroup;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_helprole &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_revokedbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
