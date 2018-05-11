---
title: 힙(클러스터형 인덱스가 없는 테이블) | Microsoft 문서
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fef08462d85ef86f76eb7647cadba6063126d7d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="heaps-tables-without-clustered-indexes"></a>힙(클러스터형 인덱스가 없는 테이블)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  힙이란 클러스터형 인덱스가 없는 테이블입니다. 힙으로 저장된 테이블에서 하나 이상의 비클러스터형 인덱스를 만들 수 있습니다. 데이터는 순서를 지정하지 않고 힙에 저장됩니다. 일반적으로 데이터는 처음에 행이 테이블에 삽입되는 순서대로 저장되지만 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 힙 안의 데이터를 이동하여 행을 효율적으로 저장할 수 있습니다. 따라서 데이터 순서는 예측할 수 없습니다. 힙에서 반환되는 행의 순서를 지정하려면 **ORDER BY** 절을 사용해야 합니다. 행의 저장소 순서를 지정하려면 테이블에서 클러스터형 인덱스를 만들어 테이블이 힙이 되지 않도록 합니다.  
  
> [!NOTE]  
>  클러스터형 인덱스를 만들지 않고 테이블을 힙으로 두면 좋은 몇 가지 이유가 있지만, 힙을 효율적으로 사용하려면 고급 기술이 요구됩니다. 힙을 테이블로 두어야 할 이유가 없는 한 대부분의 테이블에는 신중하게 선택된 클러스터형 인덱스가 있어야 합니다.  
  
## <a name="when-to-use-a-heap"></a>힙을 사용하는 경우  
 테이블이 힙이고 비클러스터형 인덱스가 없는 경우 행을 찾으려면 전체 테이블을 검사(테이블 검색)해야 합니다. 회사의 12개 지사 목록과 같이 테이블이 작은 경우에는 이렇게 하는 것이 문제가 되지 않을 수도 있습니다.  
  
 테이블을 힙으로 저장하면 파일 번호, 데이터 페이지 번호 및 페이지의 슬롯으로 구성된 RID(행 식별자)에 대한 참조로 개별 행이 식별됩니다. 행 ID는 작고 효율적인 구조입니다. 데이터 설계자는 비클러스터형 인덱스를 통해 항상 데이터에 액세스하고 RID가 클러스터형 인덱스 키보다 작은 경우에 힙을 사용합니다.  
  
## <a name="when-not-to-use-a-heap"></a>힙을 사용하지 않는 경우  
 데이터가 주로 정렬된 순서대로 반환되는 경우에는 힙을 사용하지 않습니다. 정렬 열에 대해 클러스터형 인덱스를 사용하면 정렬 작업이 필요하지 않습니다.  
  
 데이터를 자주 그룹화하는 경우 힙을 사용하지 않습니다. 데이터를 그룹화하기 전에 데이터를 정렬해야 하며, 정렬 열에 대해 클러스터형 인덱스를 사용하면 정렬 작업이 필요하지 않습니다.  
  
 테이블에서 데이터 범위를 자주 쿼리하는 경우 힙을 사용하지 않습니다.  범위 열에 대해 클러스터형 인덱스를 사용하면 전체 힙을 정렬할 필요가 없습니다.  
  
 비클러스터형 인덱스가 없고 테이블이 큰 경우 힙을 사용하지 않습니다. 힙에서 행을 찾으려면 힙의 모든 행을 읽어야 합니다.  
  
## <a name="managing-heaps"></a>힙 관리  
 힙을 만들려면 클러스터형 인덱스가 없는 테이블을 만듭니다. 테이블에 이미 클러스터형 인덱스가 포함되어 있는 경우 클러스터형 인덱스를 삭제하여 테이블을 힙에 반환합니다.  
  
 힙을 제거하려면 힙에 클러스터형 인덱스를 만듭니다.  
  
 힙을 다시 작성하여 불필요하게 사용된 공간을 복구하려면 힙에 클러스터형 인덱스를 만든 다음 해당 클러스터형 인덱스를 삭제합니다.  
  
> [!WARNING]  
>  클러스터형 인덱스를 만들거나 삭제하면 전체 테이블을 다시 쓸 필요가 없습니다. 테이블에 비클러스터형 인덱스가 포함되어 있는 경우 클러스터형 인덱스가 변경될 때마다 모든 비클러스터형 인덱스를 다시 만들어야 합니다. 따라서 힙을 클러스터형 인덱스 구조로 변경하거나 클러스터형 인덱스를 힙으로 변경하면 tempdb에서 데이터를 다시 정렬하는 데 많은 디스크 공간이 필요하고 많은 시간이 소요될 수 있습니다.  

## <a name="heap-structures"></a>힙 구조


힙이란 클러스터형 인덱스가 없는 테이블입니다. 힙에는 힙에서 사용하는 각 파티션에 대해 [의](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)sys.partitions `index_id = 0` 행이 하나 있습니다. 기본적으로 힙은 단일 파티션을 사용합니다. 힙이 다중 파티션을 사용하는 경우 각 파티션은 해당 특정 파티션에 대한 데이터를 포함하는 힙 구조를 갖습니다. 예를 들어 힙이 4개의 파티션을 사용하면 파티션마다 하나씩 총 4개의 힙 구조가 있습니다.

힙의 데이터 형식에 따라 각 힙 구조에는 특정 파티션에 대한 데이터를 저장하고 관리하는 할당 단위가 하나 이상 있습니다. 최소한 각 힙에는 파티션당 하나의 `IN_ROW_DATA` 할당 단위가 있습니다. 또한 힙에는 LOB(Large Object) 열이 포함된 경우 파티션당 하나의 `LOB_DATA` 할당 단위가 있으며 8,060바이트 행 크기 제한을 초과하는 가변 길이 열이 포함된 경우 파티션당 하나의 `ROW_OVERFLOW_DATA` 할당 단위도 있습니다.

`first_iam_page` 시스템 뷰의 `sys.system_internals_allocation_units` 열은 특정 파티션의 힙에 할당된 공간을 관리하는 IAM 페이지 체인에서 첫 번째 IAM 페이지를 가리킵니다. SQL Server에서는 IAM 페이지를 사용하여 힙 간을 이동합니다. IAM 데이터 페이지와 내부의 행은 특정 순서로 정렬되어 있지 않으며 연결되어 있지도 않습니다. 데이터 페이지 간의 유일한 논리적 연결은 IAM 페이지에 기록된 정보입니다.

> [!IMPORTANT]  
> `sys.system_internals_allocation_units` 시스템 뷰는 Microsoft SQL Server 내부 전용으로 예약되었습니다. 향후 호환성은 보장되지 않습니다.
 
IAM을 검색하여 힙의 페이지를 보유하는 익스텐트를 찾음으로써 힙의 테이블 검색 또는 연속 읽기를 수행할 수 있습니다. IAM은 익스텐트가 파일에 존재하는 순서와 동일하게 익스텐트를 나타내므로 각 파일에서 차례로 연속 힙 검색이 진행됩니다. 또한 IAM 페이지를 사용하여 검색 시퀀스를 설정하면 힙의 행이 삽입되는 순서대로 반환되지 않습니다.

다음 그림에서는 SQL Server 데이터베이스 엔진에서 IAM 페이지를 사용하여 단일 파티션 힙에서 데이터 행을 검색하는 방법을 보여 줍니다. 

![iam_heap](../../relational-databases/indexes/media/iam-heap.gif)

  
## <a name="related-content"></a>관련 내용  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [클러스터형 및 비클러스터형 인덱스 소개](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)  
  
  
