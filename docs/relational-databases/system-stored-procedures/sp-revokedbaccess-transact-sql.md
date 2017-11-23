---
title: sp_revokedbaccess (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs: TSQL
helpviewer_keywords: sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2802cbef18844b9b33b453db661d11c372d3654
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sprevokedbaccess-transact-sql"></a>sp_revokedbaccess(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 데이터베이스 사용자를 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) 대신 합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>인수  
 [  **@name_in_db =** ] **'***이름***'**  
 제거할 데이터베이스 사용자 이름입니다. *이름* 는 **sysname** 이며 기본값은 없습니다. *이름* 서버 로그인, Windows 로그인 또는 Windows 그룹의 이름이 될 수 있으며 현재 데이터베이스에 존재 해야 합니다. Windows 로그인 또는 Windows 그룹을 지정하는 경우 데이터베이스를 식별할 이름을 지정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 데이터베이스 사용자가 제거되면 해당 사용자에 종속된 사용 권한 및 별칭도 제거됩니다.  
  
 **sp_revokedbaccess** 현재 데이터베이스에서 데이터베이스 사용자만 제거할 수 있습니다. 현재 데이터베이스의 개체를 소유하는 데이터베이스를 제거하기 전에 개체 소유권을 전송하거나 개체를 데이터베이스에서 삭제해야 합니다. 자세한 내용은 참조 [ALTER authorization&#40; Transact SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 **sp_revokedbaccess** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 ALTER ANY USER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는에 매핑된 데이터베이스 사용자를 제거 `Edmonds\LolanSo` 현재 데이터베이스에서 합니다.  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [DROP user&#40; Transact SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
