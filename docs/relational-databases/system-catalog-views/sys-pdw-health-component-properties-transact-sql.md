---
description: sys.pdw_health_component_properties (Transact-sql)
title: sys.pdw_health_component_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: a6446cb81a33fef53ac398f9e23bd080b310ede4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439478"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys.pdw_health_component_properties (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  장치를 설명 하는 속성을 저장 합니다. 일부 속성은 장치 상태를 표시 하 고 일부 속성은 장치 자체를 설명 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|구성 요소의 속성에 대 한 고유 식별자입니다.<br /><br /> property_id 및 component_id이 보기의 키를 구성 합니다.|NOT NULL|  
|component_id|**int**|구성 요소의 ID입니다. [Sys.pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)를 참조 하세요.<br /><br /> property_id 및 component_id이 보기의 키를 구성 합니다.|NOT NULL|  
|property_name|**nvarchar(255)**|속성의 이름입니다.|NOT NULL|  
|physical_name|**nvarchar(32)**|제조업체에서 정의한 속성 이름입니다.|NOT NULL|  
|is_key|**bit**|장치 인스턴스가 고유 하거나 고유 하지 않은지 여부를 확인 합니다.|NOT NULL<br /><br /> 0-장치 인스턴스가 고유 합니다.<br /><br /> 1-장치 인스턴스가 고유 하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
