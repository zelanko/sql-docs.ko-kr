---
title: DROP ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ROLE
- DROP_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting roles
- database roles [SQL Server], removing
- removing roles
- DROP ROLE statement
- roles [SQL Server], removing
- dropping roles
ms.assetid: 1f6f13ae-56a2-4ef1-93f5-8e6151b83e1d
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 45ad478b02f5abfeea07024a74af90b02ecc808a
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361473"
---
# <a name="drop-role-transact-sql"></a>DROP ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  데이터베이스에서 역할을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
DROP ROLE [ IF EXISTS ] role_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP ROLE role_name  
```  
  
## <a name="arguments"></a>인수  
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 역할을 조건적으로 삭제합니다.  
  
 *role_name*  
 데이터베이스에서 삭제할 역할을 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 보안 개체를 소유한 역할은 데이터베이스에서 삭제할 수 없습니다. 보안 개체를 소유한 데이터베이스 역할을 삭제하려면 먼저 해당 보안 개체의 소유권을 이전하거나 데이터베이스에서 해당 보안 개체를 삭제해야 합니다. 멤버가 있는 역할은 데이터베이스에서 삭제할 수 없습니다. 멤버가 있는 역할을 삭제하려면 먼저 해당 역할의 멤버를 제거해야 합니다.  
  
 데이터베이스 역할에서 멤버를 제거하려면 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)를 사용합니다.  
  
 DROP ROLE을 사용하여 고정 데이터베이스 역할을 삭제할 수 없습니다.  
  
 역할 멤버 자격에 대한 내용은 sys.database_role_members 카탈로그 뷰에서 볼 수 있습니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 서버 역할을 제거하려면 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)를 사용합니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 **ALTER ANY ROLE** 권한 또는 역할에 대한 **CONTROL** 권한 또는 **db_securityadmin**의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스에서 `purchasing` 데이터베이스 역할을 삭제합니다.  
  
```  
DROP ROLE purchasing;  
GO  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  


