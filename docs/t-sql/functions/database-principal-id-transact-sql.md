---
title: DATABASE_PRINCIPAL_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a26dcac49e19f9a0dda738e58042c83cb8e46b8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 데이터베이스의 보안 주체 ID를 반환합니다. 보안 주체에 대 한 자세한 내용은 참조 [보안 주체 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>인수  
*principal_name*  
형식의 식 **sysname** 보안 주체를 나타내는입니다.  
때 *principal_name* 은 생략 하면 현재 사용자의 ID가 반환 됩니다. 괄호가 필요합니다.
  
## <a name="return-types"></a>반환 형식
**int**  
데이터베이스 보안 주체가 없는 경우 NULL입니다.
  
## <a name="remarks"></a>주의  
DATABASE_PRINCIPAL_ID는 SELECT 목록, WHERE 절 또는 식이 허용된 모든 곳에서 사용할 수 있습니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.
  
## <a name="examples"></a>예  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>1. 현재 사용자의 ID 검색  
다음 예에서는 현재 사용자의 데이터베이스 보안 주체 ID를 반환합니다.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>2. 지정한 데이터베이스 보안 주체의 ID 검색  
다음 예에서는 `db_owner` 데이터베이스 역할에 대한 데이터베이스 보안 주체 ID를 반환합니다.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  

