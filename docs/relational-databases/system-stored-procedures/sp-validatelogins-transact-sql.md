---
title: sp_validatelogins (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b60478b4ca3bdd6f2688f5a77c18cdce7166b37d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796041"
---
# <a name="spvalidatelogins-transact-sql"></a>sp_validatelogins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 주체에 매핑되었지만 Windows 환경에 더 이상 존재하지 않는 Windows 사용자 및 그룹에 대한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary(85)**|Windows 사용자 또는 그룹의 Windows SID(보안 식별자)입니다.|  
|**NT 로그인**|**sysname**|Windows 사용자 또는 그룹의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 분리된 서버 수준의 보안 주체가 데이터베이스 사용자를 소유하는 경우 분리된 서버 보안 주체를 제거하려면 먼저 데이터베이스 사용자를 제거해야 합니다. 데이터베이스 사용자를 제거 하려면 사용 하 여 [DROP USER](../../t-sql/statements/drop-user-transact-sql.md)합니다. 서버 수준의 보안 주체가 데이터베이스에서 보안 개체를 소유하는 경우 보안 개체의 소유권이 전송되거나 삭제되어야 합니다. 데이터베이스 보안 개체의 소유권을 사용 하 여 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)합니다.  
  
 더 이상 존재 하지 있는 Windows 사용자 및 그룹으로의 매핑을 제거 하려면 사용 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 하거나 **securityadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 더 이상 존재하지 않지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스가 부여되어 있는 Windows 사용자 및 그룹을 표시합니다.  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [DROP LOGIN&#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
