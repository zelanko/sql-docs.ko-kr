---
description: sp_db_vardecimal_storage_format(Transact-SQL)
title: sp_db_vardecimal_storage_format (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_vardecimal_storage_format
- sp_db_vardecimal_storage_format_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_vardecimal_storage_format
- decimal data type, compressing
- compressing decimal data
- numeric data type, compressing
- database compression [SQL Server]
- table compression [SQL Server]
ms.assetid: 9920b2f7-b802-4003-913c-978c17ae4542
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e0c834696f37dd61fcc5830d9e5ef40302e5b7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469695"
---
# <a name="sp_db_vardecimal_storage_format-transact-sql"></a>sp_db_vardecimal_storage_format(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스의 현재 VarDecimal 스토리지 형식 상태를 반환하거나 데이터베이스에 VarDecimal 스토리지 형식을 사용하도록 설정합니다.  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 사용자 데이터베이스가 항상 사용하도록 설정되어 있습니다. 데이터베이스에 VarDecimal 스토리지 형식을 사용하도록 설정하는 작업은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서만 필요합니다.  
  
> [!IMPORTANT]  
>  데이터베이스의 VarDecimal 스토리지 형식 상태를 변경하면 백업 및 복구, 데이터베이스 미러링, sp_attach_db, 로그 전달 및 복제에 영향을 줄 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @dbname =] '*database_name*'  
 스토리지 형식을 변경할 데이터베이스의 이름입니다. *database_name* 는 **sysname**이며 기본값은 없습니다. 데이터베이스 이름을 생략하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 모든 데이터베이스의 VarDecimal 스토리지 형식 상태가 반환됩니다.  
  
 @vardecimal_storage_format' | '의 [=] {' OFF '}  
 VarDecimal 스토리지 형식을 사용하도록 설정할지 여부를 지정합니다. @vardecimal_storage_format은 ON 또는 OFF가 될 수 있습니다. 매개 변수는 **varchar (3)** 이며 기본값은 없습니다. 데이터베이스 이름을 제공하지만 @vardecimal_storage_format을 생략하면 지정한 데이터베이스의 현재 설정이 반환됩니다. 이 인수는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에는 영향을 주지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 데이터베이스 저장소 형식을 변경할 수 없는 경우 sp_db_vardecimal_storage_format에서 오류를 반환합니다. 데이터베이스가 이미 지정한 상태에 있으면 저장 프로시저는 영향을 주지 않습니다.  
  
 인수를 @vardecimal_storage_format 지정 하지 않으면 데이터베이스 이름 및 Vardecimal 상태 열이 반환 됩니다.  
  
## <a name="remarks"></a>설명  
 sp_db_vardecimal_storage_format은 VarDecimal 상태를 반환하지만 VarDecimal 상태를 변경할 수는 없습니다.  
  
 다음과 같은 경우 sp_db_vardecimal_storage_format이 실패합니다.  
  
-   데이터베이스에 활성 사용자가 있는 경우  
  
-   데이터베이스를 미러링에 사용할 수 있는 경우  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 VarDecimal 스토리지 형식을 지원하지 않는 경우  
  
 VarDecimal 스토리지 형식 상태를 OFF로 변경하려면 데이터베이스를 단순 복구 모드로 설정해야 합니다. 데이터베이스가 단순 복구 모드로 설정되면 로그 체인이 끊어집니다. VarDecimal 스토리지 형식 상태를 OFF로 설정한 후 전체 데이터베이스 백업을 수행합니다.  
  
 VarDecimal 데이터베이스 압축을 사용하는 테이블이 있을 경우 상태를 OFF로 변경하면 실패합니다. 테이블의 저장소 형식을 변경 하려면 [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)을 사용 합니다. VarDecimal 스토리지 형식을 사용하는 데이터베이스 테이블을 확인하려면 다음 예와 같이 `OBJECTPROPERTY` 함수를 사용하고 `TableHasVarDecimalStorageFormat` 속성을 검색합니다.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## <a name="examples"></a>예제  
 다음 코드에서는 `AdventureWorks2012` 데이터베이스에 압축을 설정하고 상태를 확인한 다음 `Sales.SalesOrderDetail` 테이블의 decimal 및 numeric 열을 압축합니다.  
  
```  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2012 ;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
