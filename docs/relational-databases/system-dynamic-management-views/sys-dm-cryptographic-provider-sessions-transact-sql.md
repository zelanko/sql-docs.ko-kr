---
description: sys.dm_cryptographic_provider_sessions(Transact-SQL)
title: sys. dm_cryptographic_provider_sessions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 37a8854da08439c4dc3984bcdfc61a8695467c2b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455019"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  암호화 공급자에 대해 열려 있는 세션에 대한 정보를 반환합니다.  
 
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>인수  
 *session_identifier*  
 반환될 세션을 나타내는 정수입니다.  
  
 0 = 현재 연결만  
  
 1 = 모든 암호화 연결  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|암호화 공급자의 ID 번호입니다.|  
|**session_handle**|**varbytes (8)**|암호화 세션 처리입니다.|  
|**identity**|**nvarchar(128)**|암호화 공급자로 인증하는 데 사용되는 ID입니다.|  
|**spid**|**short**|연결의 세션 ID SPID입니다. 자세한 내용은 [@@SPID&#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)을 참조하세요.|  
  
## <a name="remarks"></a>설명  
 현재 연결에 대 한 **dm_cryptographic_provider_sessions** 뷰가 public에 표시 됩니다. 모든 암호화 연결을 보려면 **CONTROL** server 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
