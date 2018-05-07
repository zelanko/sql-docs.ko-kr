---
title: sys.database_scoped_configurations (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 015db41a34cdc4f22db79328e91189a77a483418
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  구성 당 한 개의 행을 포함합니다. 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|구성 옵션의 ID입니다.|  
|**name**|**nvarchar(60)**|구성 옵션의 이름입니다. 가능한 구성에 대 한 정보를 참조 하십시오. [ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)합니다.|  
|**value**|**sqlvariant**|주 복제본이 구성 옵션에 대 한 설정 값입니다.|  
|**value_for_secondary**|**sqlvariant**|보조 복제본이 구성 옵션에 대 한 설정 값입니다.|  
  
##  <a name="Permissions"></a> 사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="remarks"></a>주의  
 NULL 값으로 반환 될 때 **value_for_secondary**, 즉, 보조 PRIMARY로 설정 됩니다.  
 
 데이터베이스 범위 구성 설정은 데이터베이스와 함께 전달됩니다. 즉, 지정된 데이터베이스가 복원 또는 연결되는 경우 기존 구성 설정이 유지됩니다.
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 범위 구성 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
