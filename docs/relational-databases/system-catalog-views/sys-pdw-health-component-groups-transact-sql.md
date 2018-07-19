---
title: sys.pdw_health_component_groups (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5ba27432-7a29-4420-b73d-def621c0b3ac
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 369a2934a31bbc70b9c417966b17cd6dc25425e3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38058201"
---
# <a name="syspdwhealthcomponentgroups-transact-sql"></a>sys.pdw_health_component_groups (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  구성 요소 및 장치와의 논리적 그룹에 대 한 정보를 저장합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|구성 요소 및 장치에 대 한 고유 식별자입니다.<br /><br /> 이 보기에 대 한 키입니다.|NOT NULL|  
|group_name|**nvarchar(255)**|구성 요소 및 장치에 대 한 논리적 그룹 이름입니다.|NOT NULL|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
