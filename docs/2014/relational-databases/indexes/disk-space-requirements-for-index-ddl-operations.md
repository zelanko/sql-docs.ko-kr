---
title: 인덱스 DDL 작업의 디스크 공간 요구 사항 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
caps.latest.revision: 38
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3d8cd697dd202ee3ba72598c6915488ea052bee4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185391"
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>Disk Space Requirements for Index DDL Operations
  디스크 공간은 인덱스를 생성, 다시 작성 또는 삭제할 때 고려해야 할 주요 사항입니다. 디스크 공간이 부족하면 성능이 저하되거나 인덱스 작업이 실패할 수도 있습니다. 이 항목에서는 인덱스 DDL(데이터 정의 언어) 작업에 필요한 디스크 공간을 결정하는 데 도움이 되는 일반 정보를 제공합니다.  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>추가 디스크 공간이 필요 없는 인덱스 작업  
 다음 인덱스 작업에는 추가 디스크 공간이 필요 없습니다.  
  
-   ALTER INDEX REORGANIZE. 로그 공간은 필요합니다.  
  
-   DROP INDEX. 비클러스터형 인덱스를 삭제할 때 추가 디스크 공간이 필요 없습니다.  
  
-   DROP INDEX. 비클러스터형 인덱스가 없는 경우 MOVE TO 절을 지정하지 않고 오프라인으로 클러스터형 인덱스를 삭제할 때 추가 디스크 공간이 필요 없습니다.  
  
-   CREATE TABLE(PRIMARY KEY 또는 UNIQUE 제약 조건)  
  
## <a name="index-operations-that-require-additional-disk-space"></a>추가 디스크 공간이 필요한 인덱스 작업  
 이외의 DDL 작업에는 모두 작업 중 사용할 추가 임시 디스크 공간과 새 인덱스 구조를 저장할 영구 디스크 공간이 필요합니다.  
  
 새 인덱스 구조가 생성되면 해당 파일과 파일 그룹에 기존(원본) 구조와 새(대상) 구조를 위한 디스크 공간이 모두 필요합니다. 기존 구조는 인덱스 생성 트랜잭션이 커밋된 후 할당 취소됩니다.  
  
 다음 인덱스 DDL 작업에서는 새 인덱스 구조가 생성되고 추가 디스크 공간이 필요합니다.  
  
-   CREATE  INDEX  
  
-   CREATE  INDEX  WITH  DROP_EXISTING  
  
-   ALTER  INDEX  REBUILD  
  
-   ALTER  TABLE  ADD  CONSTRAINT(PRIMARY  KEY  또는 UNIQUE)  
  
-   ALTER TABLE DROP CONSTRAINT(PRIMARY KEY 또는 UNIQUE)(제약 조건이 클러스터형 인덱스를 기반으로 하는 경우)  
  
-   DROP INDEX MOVE TO(클러스터형 인덱스에만 적용됨)  
  
## <a name="temporary-disk-space-for-sorting"></a>정렬을 위한 임시 디스크 공간  
 원본 및 대상 구조에 필요한 디스크 공간 이외에도 쿼리 최적화 프로그램에서 정렬이 필요 없는 실행 계획을 찾지 못할 경우 정렬을 위한 임시 디스크 공간이 필요합니다.  
  
 정렬이 필요할 경우 한 번에 한 인덱스만 정렬됩니다. 예를 들어 단일 문 내에서 클러스터형 인덱스와 관련 비클러스터형 인덱스를 다시 작성할 때 인덱스는 차례로 정렬됩니다. 따라서 정렬에 필요한 추가 임시 디스크 공간은 작업에서 가장 큰 인덱스만큼만 크면 됩니다. 대개 클러스터형 인덱스가 가장 큽니다.  
  
 SORT_IN_TEMPDB 옵션이 ON으로 설정된 경우 가장 큰 인덱스가 **tempdb**에 맞아야 합니다. 이 옵션을 사용하면 인덱스를 만드는 데 사용되는 임시 디스크 공간이 늘어나지만 **tempdb** 가 사용자 데이터베이스와 다른 디스크 집합에 있을 때 인덱스를 만드는 데 필요한 시간은 줄어들 수 있습니다.  
  
 SORT_IN_TEMPDB이 기본값인 OFF로 설정된 경우 분할된 인덱스를 비롯한 각 인덱스가 해당 대상 디스크 공간에서 정렬됩니다. 이때 새 인덱스 구조를 위한 디스크 공간만 필요합니다.  
  
 디스크 공간을 계산하는 예는 [Index Disk Space Example](index-disk-space-example.md)를 참조하십시오.  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>온라인 인덱스 작업을 위한 임시 디스크 공간  
 온라인으로 인덱스 작업을 수행하면 임시 디스크 공간이 추가로 필요합니다.  
  
 온라인으로 클러스터형 인덱스를 생성, 다시 작성 또는 삭제할 경우 기존 책갈피를 새 책갈피에 매핑하기 위해 임시 비클러스터형 인덱스가 생성됩니다. SORT_IN_TEMPDB 옵션이 ON으로 설정된 경우 **tempdb**에 이 임시 인덱스가 생성됩니다. SORT_IN_TEMPDB가 OFF로 설정된 경우 대상 인덱스와 같은 파일 그룹이나 파티션 구성표가 사용됩니다. 임시 매핑 인덱스에는 테이블의 각 행에 대한 레코드가 하나씩 들어 있고 해당 내용은 기존 책갈피 열과 새 책갈피 행을 합친 것입니다. 여기에는 두 책갈피에 모두 사용되는 열이 한 번만 포함되며 고유 식별자와 레코드 식별자가 포함됩니다. 온라인 인덱스 작업에 대한 자세한 내용은 [온라인으로 인덱스 작업 수행](perform-index-operations-online.md)을 참조하세요.  
  
> [!NOTE]  
>  DROP INDEX 문에는 SORT_IN_TEMPDB 옵션을 설정할 수 없습니다. 임시 매핑 인덱스는 항상 대상 인덱스와 같은 파일 그룹이나 파티션 구성표에 생성됩니다.  
  
 온라인 인덱스 작업은 행 버전 관리를 사용하여 다른 트랜잭션에서 수정하는 내용의 영향을 받지 않습니다. 따라서 이미 읽은 행에 대한 공유 잠금을 요청할 필요가 없습니다. 온라인 인덱스 작업 중 여러 사용자가 동시에 업데이트 및 삭제 작업을 수행하려면 **tempdb**의 버전 레코드를 위한 공간이 필요합니다. 자세한 내용은 [온라인으로 인덱스 작업 수행](perform-index-operations-online.md) 을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [Index Disk Space Example](index-disk-space-example.md)  
  
 [인덱스 작업에 필요한 트랜잭션 로그 디스크 공간](transaction-log-disk-space-for-index-operations.md)  
  
 [테이블 크기 예측](../databases/estimate-the-size-of-a-table.md)  
  
 [클러스터형 인덱스의 크기 예측](../databases/estimate-the-size-of-a-clustered-index.md)  
  
 [비클러스터형 인덱스의 크기 예측](../databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [힙 크기 예측](../databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>관련 내용  
 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [ALTER INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [DROP INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [인덱스의 채우기 비율 지정](specify-fill-factor-for-an-index.md)  
  
 [인덱스 다시 구성 및 다시 작성](indexes.md)  
  
  
