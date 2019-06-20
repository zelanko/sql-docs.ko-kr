---
title: sys.workload_management_workload_classifier_details (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 0e693c97ad2702eefb0e02084b6c49d138ef934a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65089520"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql"></a>sys.workload_management_workload_classifier_details (Transact SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  각 분류자에 대 한 세부 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|분류자의 ID입니다. 에 조인 가능 [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md)합니다. Null을 허용하지 않습니다.|
|classifier_type|**sysname**|분류 수행 되는 엔터티입니다. Null을 허용하지 않습니다.|MEMBERNAME|
|classifier_value|**sysname**|분류자의 값입니다. Null을 허용하지 않습니다.||

## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.

## <a name="next-steps"></a>다음 단계
  
 SQL Data Warehouse 및 병렬 데이터 웨어하우스에 대 한 모든 카탈로그 뷰 목록을 참조 하세요 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)합니다. 워크 로드 분류자를 참조 하세요 [워크 로드 분류자 만들기](../../t-sql/statements/create-workload-classifier-transact-sql.md)합니다. 작업 분류에 대 한 자세한 내용은 SQL Data Warehouse를 참조 하세요 [워크 로드 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) 및 [작업 중요도](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
