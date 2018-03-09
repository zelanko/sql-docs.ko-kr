---
title: "데이터베이스 범위 이름 자격 증명 (Transact SQL) DROP | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96016adf491a2869054068339a7fba64f8e7fedb
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="drop-database-scoped-credential-transact-sql"></a>DROP 데이터베이스 SCOPED 자격 증명 (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  서버에서 데이터베이스 범위 자격 증명을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>인수  
 *credential_name*  
 서버에서 제거할 데이터베이스 범위 자격 증명의 이름이입니다.  
  
## <a name="remarks"></a>주의  
 데이터베이스 범위 자격 증명 자체를 삭제 하지 않고 연결 된 데이터베이스 범위 자격 증명 암호를 삭제 하려면 사용 [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md)합니다.  
  
 데이터베이스 범위 자격 증명에 대 한 정보에 표시 되는 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 `ALTER` 자격 증명에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 라는 데이터베이스 범위 자격 증명을 제거 `SalesAccess`합니다.  
  
```sql  
DROP DATABASE SCOPED CREDENTIAL AppCred;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [자격 증명 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [DATABASE SCOPED credential&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED credential&#40; Transact SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
