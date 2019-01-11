---
title: 메모리 액세스에 최적화된 개체의 스토리지 만들기 및 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1d6bb42e4b35a74ef2bd6eefb85ea81b0ed18e40
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416974"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>메모리 액세스에 최적화된 개체의 스토리지 만들기 및 관리
  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 엔진은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 통합되어 있으므로 메모리 최적화 테이블과 기존의 디스크 기반 테이블을 모두 같은 데이터베이스에 포함할 수 있습니다. 그러나 메모리 최적화 테이블의 스토리지 구조는 디스크 기반 테이블과는 다릅니다.  
  
 디스크 기반 테이블용 스토리지의 주요 특성은 다음과 같습니다.  
  
-   파일이 하나 이상 포함된 파일 그룹에 매핑됩니다.  
  
-   각 파일은 8페이지 익스텐트로 구분되며 각 페이지의 크기는 8,000바이트입니다.  
  
-   여러 테이블에서 익스텐트를 공유할 수는 있지만 할당된 페이지와 테이블 또는 인덱스 간에는 일대일 매핑이 적용됩니다. 즉, 둘 이상의 테이블이나 인덱스에서 가져온 행을 한 페이지에 포함할 수는 없습니다.  
  
-   데이터는 필요에 따라 메모리(버퍼 풀)로 이동되며 수정되거나 새로 생성된 페이지는 디스크에 비동기로 기록되므로 대개 임의의 IO가 생성됩니다.  
  
 메모리 최적화 테이블용 스토리지의 주요 특성은 다음과 같습니다.  
  
-   메모리 최적화 모든 테이블은 메모리 최적화 파일 그룹에 매핑됩니다. 이 파일 그룹은 파일 스트림 파일 그룹을 사용하여 생성됩니다.  
  
-   페이지가 없고 데이터가 행으로 유지됩니다.  
  
-   메모리 최적화 테이블의 모든 변경 내용은 활성 파일에 추가되는 방식으로 저장됩니다. 파일 읽기와 파일에 쓰기는 모두 순차적으로 수행됩니다.  
  
-   업데이트는 삭제 후 삽입으로 구현됩니다. 삭제된 행은 스토리지에서 즉시 제거되지 않으며, 삭제된 행은 [메모리 액세스에 최적화된 테이블에 대한 내구성](memory-optimized-tables.md)에서 설명한 대로 정책을 기반으로 하여 MERGE라는 백그라운드 프로세스를 통해 제거됩니다.  
  
-   디스크 기반 테이블과 달리 메모리 최적화 테이블용 스토리지는 압축되지 않습니다. 압축된(ROW 또는 PAGE) 디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션할 때는 크기 변경을 고려해야 합니다.  
  
-   메모리 최적화 테이블은 지속형일 수도 있고 그렇지 않을 수도 있습니다. 메모리 액세스에 최적화된 내구성이 있는 테이블의 스토리지만 구성해야 합니다.  
  
 이 섹션에서는 검사점 파일 쌍 외에도 메모리 최적화 테이블의 데이터가 저장되는 방법의 다른 측면에 대해 설명합니다.  
  
 이 섹션의 항목:  
  
-   [메모리 액세스에 최적화된 테이블 저장소 구성](configuring-storage-for-memory-optimized-tables.md)  
  
-   [메모리 액세스에 최적화된 파일 그룹](the-memory-optimized-filegroup.md)  
  
-   [메모리 액세스에 최적화된 테이블에 대한 내구성](memory-optimized-tables.md)  
  
-   [메모리 액세스에 최적화된 테이블에 대한 검사점 작업](checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [메모리 액세스에 최적화된 개체에 대한 내구성 정의](defining-durability-for-memory-optimized-objects.md)  
  
-   [디스크 기반 테이블 저장소와 메모리 액세스에 최적화된 테이블 저장소 비교](comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
-   [데이터 및 델타 파일 쌍에 대한 병합 모니터링 및 문제 해결](../../database-engine/monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs.md)  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
