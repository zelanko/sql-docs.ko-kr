---
title: sys. pdw_health_component_status_mappings (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 32300b0f0ee89e2a135468a658bde49bb77f7c69
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627154"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>sys. pdw_health_component_status_mappings (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssDW](../../includes/ssdw-md.md)]구성 요소 상태와 제조업체에서 정의한 구성 요소 이름 간의 매핑을 정의 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|속성의 고유 식별자입니다.<br /><br /> 이 보기의 키를 property_id, component_id 및 physical_name 구성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. [Pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)을 참조 하십시오.<br /><br /> 이 보기의 키를 property_id, component_id 및 physical_name 구성 합니다.|NOT NULL|  
|physical_name|**nvarchar(32)**|제조업체에서 정의한 속성 이름입니다.<br /><br /> 이 보기의 키를 property_id, component_id 및 physical_name 구성 합니다.|NOT NULL|  
|logical_name|**nvarchar(255)**|에 정의 된 속성 이름 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 입니다.|NOT NULL<br /><br /> 0-장치 인스턴스가 고유 합니다.<br /><br /> 1-장치 인스턴스가 고유 하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
