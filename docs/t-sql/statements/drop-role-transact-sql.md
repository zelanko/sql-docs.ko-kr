---
title: DROP ROLE (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 41c2caf816ca412e4a6048713dc66f97da5155ae
ms.openlocfilehash: 86266835ec5d54ce08bdf7fe18d93dd9d4de1737
ms.contentlocale: ko-kr
ms.lasthandoff: 10/07/2017

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
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 조건에 따라 이미 있는 경우에 역할을 삭제 합니다.  
  
 *role_name*  
 데이터베이스에서 삭제할 역할을 지정합니다.  
  
## <a name="remarks"></a>주의  
 보안 개체를 소유한 역할은 데이터베이스에서 삭제할 수 없습니다. 보안 개체를 소유한 데이터베이스 역할을 삭제하려면 먼저 해당 보안 개체의 소유권을 이전하거나 데이터베이스에서 해당 보안 개체를 삭제해야 합니다. 멤버가 있는 역할은 데이터베이스에서 삭제할 수 없습니다. 멤버가 있는 역할을 삭제하려면 먼저 해당 역할의 멤버를 제거해야 합니다.  
  
 데이터베이스 역할에서 구성원을 제거 하려면 사용 하 여 [ALTER role&#40; Transact SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md).  
  
 DROP ROLE을 사용하여 고정 데이터베이스 역할을 삭제할 수 없습니다.  
  
 역할 멤버 자격에 대한 내용은 sys.database_role_members 카탈로그 뷰에서 볼 수 있습니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 사용 하 여 서버 역할을 제거 하려면 [DROP SERVER role&#40; Transact SQL &#41; ](../../t-sql/statements/drop-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 필요 **ALTER ANY ROLE** 데이터베이스에 대 한 권한 또는 **제어** 역할 또는의 멤버 자격에 대 한 권한이 **db_securityadmin**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 역할을 삭제 `purchasing` 에서 `AdventureWorks2012` 데이터베이스입니다.  
  
```  
DROP ROLE purchasing;  
GO  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER role&#40; Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  



