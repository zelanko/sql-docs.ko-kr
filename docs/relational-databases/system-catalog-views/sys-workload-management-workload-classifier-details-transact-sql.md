---
title: sys. workload_management_workload_classifier_details (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 58b3f3315309a734a22e2732af5207b64e2f0a9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632923"
---
# <a name="sysworkload_management_workload_classifier_details-transact-sql"></a>sys. workload_management_workload_classifier_details (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  각 분류자에 대 한 세부 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|분류자의 ID입니다.  Null을 허용하지 않습니다.|
|classifier_type|**sysname**|조인 가능를 [workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md)합니다.|`membername`</br>`wlm_label`</br>`wlm_context`</br>`start_time`</br>`end_time`|
|classifier_value|**sysname**|분류자의 값입니다. Null을 허용하지 않습니다.||

## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.

## <a name="next-steps"></a>다음 단계
  
SQL Data Warehouse 및 병렬 데이터 웨어하우스의 모든 카탈로그 뷰 목록은 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)를 참조 하세요. 작업 분류자를 만들려면 [작업 분류자 만들기](../../t-sql/statements/create-workload-classifier-transact-sql.md)를 참조 하세요. 작업 분류에 대 한 자세한 내용은 SQL Data Warehouse [작업 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) 및 [작업 중요도](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) 를 참조 하세요.
