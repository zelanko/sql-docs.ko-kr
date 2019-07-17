---
title: sys.pdw_health_component_status_mappings (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ec631e9008cc37a7b4f91ed3f530e5388bdf9c0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127496"
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  간의 매핑을 정의 합니다 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 구성 요소 상태 및 구성 요소 제조업체 정의 이름입니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|속성의 고유 식별자입니다.<br /><br /> id, component_id와 physical_name이이 보기에 대 한 키를 형성합니다.|NOT NULL|  
|component_id|**int**|ID 구성 요소입니다. 참조 [sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)합니다.<br /><br /> id, component_id와 physical_name이이 보기에 대 한 키를 형성합니다.|NOT NULL|  
|physical_name|**nvarchar(32)**|제조업체에서 정의 된 속성 이름입니다.<br /><br /> id, component_id와 physical_name이이 보기에 대 한 키를 형성합니다.|NOT NULL|  
|logical_name|**nvarchar(255)**|속성 이름에 정의 된 대로 [!INCLUDE[ssDW](../../includes/ssdw-md.md)]입니다.|NOT NULL<br /><br /> 0-장치 인스턴스는 고유 합니다.<br /><br /> 1-장치 인스턴스 고유 하지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
