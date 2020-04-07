---
title: sys.credentials (거래-SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs:
- TSQL
helpviewer_keywords:
- sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f87378897256f8b4fae26b30263577bedede6175
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752894"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  각 서버 수준 자격 증명에 대해 하나의 행을 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|credential_id|**Int**|자격 증명의 ID입니다. 서버에서 중복되지 않습니다.|  
|name|**Sysname**|자격 증명의 이름입니다. 서버에서 중복되지 않습니다.|  
|credential_identity|**nvarchar(4000)**|사용할 ID의 이름입니다. 일반적으로 Windows 사용자입니다. 중복되어도 문제가 없습니다.|  
|create_date|**datetime**|자격 증명이 생성된 시간입니다.|  
|modify_date|**datetime**|자격 증명이 마지막으로 수정된 시간입니다.|  
|target_type|**은바르차르 (100)**|자격 증명의 유형입니다. 기존의 일반적인 자격 증명에 대해서는 NULL을 반환하며 암호화 공급자에 매핑된 자격 증명에 대해서는 CRYPTOGRAPHIC PROVIDER를 반환합니다. 외부 키 관리 공급자에 대한 자세한 내용은 [확장 가능한 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하십시오.|  
|target_id|**Int**|자격 증명을 매핑할 개체의 ID입니다. 기존의 일반적인 자격 증명에 대해서는 0을 반환하며 암호화 공급자에 매핑된 자격 증명에 대해서는 0이 아닌 다른 값을 반환합니다. 외부 키 관리 공급자에 대한 자세한 내용은 [확장 가능한 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하십시오.|  

## <a name="remarks"></a>설명  
데이터베이스 수준 자격 증명은 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)를 참조하십시오.
  
## <a name="permissions"></a>사용 권한  
 `VIEW ANY DEFINITION` 사용 권한 `ALTER ANY CREDENTIAL` 또는 권한이 필요합니다. 또한 보안 주체는 권한을 `VIEW ANY DEFINITION` 거부해서는 안 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [데이터베이스 엔진&#41;&#40;자격 증명](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [보안 카탈로그 보기 &#40;거래-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [데이터베이스 엔진&#41;&#40;보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
