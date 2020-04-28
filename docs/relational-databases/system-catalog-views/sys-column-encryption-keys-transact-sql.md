---
title: sys. column_encryption_keys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_encryption_keys
- column_encryption_keys_TSQL
- sys.column_encryption_keys_TSQL
- column_encryption_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_keys catalog view
ms.assetid: 43980dd8-b9b1-4869-a304-2c183ae8977d
author: jaszymas
ms.author: jaszymas
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4cd6b4a4cb8eeed0dd0a2a78adc2d39c6a2e895d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73593725"
---
# <a name="syscolumn_encryption_keys--transact-sql"></a>sys. column_encryption_keys (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]

  [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 문을 사용 하 여 만든 ceks (열 암호화 키)에 대 한 정보를 반환 합니다. 각 행은 CEK를 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK의 이름입니다.|  
|**column_encryption_key_id**|**int**|CEK의 ID입니다.|  
|**create_date**|**datetime**|CEK을 만든 날짜입니다.|  
|**modify_date**|**datetime**|CEK가 마지막으로 수정 된 날짜입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **VIEW ANY COLUMN ENCRYPTION KEY** 권한이 필요 합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;열 암호화 키 만들기](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;열 암호화 키 변경](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;열 암호화 키 삭제](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;열 마스터 키 만들기](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Secure enclaves를 사용 하는 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [보안 enclave를 사용한 Always Encrypted용 키 관리](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)    

  
  
