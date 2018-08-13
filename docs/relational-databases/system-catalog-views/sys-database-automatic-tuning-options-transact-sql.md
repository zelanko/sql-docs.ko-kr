---
title: sys.database_automatic_tuning_options (Transact SQL) | Microsoft 문서
description: SQL Database에서 자동 조정 옵션을 확인 하는 방법 알아보기
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e4c5cd169f7beca5cd7af3b96f1df229eb844d77
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39543339"
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_자동\_tuning_options (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  이 데이터베이스에 대 한 자동 튜닝 옵션을 반환합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|자동 튜닝 옵션의 이름입니다. 참조 [AUTOMATIC_TUNING 데이터베이스 설정 변경 &#40;Transact SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) 사용 가능한 옵션입니다.|  
|**desired_state**|**smallint**|사용자가 명시적으로 설정 하는 자동 조정 옵션을 원하는 작업 모드를 나타냅니다.<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|원하는 작업 모드를 자동 조정 옵션의 텍스트 설명입니다.<br />OFF<br />ON|  
|**actual_state**|**smallint**|자동 조정 옵션의 작업 모드를 나타냅니다.<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|자동 조정 옵션의 실제 작업 모드의 텍스트 설명입니다.<br />OFF<br />ON|  
|**reason**|**smallint**|실제 및 원하는 상태는 다른 이유를 나타냅니다.<br />2 = 사용 안 함<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|실제 및 원하는 상태 다른 이유는 이유에 대 한 텍스트 설명입니다.<br />사용 안 함 = 옵션은 시스템에서 사용할 수 있습니다.<br />QUERY_STORE_OFF = 쿼리 저장소 꺼져 있습니다.<br />QUERY_STORE_READ_ONLY = 읽기 전용 모드에서는 쿼리 저장소는<br />NOT_SUPPORTED = 가능 시간에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition| 
  
## <a name="permissions"></a>사용 권한  
 `VIEW DATABASE STATE` 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [자동 조정](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER 데이터베이스 집합 AUTOMATIC_TUNING &#40;SQL 트랜잭션&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
