---
description: sys. database_scoped_credentials (Transact-sql)
title: sys. database_scoped_credentials (Transact-sql) | Microsoft Docs
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
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9cfc057828086f9fdc4e4425eee32c8e836593c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464818"
---
# <a name="sysdatabase_scoped_credentials-transact-sql"></a>sys. database_scoped_credentials (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  데이터베이스의 각 데이터베이스 범위 자격 증명에 대해 하나의 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|데이터베이스 범위 자격 증명의 이름입니다. 데이터베이스에서 고유 합니다.|  
|credential_id|**int**|데이터베이스 범위 자격 증명의 ID입니다. 데이터베이스에서 고유 합니다.|  
|principal_id|**int**|이 키를 소유하는 데이터베이스 보안 주체의 ID입니다.|  
|credential_identity|**nvarchar(4000)**|사용할 ID의 이름입니다. 일반적으로 Windows 사용자입니다. 중복되어도 문제가 없습니다.|  
|create_date|**datetime**|데이터베이스 범위 자격 증명이 만들어진 시간입니다.|  
|modify_date|**datetime**|데이터베이스 범위 자격 증명이 마지막으로 수정 된 시간입니다.|  
|target_type|**nvarchar (100)**|데이터베이스 범위 자격 증명의 유형입니다. `NULL`데이터베이스 범위 자격 증명에 대해를 반환 합니다.|  
|target_id|**int**|데이터베이스 범위 자격 증명이 매핑되는 개체의 ID입니다. 데이터베이스 범위 자격 증명에 대해 0을 반환 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 `CONTROL` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [자격 증명 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [Transact-sql&#41;&#40;데이터베이스 범위 자격 증명 만들기 ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE 범위 자격 증명 &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [Transact-sql&#41;&#40;데이터베이스 범위 자격 증명 삭제 ](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
