---
title: CERTPRIVATEKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e409d5064cb0e807d12a76b42055a6a43c9cb7c1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "65948831"
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

이 함수는 인증서의 프라이빗 키를 이진 형식으로 반환합니다. 이 함수는 세 인수를 사용합니다.
-   인증서 ID  
-   함수에서 반환한 프라이빗 키 비트를 암호화하는 데 사용되는 암호화 암호입니다. 이 방법에서는 사용자에게 일반 텍스트로 키를 노출하지 않습니다.  
-   선택적 해독 암호입니다. 지정된 암호화 암호는 인증서의 프라이빗 키를 해독하는 데 사용됩니다. 그렇지 않은 경우 데이터베이스 마스터 키가 사용됩니다.  
  
인증서 프라이빗 키에 액세스할 수 있는 사용자만 이 함수를 사용할 수 있습니다. 이 함수는 프라이빗 키를 PVK 형식으로 반환합니다.
  
## <a name="syntax"></a>구문  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>인수  
*certificate_ID*  
인증서의 **certificate_id**입니다. sys.certificates 또는 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md) 함수에서 이 값을 구합니다. *cert_id*는 **int** 데이터 형식을 갖습니다.
  
*encryption_password*  
반환된 이진 값을 암호화하는 데 사용되는 암호입니다.
  
*decryption_password*  
반환된 이진 값 암호를 해독하는 데 사용되는 암호입니다.
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>설명  
**CERTENCODED** 및 **CERTPRIVATEKEY**를 함께 사용하여 이진 형태로 인증서의 다른 부분을 반환합니다.
  
## <a name="permissions"></a>사용 권한  
**CERTPRIVATEKEY**는 누구나 사용할 수 있습니다.
  
## <a name="examples"></a>예  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20401031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
**CERTPRIVATEKEY** 및 **CERTENCODED**를 사용하여 다른 데이터베이스로 인증서를 복사하는 더 복잡한 예는 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)의 예 2를 참조하세요.
  
## <a name="see-also"></a>참고 항목
[보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)
[보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)
[sys.certificates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
