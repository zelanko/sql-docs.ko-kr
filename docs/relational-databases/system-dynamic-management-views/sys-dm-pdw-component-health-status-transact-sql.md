---
title: sys.dm_pdw_component_health_status (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f711cc87308f4987c72fec75822b10502c013016
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968405"
---
# <a name="sysdmpdwcomponenthealthstatus-transact-sql"></a>sys.dm_pdw_component_health_status (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  어플라이언스 구성 요소의 현재 상태에 대 한 정보를 보유합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||NOT NULL|  
|component_id|ssNoversion|ID 구성 요소입니다. 참조 [sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)합니다.<br /><br /> pdw_node_id, component_id, id와 component_instance_id이이 보기에 대 한 키를 형성합니다.|NOT NULL|  
|property_id|**int**|ID 속성입니다. 참조 [sys.pdw_health_component_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)합니다.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|구성 요소의 인스턴스를 식별합니다. 예를 들어, component_instance_id에서 CPU의 인스턴스를 식별 될 수 있습니다 = 'CPU1'.<br /><br /> pdw_node_id, component_id, id와 component_instance_id이이 보기에 대 한 키를 형성합니다.|NOT NULL|  
|property_value|**nvarchar(255)**|현재 속성 값입니다.|NULL|  
|update_time|**datetime**|마지막으로 메트릭을 업데이트 되었습니다.|NOT NULL|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
