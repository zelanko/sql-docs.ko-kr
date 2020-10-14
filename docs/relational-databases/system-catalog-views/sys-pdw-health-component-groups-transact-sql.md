---
description: sys.pdw_health_component_groups (Transact-sql)
title: sys.pdw_health_component_groups (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 8ac09a94a4821713bd1ef3cb2c852251d9b811c9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036790"
---
# <a name="syspdw_health_component_groups-transact-sql"></a>sys.pdw_health_component_groups (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  구성 요소 및 장치의 논리적 그룹에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|구성 요소 및 장치에 대 한 고유 식별자입니다.<br /><br /> 이 보기의 키입니다.|NOT NULL|  
|group_name|**nvarchar(255)**|구성 요소 및 장치의 논리적 그룹 이름입니다.|NOT NULL|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
