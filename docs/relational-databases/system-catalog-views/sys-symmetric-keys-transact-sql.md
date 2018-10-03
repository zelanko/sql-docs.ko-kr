---
title: sys.symmetric_keys (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- symmetric_keys
- sys.symmetric_keys
- sys.symmetric_keys_TSQL
- symmetric_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.symmetric_keys catalog view
ms.assetid: d410eae1-3a52-45de-b9a1-52d2bd93a8eb
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 57e5bc6d2959e14c7af7e5ccefddc14e9bb630ee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672951"
---
# <a name="syssymmetrickeys-transact-sql"></a>sys.symmetric_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  CREATE SYMMETRIC KEY 문으로 만든 각 대칭 키에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|키 이름입니다. C4 데이터베이스 내에서 고유합니다.|  
|**principal_id**|**int**|이 키를 소유하는 데이터베이스 보안 주체의 ID입니다.|  
|**symmetric_key_id**|**int**|키 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**key_length**|**int**|키의 길이(비트)입니다.|  
|**key_algorithm**|**char(2)**|키에 사용된 알고리즘입니다.<br /><br /> R2 = RC2<br /><br /> R4 = RC4<br /><br /> D = DES<br /><br /> D3 = Triple DES<br /><br /> DT = TRIPLE_DES_3KEY<br /><br /> DX = DESX<br /><br /> A1 = AES 128<br /><br /> A2 = AES 192<br /><br /> A3 = AES 256<br /><br /> NA = EKM 키|  
|**algorithm_desc**|**nvarchar(60)**|키에 사용된 알고리즘에 대한 설명입니다.<br /><br /> RC2<br /><br /> RC4<br /><br /> DES<br /><br /> Triple_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256<br /><br /> NULL(확장 가능 키 관리 알고리즘만 해당)|  
|**create_date**|**datetime**|키를 만든 날짜입니다.|  
|**modify_date**|**datetime**|키를 수정한 날짜입니다.|  
|**key_guid**|**uniqueidentifier**|키와 연결된 GUID(Globally Unique Identifier)입니다. 지속형 키의 GUID는 자동으로 생성되고 임시 키의 GUID는 사용자가 제공한 전달 구에서 파생됩니다.|  
|**key_thumbprint**|**sql_variant**|키의 SHA-1 해시입니다. 해시는 전역적으로 고유합니다. Extensible Key Management가 아닌 키의 경우 이 값은 NULL입니다.|  
|**provider_type**|**nvarchar(120)**|암호화 공급자의 유형입니다.<br /><br /> CRYPTOGRAPHIC PROVIDER = EKM(Extensible Key Management) <br /><br /> NULL = EKM(확장 가능 키 관리) 키가 아닌 경우|  
|**cryptographic_provider_guid**|**uniqueidentifier**|암호화 공급자의 GUID입니다. Extensible Key Management가 아닌 키의 경우 이 값은 NULL입니다.|  
|**cryptographic_provider_algid**|**sql_variant**|암호화 공급자의 알고리즘 ID입니다. Extensible Key Management가 아닌 키의 경우 이 값은 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 RC4 알고리즘은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
 **DES 알고리즘 관련 설명:**  
  
-   DESX 이름이 잘못 지정되었습니다. ALGORITHM = DESX를 사용하여 만든 대칭 키에 실제로 192비트 키를 포함하는 TRIPLE DES 암호화가 사용됩니다. DESX 알고리즘은 제공되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
-   ALGORITHM = TRIPLE_DES_3KEY를 사용하여 만든 대칭 키에 192비트 키를 포함하는 TRIPLE DES가 사용됩니다.  
  
-   ALGORITHM = TRIPLE_DES를 사용하여 만든 대칭 키에 128비트 키를 포함하는 TRIPLE DES가 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
