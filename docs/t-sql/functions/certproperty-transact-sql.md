---
title: CERTPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPROPERTY
- CERTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], schema names
- schemas [SQL Server], names
- CERTPROPERTY function
ms.assetid: 966c09aa-bc4e-45b0-ba53-c8381871f638
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b43b587688b574c6d6395b72c5b368b82e617fd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

지정된 인증서 속성 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
## <a name="arguments"></a>인수  
*Cert_ID*  
인증서의 ID입니다. *Cert_ID* 는 int입니다.
  
*Expiry_Date*  
인증서의 만료 날짜입니다.
  
*Start_Date*  
인증서가 유효하게 되는 날짜입니다.
  
*Issuer_Name*  
인증서의 발급자 이름입니다.
  
*Cert_Serial_Number*  
인증서 일련 번호입니다.
  
*Subject*  
인증서의 주체입니다.
  
 *SID*  
인증서 SID입니다. 또한 이 인증서에 매핑된 로그인이나 사용자의 SID이기도 합니다.
  
*String_SID*  
문자열 형식의 인증서 SID입니다. 또한 이 인증서에 매핑된 로그인이나 사용자의 SID이기도 합니다.
  
## <a name="return-types"></a>반환 형식
속성 지정은 작은따옴표로 묶어야 합니다.
  
반환 형식은 함수 호출에 지정된 속성에 따라 다릅니다. 모든 반환 값은 반환 형식의에 래핑됩니다.이 **sql_variant**합니다.
-   *Expiry_Date* 및 *Start_Date* 반환 **datetime**합니다.  
-   *Cert_Serial_Number*, *Issuer_Name*, *주체*, 및 *String_SID* 반환 **nvarchar**합니다.  
-   *SID* 반환 **varbinary**합니다.  
  
## <a name="remarks"></a>주의  
인증서에 대 한 정보는 [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 카탈로그 뷰에 있습니다.
  
## <a name="permissions"></a>Permissions  
인증서에 대한 몇 가지 사용 권한이 필요하며 인증서에 대한 호출자의 VIEW DEFINITION 권한이 거부되지 않아야 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 인증서 주체를 반환합니다.
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2007' ,  
    SUBJECT = 'Marketing Print Division';  
GO  
  
-- Now use CertProperty to examine certificate  
-- Marketing19's properties.  
DECLARE @CertSubject sql_variant;  
set @CertSubject = CertProperty( Cert_ID('Marketing19'), 'Subject');  
PRINT CONVERT(nvarchar, @CertSubject);  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[ALTER CERTIFICATE &#40; Transact SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID &#40; Transact SQL &#41; ](../../t-sql/functions/cert-id-transact-sql.md) 
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 
 [보안 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  

