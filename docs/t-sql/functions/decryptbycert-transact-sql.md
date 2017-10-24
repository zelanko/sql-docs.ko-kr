---
title: DECRYPTBYCERT (Transact SQL) | Microsoft Docs
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
- DecryptByCert_TSQL
- DECRYPTBYCERT
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], decryption
- decryption [SQL Server], certificates
- DECRYPTBYCERT function
ms.assetid: 4950d787-40fa-4e26-bce8-2cb2ceca12fb
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ebdc328e49635af823cd64e8539ee5b7cfa95c76
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인증서의 개인 키로 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>인수  
 *certificate_ID*  
 데이터베이스에 있는 인증서의 ID입니다. *인증서*_ID는 **int**합니다.  
  
 *암호 텍스트*  
 인증서의 공개 키로 암호화된 데이터의 문자열입니다.  
  
 @ciphertext  
 형식의 변수는 **varbinary** 인증서로 암호화 된 데이터가 들어 있는입니다.  
  
 *cert_password*  
 인증서의 개인 키를 암호화하는 데 사용된 암호입니다. 유니코드여야 합니다.  
  
 @cert_password  
 형식의 변수는 **nchar** 또는 **nvarchar** 는 인증서의 개인 키를 암호화 하는 데 사용 된 암호를 포함 하 합니다. 유니코드여야 합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 이 함수는 인증서의 개인 키로 데이터의 암호를 해독합니다. 비대칭 키를 사용하는 암호화 변환에는 상당한 리소스가 사용됩니다. 따라서 EncryptByCert 및 DecryptByCert는 사용자 데이터의 일상적인 암호화에 적합하지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 인증서에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `[AdventureWorks2012].[ProtectedData04]`에서 `data encrypted by certificate JanainaCert02`로 표시된 행을 선택합니다. 먼저 인증서 `JanainaCert02`의 암호로 해독하는 인증서 `pGFD4bb925DGvbd2439587y`의 기본 키로 ciphertext를 해독합니다. 암호 해독 된 데이터에서 변환 됩니다 **varbinary** 를 **nvarchar**합니다.  
  
```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ENCRYPTBYCERT &#40; Transact SQL &#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP certificate&#40; Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

