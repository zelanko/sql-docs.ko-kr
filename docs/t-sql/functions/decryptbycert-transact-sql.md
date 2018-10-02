---
title: DECRYPTBYCERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ff7cd9e82f2e70e39b02f10726acbae657ad670c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741201"
---
# <a name="decryptbycert-transact-sql"></a>DECRYPTBYCERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 인증서의 개인 키를 사용하여 암호화된 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByCert ( certificate_ID , { 'ciphertext' | @ciphertext }   
    [ , { 'cert_password' | @cert_password } ] )  
```  
  
## <a name="arguments"></a>인수  
 *certificate_ID*  
데이터베이스에 있는 인증서 ID입니다. *certificate_ID*는 **int** 데이터 형식을 갖습니다.  
  
 *ciphertext*  
인증서의 공개 키로 암호화된 데이터의 문자열입니다.  
  
 @ciphertext  
인증서로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
 *cert_password*  
인증서의 개인 키를 암호화하는 데 사용되는 암호입니다. *cert_password*는 유니코드 데이터 형식을 가져야 합니다.  
  
 @cert_password  
인증서의 개인 키를 암호화하는 데 사용되는 암호를 포함하는 **nchar** 또는 **nvarchar** 형식의 변수입니다. *@cert_password*는 유니코드 데이터 형식을 가져야 합니다.  

## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>Remarks  
이 함수는 인증서의 개인 키로 데이터의 암호를 해독합니다. 비대칭 키를 사용하는 암호화 변환에는 상당한 리소스가 사용됩니다. 따라서 개발자는 일상적인 사용자 데이터 암호화/암호 해독에 [ENCRYPTBYCERT](./encryptbycert-transact-sql.md) 및 DECRYPTBYCERT의 사용을 피하는 것이 좋습니다.  

## <a name="permissions"></a>Permissions  
`DECRYPTBYCERT`는 인증서에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
이 예제는 인증서 `JanainaCert02`로 원래 암호화된 데이터로 표시되는 `[AdventureWorks2012].[ProtectedData04]`에서 행을 선택합니다. 예제는 먼저 인증서 `pGFD4bb925DGvbd2439587y`의 암호로 인증서 `JanainaCert02`의 개인 키를 암호 해독합니다. 그런 다음, 예제에서는 이 개인 키로 암호 텍스트를 암호 해독합니다. 예제는 암호가 해독된 데이터를 **varbinary**에서 **nvarchar**로 변환합니다.  

```  
SELECT convert(nvarchar(max), DecryptByCert(Cert_Id('JanainaCert02'),  
    ProtectedData, N'pGFD4bb925DGvbd2439587y'))  
FROM [AdventureWorks2012].[ProtectedData04]   
WHERE Description   
    = N'data encrypted by certificate '' JanainaCert02''';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ENCRYPTBYCERT&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
