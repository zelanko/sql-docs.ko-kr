---
title: sys.certificates (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- certificates
- certificates_TSQL
- sys.certificates_TSQL
- sys.certificates
dev_langs:
- TSQL
helpviewer_keywords:
- sys.certificates catalog view
ms.assetid: e5046102-a65c-401e-b80d-05636884dec9
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f5aaf349d050b2b1b1d27ae3067f003186c8c6eb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180319"
---
# <a name="syscertificates-transact-sql"></a>sys.certificates(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스의 각 인증서에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|인증서의 이름입니다. 데이터베이스 내에서 고유합니다.|  
|**certificate_id**|**int**|인증서의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**principal_id**|**int**|이 인증서를 소유하는 데이터베이스 보안 주체의 ID입니다.|  
|**pvt_key_encryption_type**|**char(2)**|개인 키가 암호화된 방법입니다.<br /><br /> NA = 인증서에 개인 키가 없음<br /><br /> MK = 개인 키가 마스터 키로 암호화됨<br /><br /> PW = 개인 키가 사용자 정의 암호로 암호화됨<br /><br /> SK = 개인 키가 서비스 마스터 키로 암호화됨|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|개인 키를 암호화하는 방법에 대한 설명입니다.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**is_active_for_begin_dialog**|**bit**|1인 경우 이 인증서는 암호화된 서비스 대화 상자를 초기화하는 데 사용됩니다.|  
|**issuer_name**|**nvarchar(442)**|인증서 발급자의 이름입니다.|  
|**cert_serial_number**|**nvarchar(64)**|인증서의 일련 번호입니다.|  
|**sid**|**varbinary(85)**|이 인증서의 로그인 SID입니다.|  
|**string_sid**|**nvarchar(128)**|이 인증서의 로그인 SID를 나타내는 문자열입니다.|  
|**subject**|**nvarchar(4000)**|이 인증서의 주체입니다.|  
|**expiry_date**|**datetime**|인증서 만료 날짜입니다.|  
|**start_date**|**datetime**|인증서가 유효하게 되는 날짜입니다.|  
|**지문**|**varbinary(32)**|인증서의 SHA-1 해시입니다. SHA-1 해시는 전역적으로 고유합니다.|  
|**attested_by**|**nvarchar(260)**|시스템에서만 사용됩니다.|  
|pvt_key_last_backup_date|**datetime**|인증서의 개인 키를 마지막으로 내보낸 날짜 및 시간입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
  
