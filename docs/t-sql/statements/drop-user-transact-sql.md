---
description: DROP USER(Transact-SQL)
title: DROP USER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_USER_TSQL
- DROP USER
dev_langs:
- TSQL
helpviewer_keywords:
- dropping users
- DROP USER statement
- deleting users
- database user removal [SQL Server]
- removing users
- users [SQL Server], removing
ms.assetid: d6e0e21a-7568-4321-b6d6-bcfba183a719
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26c3f98d2b8279d13911e37ca373044fef0c609b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496805"
---
# <a name="drop-user-transact-sql"></a>DROP USER(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 데이터베이스에서 사용자를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP USER [ IF EXISTS ] user_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP USER user_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 이미 있는 경우에만 사용자를 조건적으로 삭제합니다.  
  
 *user_name*  
 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.  
  
## <a name="remarks"></a>설명  
 보안 개체를 소유하는 사용자는 데이터베이스에서 삭제할 수 없습니다. 보안 개체를 소유하는 데이터베이스 사용자를 삭제하려면 먼저 해당 보안 개체의 소유권을 삭제하거나 이전해야 합니다.  
  
 게스트 사용자는 삭제할 수 없지만 master 또는 tempdb 이외의 데이터베이스 내에서 REVOKE CONNECT FROM GUEST를 실행하면 게스트 사용자의 CONNECT 권한이 취소되므로 사용할 수 없게 됩니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY USER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `AbolrousHazem` 데이터베이스에서 `AdventureWorks2012` 데이터베이스 사용자를 제거합니다.  
  
```  
DROP USER AbolrousHazem;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
