---
description: sp_validatelogins(Transact-SQL)
title: sp_validatelogins (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: b3237ed7a7d585e128b678772ec6d3a010fe3d00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473444"
---
# <a name="sp_validatelogins-transact-sql"></a>sp_validatelogins(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 주체에 매핑되었지만 Windows 환경에 더 이상 존재하지 않는 Windows 사용자 및 그룹에 대한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**S**|**varbinary(85)**|Windows 사용자 또는 그룹의 Windows SID(보안 식별자)입니다.|  
|**NT Login**|**sysname**|Windows 사용자 또는 그룹의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 분리된 서버 수준의 보안 주체가 데이터베이스 사용자를 소유하는 경우 분리된 서버 보안 주체를 제거하려면 먼저 데이터베이스 사용자를 제거해야 합니다. 데이터베이스 사용자를 제거 하려면 [DROP user](../../t-sql/statements/drop-user-transact-sql.md)를 사용 합니다. 서버 수준의 보안 주체가 데이터베이스에서 보안 개체를 소유하는 경우 보안 개체의 소유권이 전송되거나 삭제되어야 합니다. 보안 개체 데이터베이스의 소유권을 전송 하려면 [ALTER authorization](../../t-sql/statements/alter-authorization-transact-sql.md)을 사용 합니다.  
  
 더 이상 존재 하지 않는 Windows 사용자 및 그룹에 대 한 매핑을 제거 하려면 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)을 사용 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 또는 **securityadmin** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 더 이상 존재하지 않지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스가 부여되어 있는 Windows 사용자 및 그룹을 표시합니다.  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 저장 프로시저 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [DROP LOGIN &#40;Transact-sql&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
