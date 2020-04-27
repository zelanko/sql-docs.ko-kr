---
title: 힙(클러스터형 인덱스가 없는 테이블) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de71808c54264639aea82fe66cf23a7bfd6bd0ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63162156"
---
# <a name="heaps-tables-without-clustered-indexes"></a>힙(클러스터형 인덱스가 없는 테이블)
  힙이란 클러스터형 인덱스가 없는 테이블입니다. 힙으로 저장된 테이블에서 하나 이상의 비클러스터형 인덱스를 만들 수 있습니다. 데이터는 순서를 지정하지 않고 힙에 저장됩니다. 일반적으로 데이터는 처음에 행이 테이블에 삽입되는 순서대로 저장되지만 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 힙 안의 데이터를 이동하여 행을 효율적으로 저장할 수 있습니다. 따라서 데이터 순서는 예측할 수 없습니다. 힙에서 반환되는 행의 순서를 지정하려면 `ORDER BY` 절을 사용해야 합니다. 행의 스토리지 순서를 지정하려면 테이블에서 클러스터형 인덱스를 만들어 테이블이 힙이 되지 않도록 합니다.  
  
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
  
## <a name="related-content"></a>관련 내용  
 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [클러스터형 및 비클러스터형 인덱스 소개](clustered-and-nonclustered-indexes-described.md)  
  
  
