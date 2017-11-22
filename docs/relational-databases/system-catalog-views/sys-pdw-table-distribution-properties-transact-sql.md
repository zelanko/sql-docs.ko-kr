---
title: sys.pdw_table_distribution_properties (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b0c8b3b637fbf46edb599e6ab39804ec16bac8b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwtabledistributionproperties-transact-sql"></a>sys.pdw_table_distribution_properties (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  테이블에 대 한 배포 정보를 보유합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|다음에 대 한 속성이 지정 된 테이블의 ID입니다.||  
|**distribution_policy**|**tinyint**|0 = 정의 되지 않은<br /><br /> 1 = 없음<br /><br /> 2 = 해시<br /><br /> 3 = 복제<br /><br /> 4 = ROUND_ROBIN|복제에만 적용 됩니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.|  
|**distribution_policy_desc**|**nvarchar (60)**|정의 되지 않은 HASH, NONE, 복제, SEGMENTED_HEAP|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]해시 또는 복제 중 하나를 반환합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
