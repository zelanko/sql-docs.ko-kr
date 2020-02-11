---
title: sys. dm_pdw_component_health_active_alerts (Transact-sql
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 90531889d3e510d342ff39abdf069f75f3c371aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401715"
---
# <a name="sysdm_pdw_component_health_active_alerts-transact-sql"></a>sys. dm_pdw_component_health_active_alerts (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  구성 요소에 대 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 한 활성 경고를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 노드의 고유 식별자입니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. [Pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)을 참조 하십시오.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|alert_id|**int**|경고 유형의 ID입니다. [Pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)을 참조 하십시오.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|지정 된 경고의 인스턴스를 식별 합니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|current_value|**nvarchar(255)**|경고가 StatusChange 형식일 때 사용 됩니다. 현재 구성 요소 상태입니다. 임계값 유형의 경고에 대 한 값은 NULL입니다. 경고 유형 목록은 [pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 을 참조 하십시오.|NULL|  
|previous_value|**nvarchar(255)**|경고가 StatusChange 형식일 때 사용 됩니다. 이전 구성 요소 상태입니다. 임계값 유형의 경고에 대 한 값은 NULL입니다. 경고 유형 목록은 [pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 을 참조 하십시오.|NULL|  
|create_time|**datetime**|경고가 생성 된 시간 및 날짜입니다.|NOT NULL|  
  
 이 뷰에서 유지 되는 최대 행에 대 한 자세한 내용은의 "최소 및 최대 값"을 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]참조 하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
