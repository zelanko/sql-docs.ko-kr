---
title: sys.key_encryptions (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba1c62078f0400436a21749b28c302d2f8a2509e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syskeyencryptions-transact-sql"></a>sys.key_encryptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  CREATE SYMMETRIC KEY 문의 ENCRYPTION BY 절을 사용하여 지정된 각 대칭 키 암호화에 대해 행을 반환합니다.  

  
|열 이름|데이터 형식|Description|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|암호화된 키의 ID입니다.|  
|**지문**|**varbinary(32)**|키 암호화에 사용되는 인증서의 SHA-1 해시이거나 대칭 키의 GUID입니다.|  
|**crypt_type**|**char(4)**|암호화 유형입니다.<br /><br /> ESKS = 대칭 키를 사용한 암호화<br /><br /> ESKP, ESP2, 또는 ESP3 암호로 암호화 됨 =<br /><br /> EPUC = 인증서를 사용한 암호화<br /><br /> EPUA = 비대칭 키를 사용한 암호화<br /><br /> ESKM = 마스터 키를 사용한 암호화|  
|**crypt_type_desc**|**nvarchar (60)**|암호화 유형의 설명입니다.<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(부터는 [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)], CSS에서 사용 하기 위해 버전 번호를 포함 합니다.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> 참고: Windows DPAPI 서비스 마스터 키를 보호 하기 위해 사용 됩니다.|  
|**crypt_property**|**varbinary(max)**|부호 있는 비트 또는 암호화된 비트입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
