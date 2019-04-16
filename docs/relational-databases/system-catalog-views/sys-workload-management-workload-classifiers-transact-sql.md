---
title: sys.workload_management_workload_classifiers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
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
ms.openlocfilehash: 3b023654728375aee76bfb0c4434a8413dc81e7d
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582566"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>sys.workload_management_workload_classifiers (TRANSACT-SQL) (미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> 작업 분류 SQL Data Warehouse Gen2에서 미리 보기로 제공 됩니다. 워크 로드 관리 분류 및 중요도 미리 보기는 2019 년 4 월 9 일 이상 릴리스 날짜를 사용 하 여 빌드입니다.  사용자 워크 로드 관리 테스트에 대 한 빌드를이 날짜 이전의 사용을 피해 야 합니다.  빌드 워크 로드 관리 가능 인지를 확인 하려면 @ 선택 실행@version SQL Data Warehouse 인스턴스에 연결 된 경우.

 워크 로드 분류자에 대 한 세부 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|분류자의 고유 ID입니다. Null을 허용하지 않습니다.||
group_name|**sysname**|분류자에 할당 된 작업 그룹의 이름입니다. Null을 허용하지 않습니다. |정적 리소스 클래스</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br> </br>동적 리소스 클래스</br>smallrc</br>mediumrc</br>largerc</br>xlargerc|
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
