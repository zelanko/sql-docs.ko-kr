---
title: CERT_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1186308529dc9f4c7c7c4f792dc1e24aeb448c47
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="certid-transact-sql"></a>CERT_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

인증서 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
Cert_ID ( 'cert_name' )  
```  
  
## <a name="arguments"></a>인수  
**'** *cert_name* **'**  
데이터베이스에 있는 인증서 이름입니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>주의  
인증서 이름에 표시 되는 [sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 카탈로그 뷰에 있습니다.
  
## <a name="permissions"></a>Permissions  
인증서에 대한 몇 가지 사용 권한이 필요하며 인증서에 대한 호출자의 VIEW DEFINITION 권한이 거부되지 않아야 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 `ABerglundCert3`이라는 인증서의 ID를 반환합니다.
  
```sql
SELECT Cert_ID('ABerglundCert3');  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[sys.certificates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)
  
  

