---
title: DROP ASYMMETRIC KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ASYMMETRIC KEY
- DROP_ASYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], removing
- removing asymmetric keys
- encryption [SQL Server], asymmetric keys
- DROP ASYMMETRIC KEY statement
- dropping asymmetric keys
- deleting asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: bf94ac07-9b62-4318-b55b-1eed8f3a1ac6
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f3737521ee178f9b7287f8d86e269973841d74c6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-asymmetric-key-transact-sql"></a>DROP ASYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스에서 비대칭 키를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP ASYMMETRIC KEY key_name [ REMOVE PROVIDER KEY ]  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 데이터베이스에서 삭제할 비대칭 키의 이름입니다.  
  
 REMOVE PROVIDER KEY  
 EKM(Extensible Key Management) 장치에서 EKM 키를 제거합니다. 확장 가능 키 관리에 대 한 자세한 내용은 참조 하세요. [확장 가능 키 관리 &#40; Ekm&#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>주의  
 데이터베이스의 대칭 키를 암호화하는 데 사용되거나 사용자 또는 로그인이 매핑된 비대칭 키는 삭제할 수 없습니다. 이러한 비대칭 키를 삭제하려면 먼저 이 키에 매핑된 모든 사용자나 로그인을 삭제해야 합니다. 또한 비대칭 키로 암호화된 모든 대칭 키를 삭제하거나 변경해야 합니다. DROP ENCRYPTION 옵션을 사용할 수 있습니다 [ALTER SYMMETRIC KEY](../../t-sql/statements/alter-symmetric-key-transact-sql.md) 를 비대칭 키 암호화를 제거 합니다.  
  
 비대칭 키의 메타 데이터를 사용 하 여 액세스할 수는 [sys.asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md) 카탈로그 뷰에 있습니다. 데이터베이스 내에서 키 자체를 직접 볼 수는 없습니다.  
  
 EKM(Extensible Key Management) 장치의 EKM 키에 비대칭 키를 매핑하고 REMOVE PROVIDER KEY 옵션을 지정하지 않으면 데이터베이스에서는 키가 삭제되지만 장치에서는 삭제되지 않으며 경고가 발생합니다.  
  
## <a name="permissions"></a>Permissions  
 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `MirandaXAsymKey6` 데이터베이스에서 `AdventureWorks2012` 비대칭 키를 제거합니다.  
  
```  
USE AdventureWorks2012;  
DROP ASYMMETRIC KEY MirandaXAsymKey6;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER SYMMETRIC key&#40; Transact SQL &#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)  
  
  

