---
title: sys.database_credentials (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords:
- sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46c055e017c2cf5c06993f3e117010ac1621e175
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936743"
---
# <a name="sysdatabasecredentials-transact-sql"></a>sys.database_credentials (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  각 데이터베이스에 한 행씩 반환 범위 데이터베이스의 자격 증명.  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 대신 합니다.    
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|데이터베이스 범위 자격 증명의 ID입니다. 데이터베이스에서 고유 합니다.|  
|NAME|**sysname**|데이터베이스의 이름 범위 자격 증명. 데이터베이스에서 고유 합니다.|  
|credential_identity|**nvarchar(4000)**|사용할 ID의 이름입니다. 일반적으로 Windows 사용자입니다. 고유 하지 않아도 됩니다.|  
|create_date|**datetime**|데이터베이스 범위 자격 증명을 만든 시간입니다.|  
|modify_date|**datetime**|데이터베이스 범위 자격 증명을 마지막으로 수정 된 시간입니다.|  
|target_type|**nvarchar(100)**|유형의 데이터베이스 범위 자격 증명. 범위 자격 증명을 데이터베이스에 대 한 NULL을 반환 합니다.|  
|target_id|**int**|데이터베이스 범위 자격 증명에 매핑되는 개체의 ID입니다. 범위 자격 증명을 데이터베이스에 대 한 0을 반환 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 `CONTROL` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
