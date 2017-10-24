---
title: "DENY 인증서 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], permissions
- permissions [SQL Server], certificates
- DENY statement, certificates
- denying permissions [SQL Server], certificates
ms.assetid: 5971ff9e-d6a4-414b-ae1f-819bc2e348f5
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62676021ffccb67725a0c2e8273f6fa1c68874bb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="deny-certificate-permissions-transact-sql"></a>DENY 인증서 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인증서에 대한 사용 권한을 거부합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DENY permission  [ ,...n ]   
    ON CERTIFICATE :: certificate_name   
    TO principal [ ,...n ]  
    [ CASCADE ]  
    [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>인수  
 *사용 권한*  
 인증서에 대해 거부할 수 있는 사용 권한을 지정합니다. 아래와 같습니다.  
  
 ON 인증서 **::***certificate_name*  
 사용 권한을 거부할 인증서를 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 *데이터베이스 _ 보안 주체*  
 사용 권한을 거부할 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
 CASCADE  
 사용 권한이 거부된 보안 주체에게 사용 권한을 부여 받은 다른 보안 주체의 사용 권한도 거부됨을 나타냅니다.  
  
 *denying_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 거부하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>주의  
 인증서는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 인증서에 대해 거부할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|인증서 권한|인증서 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CERTIFICATE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 인증서에 대한 CONTROL 권한이 필요합니다. AS 절을 사용한 경우 지정한 보안 주체가 인증서를 소유해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [APPLICATION role&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

