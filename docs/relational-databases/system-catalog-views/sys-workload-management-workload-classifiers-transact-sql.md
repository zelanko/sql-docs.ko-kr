---
title: sys. workload_management_workload_classifiers (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 585eb4551fb688f4f6a620729310b0245462cbff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632961"
---
# <a name="sysworkload_management_workload_classifiers-transact-sql"></a>sys. workload_management_workload_classifiers (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 작업 분류자에 대 한 세부 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|분류자의 고유 ID입니다. Null을 허용하지 않습니다.||
group_name|**sysname**|분류자가 할당 된 작업 그룹의 이름입니다. Null을 허용하지 않습니다. 조인 가능를 workload_management_workload_groups ||
name|**sysname**|분류자의 이름입니다. 는 인스턴스에 대해 고유 해야 합니다. Null을 허용하지 않습니다.||
|importance|**sysname**|는이 작업 그룹의 요청에 대 한 상대적 중요도와 공유 리소스에 대 한 작업 그룹 전체에 해당 합니다.  분류자에 지정 된 중요도는 작업 그룹 중요도 설정을 재정의 합니다. Null을 허용합니다.  Null 인 경우 작업 그룹 중요도 설정이 사용 됩니다.|낮음, below_normal, 보통 (기본값), above_normal, 높음 |
|create_time|**datetime**|분류자를 만든 시간입니다. Null을 허용하지 않습니다.||
modify_time|**datetime**|분류자가 마지막으로 수정 된 시간입니다. Null을 허용하지 않습니다.||
is_enabled|**bit**|INTERNAL||
|&nbsp;||||
  
## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.

## <a name="next-steps"></a>다음 단계

 SQL Data Warehouse 및 병렬 데이터 웨어하우스의 모든 카탈로그 뷰 목록은 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)를 참조 하세요. 작업 분류자를 만들려면 [작업 분류자 만들기](../../t-sql/statements/create-workload-classifier-transact-sql.md)를 참조 하세요. 작업 분류에 대 한 자세한 내용은 [작업 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) 를 참조 하세요.
