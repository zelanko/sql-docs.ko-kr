---
title: ENCRYPTBYCERT (Transact SQL) | Microsoft Docs
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
- ENCRYPTBYCERT
- ENCRYPTBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], encryption
- encryption [SQL Server], certificates
- ENCRYPTBYCERT function
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a0165a370081fc32974cccbfdfd4f97abf0e1b9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인증서의 공개 키를 사용하여 데이터를 암호화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
## <a name="arguments"></a>인수  
 *certificate_ID*  
 데이터베이스에 있는 인증서 ID입니다. **int**합니다.  
  
 *일반 텍스트*  
 인증서로 암호화될 데이터 문자열입니다.  
  
 **@cleartext**  
 형식의 변수 **nvarchar**, **char**, **varchar**, **이진**, **varbinary**, 또는 **nchar** 데이터가 들어 있는 인증서의 공개 키로 암호화 됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 이 함수는 인증서의 공개 키를 사용하여 데이터를 암호화합니다. 이러한 암호화된 텍스트는 이에 대응하는 개인 키로만 해독할 수 있습니다. 이러한 비대칭 변환은 대칭 키를 사용한 암호화 및 암호 해독에 비해 비용이 많이 듭니다. 그러므로 테이블의 사용자 데이터와 같이 큰 데이터 집합으로 작업할 경우에는 비대칭 암호화를 사용하지 않는 것이 좋습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@cleartext`에 저장된 일반 텍스트를 `JanainaCert02`라는 인증서로 암호화합니다. 암호화된 데이터는 `ProtectedData04` 테이블에 삽입됩니다.  
  
```  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DECRYPTBYCERT &#40; Transact SQL &#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP certificate&#40; Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
