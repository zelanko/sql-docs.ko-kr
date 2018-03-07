---
title: VERIFYSIGNEDBYCERT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6267b5ca34c3e69af9611c2cdb4a607a7d539f00
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  디지털 서명된 데이터가 서명된 후 변경되었는지 여부를 테스트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
## <a name="arguments"></a>인수  
 *Cert_ID*  
 데이터베이스에 있는 인증서의 ID입니다. *Cert_ID* 은 **int**합니다.  
  
 *signed_data*  
 형식의 변수는 **nvarchar**, **char**, **varchar**, 또는 **nchar** 인증서로 서명 된 데이터가 들어 있는입니다.  
  
 *서명*  
 서명된 데이터에 첨부된 서명입니다. *서명* 은 **varbinary**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 서명된 데이터가 변경되지 않았으면 1을, 변경되었으면 0을 반환합니다.  
  
## <a name="remarks"></a>주의  
 **VerifySignedBycert** 지정된 된 인증서의 공개 키를 사용 하 여 데이터의 서명을 해독 하 고 암호 해독 된 데이터의 새로 계산 된 MD5 해시 값을 비교 합니다. 값이 일치하면 서명이 유효하게 됩니다.  
  
## <a name="permissions"></a>Permissions  
 인증서에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>1. 서명된 데이터가 변경되지 않았는지 확인  
 다음 예에서는 `Signed_Data`의 정보가 `Shipping04`라는 인증서로 서명된 후 변경되었는지 테스트합니다. 서명은 `DataSignature`에 저장됩니다. 인증서 `Shipping04`는 데이터베이스 내의 인증서 ID를 반환하는 `Cert_ID`로 전달됩니다. `VerifySignedByCert`가 1을 반환하면 서명이 올바른 것입니다. `VerifySignedByCert`가 0을 반환하면 `Signed_Data`의 데이터는 `DataSignature`를 생성하는 데 사용된 데이터와 다릅니다. 이 경우 `Signed_Data`가 서명된 후 변경되었거나 `Signed_Data`가 다른 인증서로 서명된 것입니다.  
  
```  
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>2. 유효한 서명을 가진 레코드만 반환  
 이 쿼리에서는 인증서 `Shipping04`를 사용하여 서명된 이후 변경되지 않은 레코드만 반환합니다.  
  
```  
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CERT_ID &#40; Transact SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40; Transact SQL &#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP certificate&#40; Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
