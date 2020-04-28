---
title: sys. pdw_column_distribution_properties (Transact-sql)
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
ms.openlocfilehash: 5b71df1a25a9cd8480f23dc104792ad8f3e70f35
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401693"
---
# <a name="syspdw_column_distribution_properties-transact-sql"></a>sys. pdw_column_distribution_properties (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  열에 대 한 배포 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|열이 속한 개체의 ID입니다.||  
|**column_id**|**int**|열의 ID입니다.||  
|**distribution_ordinal**|**tinyint**|분산 집합 내의 서 수 (1부터 기반)입니다.|0 = 배포 열이 아닙니다. 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 이 열을 사용 하 여 부모 테이블을 배포 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
