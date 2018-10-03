---
title: sys.pdw_health_components (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d8f0032eab0067f845ecc4f67a7b009d0ee1b676
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731079"
---
# <a name="syspdwhealthcomponents-transact-sql"></a>sys.pdw_health_components (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  모든 구성 요소 및 시스템에 존재 하는 장치에 대 한 정보를 저장 합니다. 여기에 하드웨어, 저장소 장치 및 네트워크 장치 포함 됩니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|구성 요소 또는 장치의 고유 식별자입니다.<br /><br /> 이 보기에 대 한 키입니다.|NOT NULL|  
|group_id|**정수**|이 구성 요소가 속한 논리적 구성 요소 그룹입니다. 참조 [sys.pdw_health_components (병렬 데이터 웨어하우스)](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)합니다.|NOT NULL|  
|component_name|**nvarchar(255)**|구성 요소의 이름입니다.|NOT NULL|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
