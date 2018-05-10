---
title: sys.dm_pdw_component_health_alerts (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e39ad74d0600927985a1bf06bf3b986f97a0bd4
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  저장소는 어플라이언스 구성 요소에 대해 경고를 이전에 발생합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|고유 식별자는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 노드.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, 및 alert_instance_id이이 보기에 대 한 키를 형성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. 참조 [sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)합니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, 및 alert_instance_id이이 보기에 대 한 키를 형성 합니다.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id, 및 alert_instance_id이이 보기에 대 한 키를 형성 합니다.|NOT NULL|  
|alert_id|**int**|경고 유형에 대 한 ID입니다. 참조 [sys.pdw_health_alerts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)합니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, 및 alert_instance_id이이 보기에 대 한 키를 형성 합니다.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|지정된 된 경고의 인스턴스를 식별합니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, 및 alert_instance_id이이 보기에 대 한 키를 형성 합니다.|NOT NULL|  
|previous_value|**nvarchar(255)**|경고가 StatusChange 유형의 경우 사용 합니다. 이전 구성 요소 상태입니다. 값은 임계값 유형의 경고에 대 한 NULL입니다. 참조 [sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 경고 유형 목록에 대 한 합니다.|NULL|  
|current_value|**nvarchar(255)**|경고가 StatusChange 유형의 경우 사용 합니다. 현재 구성 요소 상태입니다. 값은 임계값 유형의 경고에 대 한 NULL입니다. 참조 [sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 경고 유형 목록에 대 한 합니다.|NULL|  
|create_time|**datetime**|경고가 생성 된 날짜 및 시간입니다.|NOT NULL|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
