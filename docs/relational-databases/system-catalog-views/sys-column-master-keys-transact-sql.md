---
title: sys.column_master_keys (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4251ecafad275e64021729abe54fc243d9077f9f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079726"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  사용 하 여 추가 된 각 데이터베이스 마스터 키에 대 한 행을 반환 합니다 [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) 문입니다. 각 행에는 단일 열 마스터 키 (CMK)를 나타냅니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK의 이름입니다.|  
|**column_master_key_id**|**int**|열 마스터 키의 ID입니다.|  
|**create_date**|**datetime**|열 마스터 키를 만든 날짜입니다.|  
|**modify_date**|**datetime**|열 마스터 키를 마지막으로 수정한 날짜입니다.|  
|**key_store_provider_name**|**sysname**|CMK를 포함 하는 열 마스터 키 저장소에 대 한 공급자의 이름입니다. 허용된 값은<br /><br /> MSSQL_CERTIFICATE_STORE – 열 마스터 키 저장소는 인증서 저장소입니다.<br /><br /> 사용자 정의 값, 열 마스터 키 저장소를 사용자 지정 형식인 경우.|  
|**key_path**|**nvarchar(4000)**|키의 열 마스터 키 저장소 관련 경로입니다. 경로의 형식이 열 마스터 키 저장소 형식에 따라 달라 집니다. 예:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 개발자는 사용자 지정 열 마스터 키 저장소에 대 한 정의 어떤 키 경로 사용자 지정 열 마스터 키 저장소입니다.|  
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **VIEW ANY COLUMN MASTER KEY** 권한.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
