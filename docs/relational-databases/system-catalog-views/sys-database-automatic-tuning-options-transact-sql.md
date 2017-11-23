---
title: sys.database_automatic_tuning_options (Transact SQL) | Microsoft Docs
description: "SQL 데이터베이스에서 자동 튜닝 옵션을 확인 하는 방법을 알아봅니다"
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs: TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: "24"
author: jovanpop-msft
ms.author: jovanpop
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44cc105b0edfa6c71b114800ce5be7538f9393a1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_자동\_tuning_options (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  이 데이터베이스에 대 한 자동 튜닝 옵션을 반환합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar (128)**|자동 튜닝 옵션의 이름입니다. 참조 [데이터베이스 집합 AUTOMATIC_TUNING &#40; 변경 Transact SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) 사용할 수 있는 옵션에 대 한 합니다.|  
|**desired_state**|**smallint**|사용자가 명시적으로 설정 하는 자동 튜닝 옵션을 원하는 작업 모드를 나타냅니다.<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar (60)**|자동 튜닝 옵션의 원하는 작업 모드의 텍스트 설명입니다.<br />OFF<br />ON|  
|**actual_state**|**smallint**|자동 튜닝 옵션의 작업 모드를 나타냅니다.<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar (60)**|자동 튜닝 옵션의 실제 작동 모드의 텍스트 설명입니다.<br />OFF<br />ON|  
|**이유**|**smallint**|실제 및 원하는 상태는 다른 이유를 나타냅니다.<br />2 = 사용 안 함<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar (60)**|실제 및 원하는 상태가 다른 이유는 이유를 나타내는 텍스트 설명입니다.<br />사용 하지 않도록 설정 = 옵션은 시스템에서 사용할 수 있습니다.<br />QUERY_STORE_OFF = 쿼리 저장소가 꺼져 있습니다.<br />QUERY_STORE_READ_ONLY = 쿼리 저장소가 읽기 전용 모드입니다.<br />NOT_SUPPORTED 사용 가능 = 에서만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition| 
  
## <a name="permissions"></a>Permissions  
 필요는 `VIEW DATABASE STATE` 권한.  
  
## <a name="see-also"></a>관련 항목:  
 [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [데이터베이스 집합 AUTOMATIC_TUNING &#40; 변경 Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
