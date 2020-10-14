---
description: sys.pdw_health_component_status_mappings (Transact-sql)
title: sys.pdw_health_component_status_mappings (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 583790fa6b14660f2e48f39ca44c06fbbfb9ff5b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034826"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>sys.pdw_health_component_status_mappings (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  [!INCLUDE[ssDW](../../includes/ssdw-md.md)]구성 요소 상태와 제조업체에서 정의한 구성 요소 이름 간의 매핑을 정의 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|속성의 고유 식별자입니다.<br /><br /> 이 보기의 키를 property_id, component_id 및 physical_name 구성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. [Sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)를 참조 하세요.<br /><br /> 이 보기의 키를 property_id, component_id 및 physical_name 구성 합니다.|NOT NULL|  
|physical_name|**nvarchar(32)**|제조업체에서 정의한 속성 이름입니다.<br /><br /> 이 보기의 키를 property_id, component_id 및 physical_name 구성 합니다.|NOT NULL|  
|logical_name|**nvarchar(255)**|에 정의 된 속성 이름 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 입니다.|NOT NULL<br /><br /> 0-장치 인스턴스가 고유 합니다.<br /><br /> 1-장치 인스턴스가 고유 하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
