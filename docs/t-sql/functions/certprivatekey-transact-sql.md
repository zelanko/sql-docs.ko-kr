---
title: CERTPRIVATEKEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs: TSQL
helpviewer_keywords: CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df513e6ce63ff49e31ad05e5a4dca0372de69c83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

인증서의 개인 키를 이진 형식으로 반환합니다. 이 함수는 세 인수를 사용합니다.
-   인증서 ID  
-   키가 사용자에게 일반 텍스트로 노출되지 않도록 함수에서 반환하는 개인 키 비트를 암호화하는 데 사용되는 암호화된 암호입니다.  
-   해독 암호(옵션)입니다. 해독 암호를 지정하면 해당 암호가 인증서의 개인 키 암호를 해독하는 데 사용되고 그렇지 않으면 데이터베이스 마스터 키가 사용됩니다.  
  
인증서의 개인 키에 대한 액세스 권한이 있는 사용자만 이 함수를 사용할 수 있습니다. 이 함수는 개인 키를 PVK 형식으로 반환합니다.
  
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
이 **certificate_id** 인증서의 합니다. Sys.certificates 또는 사용 하 여 사용할 수는 [CERT_ID &#40; Transact SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) 함수입니다. *cert_id* 형식이 **int**
  
*encryption_password*  
반환된 이진 값을 암호화하는 데 사용되는 암호입니다.
  
*decryption_password*  
반환된 이진 값 암호를 해독하는 데 사용되는 암호입니다.
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>주의  
**CERTENCODED** 및 **CERTPRIVATEKEY** 는 이진 형식으로 인증서의 다른 부분을 반환 하는 데 함께 사용 됩니다.
  
## <a name="permissions"></a>Permissions  
**CERTPRIVATEKEY** 는 누구나 사용할 수 있습니다.
  
## <a name="examples"></a>예  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20141031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
사용 하는 보다 복잡 한 예제에 대 한 **CERTPRIVATEKEY** 및 **CERTENCODED** 인증서를 다른 데이터베이스로 복사할 항목의 예제 B를 참조 하십시오. [CERTENCODED &#40; Transact SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).
  
## <a name="see-also"></a>참고 항목
[보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[Certificate&#40; 만들기 Transact SQL &#41; ](../../t-sql/statements/create-certificate-transact-sql.md) 
 [보안 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/security-functions-transact-sql.md) 
 [sys.certificates&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
