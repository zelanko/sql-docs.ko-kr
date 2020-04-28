---
title: sys. column_master_keys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b7c219b2eb56fc299857a5a189ddd9db041f2f47
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73594528"
---
# <a name="syscolumn_master_keys-transact-sql"></a>sys.column_master_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [CREATE MASTER key](../../t-sql/statements/create-column-master-key-transact-sql.md) 문을 사용 하 여 추가한 각 데이터베이스 마스터 키에 대해 하나의 행을 반환 합니다. 각 행은 단일 열 마스터 키 (CMK)를 나타냅니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK의 이름입니다.|  
|**column_master_key_id**|**int**|열 마스터 키의 ID입니다.|  
|**create_date**|**datetime**|열 마스터 키가 만들어진 날짜입니다.|  
|**modify_date**|**datetime**|열 마스터 키가 마지막으로 수정 된 날짜입니다.|  
|**key_store_provider_name**|**sysname**|CMK를 포함 하는 열 마스터 키 저장소에 대 한 공급자의 이름입니다. 허용된 값은<br /><br /> MSSQL_CERTIFICATE_STORE-열 마스터 키 저장소가 인증서 저장소 인 경우<br /><br /> 열 마스터 키 저장소가 사용자 지정 형식인 경우 사용자 정의 값입니다.|  
|**key_path**|**nvarchar(4000)**|키의 열 마스터 키 저장소 관련 경로입니다. 경로의 형식은 열 마스터 키 저장소 유형에 따라 달라 집니다. 예제:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 사용자 지정 열 마스터 키 저장소의 경우 개발자는 사용자 지정 열 마스터 키 저장소에 대 한 키 경로를 정의 해야 합니다.|  
|**allow_enclave_computations**|**bit**|열 마스터 키가 enclave로 설정 되어 있는지 여부를 나타냅니다 .이 마스터 키로 암호화 된 열 암호화 키를 서버 쪽 secure enclaves 내에서 계산 하는 데 사용할 수 있습니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.|  
|**서명**|**varbinary(max)**|**Key_path**에서 참조 하는 열 마스터 키를 사용 하 여 생성 된 **key_path** 및 **allow_enclave_computations**의 디지털 서명입니다.|


  
## <a name="permissions"></a>사용 권한  
 **VIEW ANY COLUMN MASTER KEY** 권한이 필요 합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;열 마스터 키 만들기](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [보안 enclave를 사용한 Always Encrypted용 키 관리](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
 
  
  
