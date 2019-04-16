---
title: sys.workload_management_workload_classifier_details (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
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
ms.openlocfilehash: 9afd00a887244c02849d40eed635500b06533709
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582726"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (TRANSACT-SQL) (미리 보기)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> 작업 분류 SQL Data Warehouse Gen2에서 미리 보기로 제공 됩니다. 워크 로드 관리 분류 및 중요도 미리 보기는 2019 년 4 월 9 일 이상 릴리스 날짜를 사용 하 여 빌드입니다.  사용자 워크 로드 관리 테스트에 대 한 빌드를이 날짜 이전의 사용을 피해 야 합니다.  빌드 워크 로드 관리 가능 인지를 확인 하려면 @ 선택 실행@version SQL Data Warehouse 인스턴스에 연결 된 경우.

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
