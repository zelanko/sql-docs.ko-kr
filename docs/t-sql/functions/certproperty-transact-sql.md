---
title: CERTPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0323bb93388010c1ba9c20176893674aff03760a
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112161"
---
# <a name="certproperty-transact-sql"></a>CERTPROPERTY(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

지정된 인증서 속성 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CertProperty ( Cert_ID , '<PropertyName>' )  
  
<PropertyName> ::=  
   Expiry_Date | Start_Date | Issuer_Name   
   | Cert_Serial_Number | Subject | SID | String_SID   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*Cert_ID*  
int 데이터 형식의 인증서 ID 값입니다.
  
*Expiry_Date*  
인증서 만료 날짜입니다.
  
*Start_Date*  
인증서가 유효하게 되는 날짜입니다.
  
*Issuer_Name*  
인증서 발급자의 이름입니다.
  
*Cert_Serial_Number*  
인증서 일련 번호입니다.
  
*Subject*  
인증서 주체입니다.
  
 *SID*  
인증서 SID입니다. 또한 이 인증서에 매핑된 로그인이나 사용자의 SID이기도 합니다.
  
*String_SID*  
문자열 형식의 인증서 SID입니다. 또한 이 인증서에 매핑된 로그인이나 사용자의 SID이기도 합니다.
  
## <a name="return-types"></a>반환 형식
속성 지정은 작은따옴표로 묶어야 합니다.
  
반환 형식은 함수 호출에 지정된 속성에 따라 다릅니다. **sql_variant** 반환 형식은 모든 반환 값을 래핑합니다.
-   *Expiry_Date* 및 *Start_Date*는 **datetime**을 반환합니다.  
-   *Cert_Serial_Number*, *Issuer_Name*, *String_SID* 및 *Subject*는 모두 **nvarchar**를 반환합니다.  
-   *SID*는 **varbinary**를 반환합니다.  
  
## <a name="remarks"></a>설명  
[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 카탈로그 뷰에서 인증서 정보를 참조합니다.
  
## <a name="permissions"></a>사용 권한  
인증서에 대한 적절한 사용 권한이 필요하며 인증서에 대한 호출자의 VIEW 권한이 거부되지 않아야 합니다. 인증서 사용 권한에 대한 자세한 내용은 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md) 및[GRANT CERTIFICATE PERMISSIONS &#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)을 참조하세요.
  
## <a name="examples"></a>예  
다음 예에서는 인증서 주체를 반환합니다.
  
```sql
-- First create a certificate.  
CREATE CERTIFICATE Marketing19 WITH   
    START_DATE = '04/04/2004' ,  
    EXPIRY_DATE = '07/07/2040' ,  
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
[ALTER CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)  
[CERT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)
[암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)
[sys.certificates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
[보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
