---
title: sys. credentials (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
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
ms.openlocfilehash: da427117b2282c9014ff0171e1a7c29f7490940e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078750"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  각 서버 수준 자격 증명에 대해 하나의 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|자격 증명의 ID입니다. 서버에서 중복되지 않습니다.|  
|name|**sysname**|자격 증명의 이름입니다. 서버에서 중복되지 않습니다.|  
|credential_identity|**nvarchar(4000)**|사용할 ID의 이름입니다. 일반적으로 Windows 사용자입니다. 중복되어도 문제가 없습니다.|  
|create_date|**datetime**|자격 증명이 생성된 시간입니다.|  
|modify_date|**datetime**|자격 증명이 마지막으로 수정된 시간입니다.|  
|target_type|**nvarchar (100)**|자격 증명의 유형입니다. 기존의 일반적인 자격 증명에 대해서는 NULL을 반환하며 암호화 공급자에 매핑된 자격 증명에 대해서는 CRYPTOGRAPHIC PROVIDER를 반환합니다. 외부 키 관리 공급자에 대 한 자세한 내용은 [EKM&#41;&#40;확장 가능 키 관리 ](../../relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조 하세요.|  
|target_id|**int**|자격 증명을 매핑할 개체의 ID입니다. 기존의 일반적인 자격 증명에 대해서는 0을 반환하며 암호화 공급자에 매핑된 자격 증명에 대해서는 0이 아닌 다른 값을 반환합니다. 외부 키 관리 공급자에 대 한 자세한 내용은 [EKM&#41;&#40;확장 가능 키 관리 ](../../relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조 하세요.|  

## <a name="remarks"></a>설명  
데이터베이스 수준 자격 증명은 [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)를 참조 하세요.
  
## <a name="permissions"></a>사용 권한  
 사용 권한 `VIEW ANY DEFINITION` 또는 `ALTER ANY CREDENTIAL` 사용 권한 중 하나가 필요 합니다. 또한 보안 주체에 게 권한이 거부 `VIEW ANY DEFINITION` 되지 않아야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
