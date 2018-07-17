---
title: OPEN SYMMETRIC KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPEN SYMMETRIC KEY
- OPEN_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], opening
- OPEN SYMMETRIC KEY statement
ms.assetid: ff019a7c-c373-46c7-ac43-ffb7e2ee60b3
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 123689fada7686f68b7dce614198452355876d12
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37790084"
---
# <a name="open-symmetric-key-transact-sql"></a>OPEN SYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대칭 키를 해독하여 사용할 수 있게 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OPEN SYMMETRIC KEY Key_name DECRYPTION BY <decryption_mechanism>  
  
<decryption_mechanism> ::=  
    CERTIFICATE certificate_name [ WITH PASSWORD = 'password' ]  
    |  
    ASYMMETRIC KEY asym_key_name [ WITH PASSWORD = 'password' ]  
    |  
    SYMMETRIC KEY decrypting_Key_name  
    |  
    PASSWORD = 'decryption_password'  
```  
  
## <a name="arguments"></a>인수  
 *Key_name*  
 열려는 대칭 키의 이름입니다.  
  
 CERTIFICATE *certificate_name*  
 대칭 키 해독에 사용할 개인 키를 가지고 있는 인증서의 이름입니다.  
  
 ASYMMETRIC KEY *asym_key_name*  
 대칭 키 해독에 사용할 개인 키를 가지고 있는 비대칭 키의 이름입니다.  
  
 WITH PASSWORD ='*password*'  
 인증서나 비대칭 키의 개인 키를 암호화하는 데 사용된 암호입니다.  
  
 SYMMETRIC KEY *decrypting_key_name*  
 열려는 대칭 키를 해독하는 데 사용할 대칭 키의 이름입니다.  
  
 PASSWORD ='*password*'  
 대칭 키를 보호하는 데 사용된 암호입니다.  
  
## <a name="remarks"></a>Remarks  
 열린 대칭 키는 보안 컨텍스트가 아니라 세션에 바인딩됩니다. 열린 키는 명시적으로 닫히거나 세션이 종료될 때까지 계속 사용할 수 있습니다. 대칭 키를 연 후 컨텍스트를 전환하면 키가 계속 열려 있으며 가장된 컨텍스트에서 사용할 수 있습니다. 열린 대칭 키에 대한 정보는 [sys.openkeys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 대칭 키가 다른 키로 암호화되어 있으면 먼저 해당 키를 열어야 합니다.  
  
 대칭 키가 이미 열려 있으면 쿼리가 **NO_OP**입니다.  
  
 대칭 키를 해독하기 위해 제공한 암호, 인증서 또는 키가 올바르지 않으면 쿼리가 실패합니다.  
  
 암호화 공급자에서 만든 대칭 키는 열 수 없습니다. 암호화 공급자가 이런 키를 열고 닫으므로 이런 종류의 키를 사용한 암호화 및 해독 작업은 **OPEN** 문이 없어도 성공적으로 수행됩니다.  
  
## <a name="permissions"></a>사용 권한  
 호출자는 키에 대한 일부 사용 권한을 가지고 있어야 하며 키에 대한 VIEW DEFINITION 권한이 거부되지 않은 상태여야 합니다. 해독 메커니즘에 따라 추가 요구 사항이 따를 수도 있습니다.  
  
-   인증서에 의한 암호 해독: 인증서에 대한 CONTROL 권한이 있어야 하고 인증서의 개인 키를 암호화하는 데 사용된 암호를 알고 있어야 합니다.  
  
-   비대칭 키에 의한 암호 해독: 비대칭 키에 대한 CONTROL 권한이 있어야 하고 비대칭 키의 개인 키를 암호화하는 데 사용된 암호를 알고 있어야 합니다.  
  
-   DECRYPTION BY PASSWORD: 대칭 키를 암호화하는 데 사용된 암호 중 하나를 알고 있어야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-opening-a-symmetric-key-by-using-a-certificate"></a>1. 인증서를 사용하여 대칭 키 열기  
 다음 예에서는 `SymKeyMarketing3` 대칭 키를 열고 `MarketingCert9` 인증서의 개인 키를 사용하여 해독합니다.  
  
```  
USE AdventureWorks2012;  
OPEN SYMMETRIC KEY SymKeyMarketing3   
    DECRYPTION BY CERTIFICATE MarketingCert9;  
GO  
```  
  
### <a name="b-opening-a-symmetric-key-by-using-another-symmetric-key"></a>2. 다른 대칭 키를 사용하여 대칭 키 열기  
 다음 예에서는 `MarketingKey11` 대칭 키를 열고 `HarnpadoungsatayaSE3` 대칭 키를 사용하여 해독합니다.  
  
```  
USE AdventureWorks2012;  
-- First open the symmetric key that you want for decryption.  
OPEN SYMMETRIC KEY HarnpadoungsatayaSE3   
    DECRYPTION BY CERTIFICATE sariyaCert01;  
-- Use the key that is already open to decrypt MarketingKey11.  
OPEN SYMMETRIC KEY MarketingKey11   
    DECRYPTION BY SYMMETRIC KEY HarnpadoungsatayaSE3;  
GO   
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
