---
title: sys. cryptographic_providers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cryptographic_providers
- sys.cryptographic_providers
- sys.cryptographic_providers_TSQL
- cryptographic_providers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.cryptographic_providers catalog view
ms.assetid: 9da0da95-792e-48b4-9f60-47f0729c279c
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 489baa68c8fe37d4f240d26cb93d65b73016d7dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787177"
---
# <a name="syscryptographic_providers-transact-sql"></a>sys.cryptographic_providers(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  등록된 각 암호화 공급자에 대해 하나의 행을 반환합니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|암호화 공급자의 ID 번호입니다.|  
|**name**|**sysname**|암호화 공급자의 이름입니다.|  
|**guid**|**uniqueidentifier**|고유한 공급자 GUID입니다.|  
|**version**|**nvarchar(50)**|'*Aa.bb.cccc.dd*' 형식의 공급자 버전입니다.|  
|**dll_path**|**nvarchar(512)**|EKM(Extensible Key Management) API(애플리케이션 프로그래밍 인터페이스)를 구현하는 DLL의 경로입니다.|  
|**is_enabled**|**bit**|공급자가 서버에서 설정되어 있는지 여부입니다.<br /><br /> 0 = 설정 안 함(기본값)<br /><br /> 1 = 사용|  
  
## <a name="remarks"></a>설명  
 **Cryptographic_providers** 뷰는 공용에 표시 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EKM&#41;&#40;확장 가능 키 관리](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
  
