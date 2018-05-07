---
title: sys.dm_resource_governor_configuration (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_resource_governor_configuration_TSQL
- dm_resource_governor_configuration
- sys.dm_resource_governor_configuration
- sys.dm_resource_governor_configuration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_configuration dynamic management view
ms.assetid: c89aab6a-0434-4ce6-af8c-f8a1a3284e38
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 32b6a579619204aa0eaaae82da9f56cde9257edb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmresourcegovernorconfiguration-transact-sql"></a>sys.dm_resource_governor_configuration(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  리소스 관리자의 현재 인-메모리 구성을 포함하는 행을 반환합니다.  
  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|리소스 관리자에서 현재 사용하는 분류자 함수의 ID입니다. 사용되는 함수가 없으면 0 값을 반환합니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 이 새 요청을 분류 하는 데 사용 하는 함수와 규칙을 사용 하 여 이러한 요청을 적절 한 작업 그룹에 라우팅합니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.|  
|is_reconfiguration_pending|**bit**|ALTER RESOURCE GOVERNOR RECONFIGURE 문으로 그룹 또는 풀을 변경했는지 여부 및 인-메모리 구성에 적용되지 않았는지 여부를 나타냅니다. 반환되는 값은 다음 중 하나입니다.<br /><br /> 0 - 재구성 문이 필요 없습니다.<br /><br /> 1 - 보류 중인 구성 변경 내용을 적용하려면 재구성 문이나 서버 재시작이 필요합니다.<br /><br /> **참고:** 반환 되는 값은 항상 0 리소스 관리자를 사용 하지 않도록 설정 합니다.<br /><br /> Null을 허용하지 않습니다.|  
|max_outstanding_io_per_volume|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 볼륨당 미해결 I/O의 최대 개수입니다.|  
  
## <a name="remarks"></a>주의  
 이 동적 관리 뷰는 인-메모리 구성을 표시합니다. 저장된 구성 메타데이터를 보려면 해당 카탈로그 뷰를 사용합니다.  
  
 다음 예에서는 리소스 관리자 구성의 인-메모리 값과 저장된 메타데이터 값을 가져와서 비교하는 방법을 보여 줍니다.  
  
```  
USE master;  
go  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
go  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
go  
```  
  
## <a name="permissions"></a>Permissions  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.resource_governor_configuration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-configuration-transact-sql.md)   
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)  
  
  

