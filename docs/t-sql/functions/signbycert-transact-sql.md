---
title: SIGNBYCERT (Transact SQL) | Microsoft Docs
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
- SIGNBYCERT
- SIGNBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text signing [SQL Server]
- encryption [SQL Server], certificates
- certificates [SQL Server], text signing
- SignByCert function
- signing text [SQL Server]
- SIGNBYCERT function
- cryptography [SQL Server], certificates
ms.assetid: b4c6bced-4473-4bae-85b9-56deced495f9
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b753e29b576d70b8c77dc40b570ab10dc314f22e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="signbycert-transact-sql"></a>SIGNBYCERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인증서를 사용하여 일반 텍스트에 서명하고 서명을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SignByCert ( certificate_ID , @cleartext [ , 'password' ] )  
```  
  
## <a name="arguments"></a>인수  
 *certificate_ID*  
 현재 데이터베이스에 있는 인증서 ID입니다. *certificate_ID* 은 **int**합니다.  
  
 *@cleartext*  
 형식의 변수는 **nvarchar**, **char**, **varchar**, 또는 **nchar** 서명 될 데이터가 들어 있는입니다.  
  
 **'** *암호* **'**  
 인증서 개인 키를 암호화할 때 사용한 암호입니다. *암호* 은 **nvarchar (128)**합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 인증서에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 텍스트에 서명 `@SensitiveData` 인증서로 `ABerglundCert07`, 먼저 암호 "pGFD4bb925DGvbd2439587y"를 사용 하 여 인증서 암호를 해독할 필요 합니다. 그런 다음 `SignedData04` 테이블에 일반 텍스트와 서명을 삽입합니다.  
  
```  
DECLARE @SensitiveData nvarchar(max);  
SET @SensitiveData = N'Saddle Price Points are   
    2, 3, 5, 7, 11, 13, 17, 19, 23, 29';  
INSERT INTO [SignedData04]  
    VALUES( N'data signed by certificate ''ABerglundCert07''',  
    @SensitiveData, SignByCert( Cert_Id( 'ABerglundCert07' ),   
    @SensitiveData, N'pGFD4bb925DGvbd2439587y' ));  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [VERIFYSIGNEDBYCERT &#40; Transact SQL &#41;](../../t-sql/functions/verifysignedbycert-transact-sql.md)   
 [CERT_ID &#40; Transact SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP certificate&#40; Transact SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

