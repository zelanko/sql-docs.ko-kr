---
title: sys.database_credentials (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords:
- sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 88ec73b3c29dfa8d9db0d4322b34b08ac535a621
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180209"
---
# <a name="sysdatabasecredentials-transact-sql"></a>sys.database_credentials (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  각 데이터베이스에 대해 하나의 행을 반환 범위는 데이터베이스에서 자격 증명입니다.  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 대신 합니다.    
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|데이터베이스 범위 자격 증명의 ID입니다. 데이터베이스에서 고유 합니다.|  
|name|**sysname**|데이터베이스의 이름 범위 자격 증명입니다. 데이터베이스에서 고유 합니다.|  
|credential_identity|**nvarchar(4000)**|사용할 ID의 이름입니다. 일반적으로 Windows 사용자입니다. 중복되어도 문제가 없습니다.|  
|create_date|**datetime**|데이터베이스 범위 자격 증명을 만든 시간입니다.|  
|modify_date|**datetime**|데이터베이스 범위 자격 증명 마지막으로 수정한 시간입니다.|  
|target_type|**nvarchar(100)**|유형의 데이터베이스 범위 자격 증명입니다. 데이터베이스에 대 한 NULL을 반환 범위가 자격 증명을 지정 합니다.|  
|target_id|**int**|데이터베이스 범위 자격 증명에 매핑되는 개체의 ID입니다. 자격 증명을 범위가 지정 된 데이터베이스에 대 한 0을 반환 합니다.|  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 `CONTROL` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
