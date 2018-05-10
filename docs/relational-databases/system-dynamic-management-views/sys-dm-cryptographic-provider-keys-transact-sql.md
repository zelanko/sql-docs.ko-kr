---
title: sys.dm_cryptographic_provider_keys (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 063745549cc60f2c8fe9c59a5470d98758b76c77
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmcryptographicproviderkeys-transact-sql"></a>sys.dm_cryptographic_provider_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  EKM(확장 가능 키 관리) 공급자가 제공한 키에 대한 정보를 반환합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
## <a name="permissions"></a>Permissions  
 이 뷰가 쿼리되면 사용자 컨텍스트를 공급자로 인증하고 모든 키를 열거하여 사용자에게 표시합니다.  
  
 사용자가 EKM 공급자로 인증할 수 없으면 키 정보가 반환되지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 ID 번호 `1234567`과 함께 공급자에 대한 키 속성을 표시합니다.  
  
```  
SELECT * FROM sys.dm_cryptographic_provider_keys(1234567);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
