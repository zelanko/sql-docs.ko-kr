---
title: sys.master_key_passwords (거래-SQL) | 마이크로 소프트 문서
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 926acd9beb00102e19dbc2844e282d74bc890915
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752904"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  **sp_control_dbmasterkey_password** 저장 프로시저를 사용하여 추가된 각 데이터베이스 마스터 키 암호에 대한 행을 반환합니다. 마스터 키를 보호하는 데 사용된 암호는 자격 증명 저장소에 저장됩니다. 자격 증명 이름은 다음과 같습니다: ##DBMKEY_<random_password_guid random_password_guid ##random_password_guid>_ database_family_guid><>_<. 암호는 자격 증명 암호로 저장됩니다. **sp_control_dbmasterkey_password**사용하여 추가된 각 암호에 대해 **sys.credentials에 행이 있습니다.**  
  
 이 보기의 각 행은 해당 자격 증명과 연결된 암호로 보호되는 마스터 키의 **데이터베이스** credential_id **및 데이터베이스의 family_guid** 보여 줍니다. **credential_id** **sys.credentials를** 가진 조인은 **create_date** 및 자격 증명 이름과 같은 유용한 필드를 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**credential_id**|**Int**|암호가 속한 자격 증명의 ID입니다. 이 ID는 서버 인스턴스 내에서 고유합니다.|  
|**family_guid**|**uniqueidentifier**|생성 시 원래 데이터베이스의 고유 ID입니다. 이 GUID는 데이터베이스를 복원하거나 연결한 경우뿐만 아니라 데이터베이스 이름을 변경한 경우에도 동일하게 유지됩니다.<br /><br /> 서비스 마스터 키에 의한 자동 암호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 해독에 실패하면 **family_guid** 사용하여 데이터베이스 마스터 키를 보호하는 데 사용되는 암호를 포함할 수 있는 자격 증명을 식별합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰 &#40;거래-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [보안 카탈로그 보기 &#40;거래-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [대칭 키 &#40;거래 SQL&#41;만들기](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [암호화 계층 구조](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
