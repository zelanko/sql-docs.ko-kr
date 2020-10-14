---
description: sys.pdw_column_distribution_properties (Transact-sql)
title: sys.pdw_column_distribution_properties (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 83bdcf74beb32e7fd5425ca56dcdd79c7c0d3d6c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035786"
---
# <a name="syspdw_column_distribution_properties-transact-sql"></a>sys.pdw_column_distribution_properties (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  열에 대 한 배포 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|열이 속한 개체의 ID입니다.||  
|**column_id**|**int**|열의 ID입니다.||  
|**distribution_ordinal**|**tinyint**|분산 집합 내의 서 수 (1부터 기반)입니다.|0 = 배포 열이 아닙니다. 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 이 열을 사용 하 여 부모 테이블을 배포 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Azure Synapse Analytics 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
