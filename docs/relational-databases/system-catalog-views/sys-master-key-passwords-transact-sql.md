---
description: sys.master_key_passwords(Transact-SQL)
title: sys. master_key_passwords (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c928b85aed482e774b8b180c6f97c2138f7ad0d0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539697"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  **Sp_control_dbmasterkey_password** 저장 프로시저를 사용 하 여 추가한 각 데이터베이스 마스터 키 암호에 대해 하나의 행을 반환 합니다. 마스터 키를 보호하는 데 사용된 암호는 자격 증명 저장소에 저장됩니다. 자격 증명 이름은 다음 형식을 따릅니다. # #DBMKEY_<database_family_guid>_<random_password_guid> # #. 암호는 자격 증명 암호로 저장됩니다. **Sp_control_dbmasterkey_password**를 사용 하 여 추가 된 각 암호에 대해 **sys. 자격 증명**에 행이 있습니다.  
  
 이 뷰의 각 행에는 해당 자격 증명과 연결 된 암호에 의해 보호 되는 마스터 키 인 데이터베이스의 **credential_id** 및 **family_guid** 표시 됩니다. **Credential_id** 에서 **sys. 자격 증명과** 의 조인은 **create_date** 및 자격 증명 이름과 같은 유용한 필드를 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|암호가 속한 자격 증명의 ID입니다. 이 ID는 서버 인스턴스 내에서 고유합니다.|  
|**family_guid**|**uniqueidentifier**|생성 시 원래 데이터베이스의 고유 ID입니다. 이 GUID는 데이터베이스를 복원하거나 연결한 경우뿐만 아니라 데이터베이스 이름을 변경한 경우에도 동일하게 유지됩니다.<br /><br /> 서비스 마스터 키에의 한 자동 암호 해독에 실패 하면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **family_guid** 을 사용 하 여 데이터베이스 마스터 키를 보호 하는 데 사용 되는 암호를 포함할 수 있는 자격 증명을 식별 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
