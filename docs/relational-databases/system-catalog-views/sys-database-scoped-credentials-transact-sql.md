---
title: sys.database_scoped_credentials (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.database_scoped_credentials
- sys.database_scoped_credentials_TSQL
- database_scoped_credentials
- database_scoped_credentials_TSQL
helpviewer_keywords:
- sys.database_scoped_credentials catalog view
ms.assetid: 68e8aa6b-bcdc-42aa-93d8-d498f724c188
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d3718357b68aa47bbc32e4d975a546f3e86cb73
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814841"
---
# <a name="sysdatabasescopedcredentials-transact-sql"></a>sys.database_scoped_credentials (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  각 데이터베이스에 한 행씩 반환 범위 데이터베이스의 자격 증명.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|데이터베이스 범위 자격 증명의 ID입니다. 데이터베이스에서 고유 합니다.|  
|NAME|**sysname**|데이터베이스의 이름 범위 자격 증명. 데이터베이스에서 고유 합니다.|  
|credential_identity|**nvarchar(4000)**|사용할 ID의 이름입니다. 일반적으로 Windows 사용자입니다. 중복되어도 문제가 없습니다.|  
|create_date|**datetime**|데이터베이스 범위 자격 증명을 만든 시간입니다.|  
|modify_date|**datetime**|데이터베이스 범위 자격 증명을 마지막으로 수정 된 시간입니다.|  
|target_type|**nvarchar(100)**|유형의 데이터베이스 범위 자격 증명. 반환 `NULL` 데이터베이스 범위 자격 증명입니다.|  
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
  
  
