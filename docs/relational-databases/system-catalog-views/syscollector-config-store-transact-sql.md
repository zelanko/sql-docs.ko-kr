---
title: syscollector_config_store (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8b637834db24c769284380f8d6edde923143f26
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorconfigstore-transact-sql"></a>syscollector_config_store(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 집합 인스턴스가 아닌 전체 데이터 수집기에 적용되는 속성을 반환합니다. 이 뷰의 각 행은 관리 데이터 웨어하우스의 이름, 관리 데이터 웨어하우스가 위치한 인스턴스 이름과 같은 특정 데이터 수집기 속성을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|parameter_name|**nvarchar(128)**|속성의 이름입니다. Null을 허용하지 않습니다.|  
|parameter_value|**sql_variant**|실제 속성 값입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>Permissions  
 뷰에 대한 SELECT 권한이나 dc_operator, dc_proxy 또는 dc_admin 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="remarks"></a>주의  
 사용 가능한 속성 목록은 고정되어 있으며 해당 값은 적절한 저장 프로시저를 사용해서만 변경할 수 있습니다. 다음 표에서는 이 뷰를 통해 표시되는 속성에 대해 설명합니다.  
  
|속성 이름|Description|  
|-------------------|-----------------|  
|CacheDirectory|수집기 유형 패키지가 임시 정보를 저장하는 파일 시스템의 디렉터리 이름입니다.<br /><br /> NULL = 기본 임시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디렉터리가 사용됩니다.|  
|CacheWindow|실패한 데이터 업로드를 위한 캐시 디렉터리의 데이터 보존 정책을 나타냅니다.<br /><br /> -1 = 실패한 모든 업로드의 데이터를 보존합니다.<br /><br /> 0 = 실패한 업로드의 데이터를 보존하지 않습니다.<br /><br /> *n*= 데이터를 보존  *n*  실패 한 이전 업로드 여기서  *n*  > = 1입니다.<br /><br /> 이 값을 변경하려면 sp_syscollector_set_cache_window 저장 프로시저를 사용하십시오.|  
|CollectorEnabled|데이터 수집기의 상태를 나타냅니다.<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용<br /><br /> 이 값을 변경하려면 sp_syscollector_enable_collector 또는 sp_syscollector_disable_collector 저장 프로시저를 사용하십시오.|  
|MDWDatabase|관리 데이터 웨어하우스의 이름입니다. 이 값을 변경하려면 sp_syscollector_set_warehouse_database_name 저장 프로시저를 사용하십시오.|  
|MDWInstance|관리 데이터 웨어하우스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. 이 값을 변경하려면 sp_syscollector_set_warehouse_instance_name 저장 프로시저를 사용하십시오.|  
  
## <a name="examples"></a>예  
 다음 예에서는 syscollector_config_store 뷰를 쿼리합니다.  
  
```sql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [sp_syscollector_set_warehouse_database_name&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [sp_syscollector_set_warehouse_instance_name&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
