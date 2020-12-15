---
title: sys.database_automatic_tuning_options (Transact-sql) | Microsoft Docs
description: SQL Database에서 자동 조정 옵션을 확인 하는 방법에 대해 알아봅니다. 필요한 권한을 확인 하 고 사용 가능한 추가 리소스를 확인 합니다.
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4da712a23dde26d12164957718c3bdfbf89eb487
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475224"
---
# <a name="sysdatabase_automatic_tuning_options-transact-sql"></a>sys. 데이터베이스 \_ 자동 \_ Tuning_options (transact-sql)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  이 데이터베이스에 대 한 자동 튜닝 옵션을 반환 합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|자동 조정 옵션의 이름입니다. 사용 가능한 옵션은 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 을 참조 하십시오.|  
|**desired_state**|**smallint**|사용자가 명시적으로 설정 하는 자동 조정 옵션에 대 한 원하는 작업 모드를 나타냅니다.<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|자동 조정 옵션의 원하는 작업 모드에 대 한 텍스트 설명입니다.<br />OFF<br />켜기|  
|**actual_state**|**smallint**|자동 조정 옵션의 작업 모드를 나타냅니다.<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|자동 조정 옵션의 실제 작업 모드에 대 한 텍스트 설명입니다.<br />OFF<br />켜기|  
|**reason**|**smallint**|실제 및 원하는 상태가 다른 이유를 나타냅니다.<br />2 = 사용 안 함<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|실제 및 원하는 상태가 다른 이유에 대 한 텍스트 설명입니다.<br />DISABLED = 옵션이 시스템에서 사용 하지 않도록 설정 되었습니다.<br />QUERY_STORE_OFF = 쿼리 저장소 해제 되어 있습니다.<br />QUERY_STORE_READ_ONLY = 쿼리 저장소 읽기 전용 모드입니다.<br />NOT_SUPPORTED = Enterprise edition 에서만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]| 
  
## <a name="permissions"></a>사용 권한  
 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [자동 조정](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Transact-sql&#41;sys.database_query_store_options &#40;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Transact-sql&#41;sys.dm_db_tuning_recommendations &#40;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
