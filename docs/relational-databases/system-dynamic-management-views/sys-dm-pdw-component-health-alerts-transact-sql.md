---
description: sys.dm_pdw_component_health_alerts (Transact-sql)
title: sys.dm_pdw_component_health_alerts (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 97202c1532685abfe6d12c1dfe0f44642ecc5723
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482644"
---
# <a name="sysdm_pdw_component_health_alerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  어플라이언스 구성 요소에 이전에 발급 된 경고를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|노드의 고유 식별자 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 입니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. [Sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)를 참조 하세요.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|alert_id|**int**|경고 유형의 ID입니다. [Sys.pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)를 참조 하세요.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|alert_instance_id|**nvarchar (36)**|지정 된 경고의 인스턴스를 식별 합니다.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id 및 alert_instance_id이 뷰의 키를 구성 합니다.|NOT NULL|  
|previous_value|**nvarchar(255)**|경고가 StatusChange 형식일 때 사용 됩니다. 이전 구성 요소 상태입니다. 임계값 유형의 경고에 대 한 값은 NULL입니다. 경고 유형 목록은 [sys.pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 를 참조 하세요.|NULL|  
|current_value|**nvarchar(255)**|경고가 StatusChange 형식일 때 사용 됩니다. 현재 구성 요소 상태입니다. 임계값 유형의 경고에 대 한 값은 NULL입니다. 경고 유형 목록은 [sys.pdw_health_alerts &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) 를 참조 하세요.|NULL|  
|create_time|**datetime**|경고가 생성 된 시간 및 날짜입니다.|NOT NULL|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
