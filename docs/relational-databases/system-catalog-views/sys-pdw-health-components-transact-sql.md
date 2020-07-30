---
title: sys. pdw_health_components (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 83bea79a009e25d54f9d0ae589936de7fed7d94a
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396045"
---
# <a name="syspdw_health_components-transact-sql"></a>sys. pdw_health_components (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  시스템에 존재 하는 모든 구성 요소 및 장치에 대 한 정보를 저장 합니다. 여기에는 하드웨어, 저장 장치 및 네트워크 장치가 포함 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|구성 요소 또는 장치의 고유 식별자입니다.<br /><br /> 이 보기의 키입니다.|NOT NULL|  
|group_id|**정수**|이 구성 요소가 속한 논리적 구성 요소 그룹입니다. [Pdw_health_components (병렬 데이터 웨어하우스)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)를 참조 하세요.|NOT NULL|  
|component_name|**nvarchar(255)**|구성 요소의 이름입니다.|NOT NULL|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
