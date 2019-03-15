---
title: sys.workload_management_workload_classifiers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2019
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
ms.openlocfilehash: d93876db1bb31edab2ad128a0ab8af4d4a5230cd
ms.sourcegitcommit: aa8bec762be29a29aed651d98ed4d868da85ba67
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57975377"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>sys.workload_management_workload_classifiers (TRANSACT-SQL) (미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 워크 로드 분류자에 대 한 세부 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|분류자의 고유 ID입니다. Null을 허용하지 않습니다.||
group_name|**sysname**|분류자에 할당 된 작업 그룹의 이름입니다. Null을 허용하지 않습니다. |정적 리소스 클래스</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br>동적 리소스 클래스</br>smallrc</br>mediumrc</br>Largerc</br>xlargerc|
NAME|**sysname**|분류자의 이름입니다. 인스턴스에 고유 해야 합니다. Null을 허용하지 않습니다.||
|importance|**sysname**|공유 리소스에 대 한 작업 그룹 및이 작업 그룹에서 요청의 상대적 중요도가입니다.  중요도 분류자에 지정 된 작업 그룹 중요도 설정 보다 우선 합니다.|낮음, 높으나 높음, 보통, 높으나, 높음 |
|create_time|**datetime**|분류자를 만든 시간입니다. Null을 허용하지 않습니다.||
modify_time|**datetime**|분류자를 마지막으로 수정한 시간입니다. Null을 허용하지 않습니다.||
is_enabled|**bit**|분류자 사용 되는지 여부를 표시 합니다. 기본적으로 사용 됩니다. Null을 허용하지 않습니다.|0 = 분류자를 사용할 수 없습니다 </br> 1 = 분류자를 사용 하도록 설정|
|&nbsp;||||
  
## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.

## <a name="next-steps"></a>다음 단계

 SQL Data Warehouse 및 병렬 데이터 웨어하우스에 대 한 모든 카탈로그 뷰 목록을 참조 하세요 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)합니다. 워크 로드 분류자를 참조 하세요 [워크 로드 분류자 만들기](../../t-sql/statements/create-workload-classifier-transact-sql.md)합니다. 작업 분류에 대 한 자세한 내용은 참조 하세요. [SQL 데이터 웨어하우스 작업 분류](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
