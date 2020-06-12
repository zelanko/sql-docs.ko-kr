---
title: sys. pdw_health_component_groups (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5362c1f441c3b5afee22e8cac75290b476ef8263
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627053"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>sys. pdw_health_component_groups (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  구성 요소 및 장치의 논리적 그룹에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|구성 요소 및 장치에 대 한 고유 식별자입니다.<br /><br /> 이 보기의 키입니다.|NOT NULL|  
|group_name|**nvarchar(255)**|구성 요소 및 장치의 논리적 그룹 이름입니다.|NOT NULL|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
