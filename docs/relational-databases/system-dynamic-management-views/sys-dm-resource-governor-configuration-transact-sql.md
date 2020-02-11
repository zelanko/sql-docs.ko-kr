---
title: sys. dm_resource_governor_configuration (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6d37a6ad94056007dd7c941d53ce52b4b84498a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73983296"
---
# <a name="sysdm_resource_governor_configuration-transact-sql"></a>sys.dm_resource_governor_configuration(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  리소스 관리자의 현재 인-메모리 구성을 포함하는 행을 반환합니다.  
  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|리소스 관리자에서 현재 사용하는 분류자 함수의 ID입니다. 사용되는 함수가 없으면 0 값을 반환합니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 이 함수는 새 요청을 분류 하 고 규칙을 사용 하 여 이러한 요청을 적절 한 작업 그룹으로 라우팅하는 데 사용 됩니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.|  
|is_reconfiguration_pending|**bit**|ALTER RESOURCE GOVERNOR RECONFIGURE 문으로 그룹 또는 풀을 변경했는지 여부 및 인-메모리 구성에 적용되지 않았는지 여부를 나타냅니다. 반환되는 값은 다음 중 하나입니다.<br /><br /> 0 - 재구성 문이 필요 없습니다.<br /><br /> 1 - 보류 중인 구성 변경 내용을 적용하려면 재구성 문이나 서버 재시작이 필요합니다.<br /><br /> **참고:** Resource Governor 사용 하지 않도록 설정 된 경우 반환 되는 값은 항상 0입니다.<br /><br /> Null을 허용하지 않습니다.|  
|max_outstanding_io_per_volume|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 볼륨당 미해결 I/O의 최대 개수입니다.|  
  
## <a name="remarks"></a>설명  
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
  
## <a name="permissions"></a>사용 권한  
 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [resource_governor_configuration &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-configuration-transact-sql.md)   
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)  
  
  

