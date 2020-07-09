---
title: CERT_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERT_ID
- CERT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], certificates
- CERT_ID function
- IDs [SQL Server], certificates
- certificates [SQL Server], IDs
ms.assetid: 59cc06f5-272e-4936-8afe-afba7aba8eea
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8c3c6361737f8aefd3e6e9eac0af7caf29684b97
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732747"
---
# <a name="cert_id-transact-sql"></a>CERT_ID(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 함수는 인증서의 ID 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>인수  
**'** *cert_name* **'**  

데이터베이스의 인증서 이름입니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>설명  
[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 카탈로그 뷰는 인증서 이름을 보여 줍니다.
  
## <a name="permissions"></a>사용 권한  
인증서에 대한 적절한 사용 권한이 필요하며 인증서에 대한 호출자의 VIEW DEFINITION 권한이 거부되지 않아야 합니다. 인증서 사용 권한에 대한 자세한 내용은 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md#permissions)을 참조하세요.
  
## <a name="examples"></a>예  
이 예에서는 `ABerglundCert3`이라는 인증서의 ID를 반환합니다.
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[sys.certificates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  
