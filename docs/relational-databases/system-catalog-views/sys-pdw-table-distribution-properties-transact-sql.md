---
title: sys.pdw_table_distribution_properties (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8e90ef2298241dd9e59917f2ad6877a6a92b0960
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001091"
---
# <a name="syspdwtabledistributionproperties-transact-sql"></a>sys.pdw_table_distribution_properties (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  테이블에 대 한 배포 정보를 보유합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|다음에 대 한 속성을 지정 된 테이블의 ID입니다.||  
|**distribution_policy**|**tinyint**|0 = UNDEFINED<br /><br /> 1 = 없음<br /><br /> 2 = HASH<br /><br /> 3 = 복제<br /><br /> 4 = ROUND_ROBIN|복제에만 적용 됩니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]합니다.|  
|**distribution_policy_desc**|**nvarchar(60)**|정의 되지 않은 복제 NONE, 해시, SEGMENTED_HEAP|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 해시 또는 복제를 반환합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
