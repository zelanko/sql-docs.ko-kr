---
description: sys.dm_cryptographic_provider_keys(Transact-SQL)
title: sys. dm_cryptographic_provider_keys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys_TSQL
- dm_cryptographic_provider_keys
- sys.dm_cryptographic_provider_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_keys dynamic management function
ms.assetid: 5a8c1421-c56b-44b5-96e5-4f01782a0c7c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1f2ee5bd2a0aecd1cd56d4efd041caf920f19e61
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542333"
---
# <a name="sysdm_cryptographic_provider_keys-transact-sql"></a>sys.dm_cryptographic_provider_keys(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  EKM(확장 가능 키 관리) 공급자가 제공한 키에 대한 정보를 반환합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
dm_cryptographic_provider_keys ( provider_id )  
```  
  
## <a name="arguments"></a>인수  
 *provider_id*  
 EKM 공급자의 ID 번호이며 기본값은 없습니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**key_id**|**int**|공급자에서 키의 ID 번호입니다.|  
|**key_name**|**nvarchar(512)**|공급자에서 키의 이름입니다.|  
|**key_thumbprint**|**varbinary(32)**|키의 공급자 손도장입니다|  
|**algorithm_id**|**int**|공급자에서 알고리즘의 ID 번호입니다.|  
|**algorithm_tag**|**int**|공급자에서 알고리즘의 태그입니다.|  
|**key_type**|**nchar(256)**|공급자에서 키의 유형입니다.|  
|**key_length**|**int**|공급자에서 키의 길이입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 뷰가 쿼리되면 사용자 컨텍스트를 공급자로 인증하고 모든 키를 열거하여 사용자에게 표시합니다.  
  
 사용자가 EKM 공급자로 인증할 수 없으면 키 정보가 반환되지 않습니다.  
  
## <a name="examples"></a>예제  
 다음 예제에서는 ID 번호 `1234567`과 함께 공급자에 대한 키 속성을 표시합니다.  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
