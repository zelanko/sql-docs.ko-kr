---
title: DATABASE_PRINCIPAL_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e0583570ce9a4d11b2e4aa6c019c8f4ccc753239
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 데이터베이스의 보안 주체 ID를 반환합니다. 보안 주체에 대한 자세한 내용은 [Principals&#40;데이터베이스 엔진#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)를 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>인수  
*principal_name*  
보안 주체를 나타내는 **sysname** 형식의 식입니다.  
*principal_name*을 생략하면 현재 사용자의 ID가 반환됩니다. 괄호가 필요합니다.
  
## <a name="return-types"></a>반환 형식
**int**  
데이터베이스 보안 주체가 없는 경우 NULL입니다.
  
## <a name="remarks"></a>Remarks  
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
  
## <a name="see-also"></a>관련 항목:
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
