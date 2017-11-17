---
title: DROP CRYPTOGRAPHIC PROVIDER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP CRYPTOGRAPHIC PROVIDER
- DROP_CRYPTOGRAPHIC_PROVIDER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP CRYPTOGRAPHIC PROVIDER statement
ms.assetid: 71c55c20-439e-4897-aef5-f20e556d668f
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: af3ad1b0356f5eea3812ddd8fe5ce60e9e71aea0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-cryptographic-provider-transact-sql"></a>DROP CRYPTOGRAPHIC PROVIDER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내의 암호화 공급자를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP CRYPTOGRAPHIC PROVIDER provider_name   
```  
  
## <a name="arguments"></a>인수  
 *provider_name*  
 EKM(확장 가능 키 관리) 공급자의 이름입니다.  
  
## <a name="remarks"></a>주의  
 EKM(Extensible Key Management) 공급자를 삭제하려면 공급자를 사용하는 모든 세션을 중지해야 합니다.  
  
 EKM 공급자는 매핑된 자격 증명이 없는 경우에만 삭제할 수 있습니다.  
  
 EKM 공급자를 삭제할 때 EKM 공급자에 매핑된 키가 있으면 해당 키의 GUID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장됩니다. 공급자가 같은 키 GUID로 나중에 만들어진 경우 해당 키는 다시 사용됩니다.  
  
## <a name="permissions"></a>Permissions  
 대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `SecurityProvider`라는 암호화 공급자를 삭제합니다.  
  
```  
/* First, disable provider to perform the upgrade.  
This will terminate all open cryptographic sessions. */  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
SET ENABLED = OFF;  
GO  
/* Drop the provider. */  
DROP CRYPTOGRAPHIC PROVIDER SecurityProvider;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  

