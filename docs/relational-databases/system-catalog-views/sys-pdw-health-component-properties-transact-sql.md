---
title: sys. pdw_health_component_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2b31baacea8d4754fbc81e1c1c747a2c95b1402b
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627055"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys. pdw_health_component_properties (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  장치를 설명 하는 속성을 저장 합니다. 일부 속성은 장치 상태를 표시 하 고 일부 속성은 장치 자체를 설명 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|구성 요소의 속성에 대 한 고유 식별자입니다.<br /><br /> property_id 및 component_id이 보기의 키를 구성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. [Pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)을 참조 하십시오.<br /><br /> property_id 및 component_id이 보기의 키를 구성 합니다.|NOT NULL|  
|property_name|**nvarchar(255)**|속성의 이름입니다.|NOT NULL|  
|physical_name|**nvarchar(32)**|제조업체에서 정의한 속성 이름입니다.|NOT NULL|  
|is_key|**bit**|장치 인스턴스가 고유 하거나 고유 하지 않은지 여부를 확인 합니다.|NOT NULL<br /><br /> 0-장치 인스턴스가 고유 합니다.<br /><br /> 1-장치 인스턴스가 고유 하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
