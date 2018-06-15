---
title: 인덱스 디스크 공간 예 | Microsoft 문서
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46809da9211dbb4ec8704a788945b30cf5e6ca65
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32939828"
---
# <a name="index-disk-space-example"></a>인덱스 디스크 공간 예
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  인덱스를 생성하거나, 다시 작성하거나, 삭제할 때마다 해당 파일 및 파일 그룹에서 이전(원본) 및 새(대상) 구조 모두에 대한 디스크 공간이 필요합니다. 기존 구조는 인덱스 생성 트랜잭션이 커밋된 후 할당 취소됩니다. 또한 분류 작업을 위한 임시 디스크 공간도 추가로 필요할 수 있습니다. 자세한 내용은 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)을 참조하세요.  
  
 다음 예에서는 클러스터형 인덱스를 만들기 위한 디스크 공간 요구 사항을 확인합니다.  
  
 클러스터형 인덱스를 만들기 전에 다음과 같은 조건이 참인 것으로 가정합니다.  
  
-   기존 테이블(힙)에 행이 백만 개 있습니다. 각 행의 길이는 200바이트입니다.  
  
-   비클러스터형 인덱스 A에 행이 백만 개 있습니다. 각 행의 길이는 50바이트입니다.  
  
-   비클러스터형 인덱스 B에 행이 백만 개 있습니다. 각 행의 길이는 80바이트입니다.  
  
-   index create memory 옵션이 2MB로 설정되어 있습니다.  
  
-   모든 기존 및 새 인덱스의 채우기 비율 값은 80입니다. 즉, 페이지의 80%가 채워집니다.  
  
    > [!NOTE]  
    >  클러스터형 인덱스를 만들 경우 행 표시기를 새 클러스터형 인덱스 키로 대체하기 위해 두 개의 비클러스터형 인덱스를 다시 작성해야 합니다.  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>오프라인 인덱스 작업의 디스크 공간 계산  
 아래의 단계에서는 인덱스 작업 동안 사용할 임시 디스크 공간과 새 인덱스를 저장하기 위한 영구 디스크 공간을 모두 계산합니다. 결과를 반올림하고 인덱스 리프 수준의 크기만 고려하는 등 대략적으로 계산합니다. 대략적으로 계산한 경우에는 이를 나타내기 위해 물결표(~)를 사용합니다.  
  
1.  원본 구조의 크기를 확인합니다.  
  
     힙: 1백만 * 200바이트 = 200MB  
  
     비클러스터형 인덱스 A: 1백만 * 50바이트/80% = 63MB  
  
     비클러스터형 인덱스 B: 1백만 * 80바이트/80% = 100MB  
  
     기존 구조의 전체 크기: 363MB  
  
2.  대상 인덱스 구조의 크기를 확인합니다. 새 클러스터형 키 길이가 uniqueifier를 포함하여 24바이트인 것으로 가정합니다. 비클러스터형 인덱스 모두의 행 표시기(8바이트 길이)가 이 클러스터형 키로 대체됩니다.  
  
     클러스터형 인덱스: 1백만 * 200바이트/80% = 250MB  
  
     비클러스터형 인덱스 A: 1백만 * (50 – 8 + 24)바이트/80% = 83MB  
  
     비클러스터형 인덱스 B: 1백만 * (80 – 8 + 24)바이트/80% = 120MB  
  
     새 구조의 전체 크기: 453MB  
  
     인덱스 작업 동안 원본 구조와 대상 구조를 모두 지원하는 데 필요한 전체 디스크 공간은 816MB(363+453)입니다. 인덱스 작업이 커밋되면 원본 구조에 현재 할당된 공간은 할당 취소됩니다.  
  
3.  정렬을 위한 추가 임시 디스크 공간을 확인합니다.  
  
     SORT_IN_TEMPDB를 ON으로 설정하여 **tempdb** 에서 정렬하고 SORT_IN_TEMPDB를 OFF로 설정하여 대상 위치에서 정렬하기 위한 공간 요구 사항이 나와 있습니다.  
  
    1.  SORT_IN_TEMPDB을 ON으로 설정한 경우 **tempdb** 에 가장 큰 인덱스(1백만*200바이트~200MB)를 보관할 만큼 충분한 디스크 공간이 있어야 합니다. 정렬 작업에서는 채우기 비율을 고려하지 않습니다.  
  
         **tempdb** 위치의 추가 디스크 공간은 [index create memory 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 값 = 2MB와 같습니다.  
  
         SORT_IN_TEMPDB를 ON으로 설정한 경우의 전체 임시 디스크 공간 크기~202MB.  
  
    2.  SORT_IN_TEMPDB를 OFF(기본값)로 설정한 경우 2단계에서 이미 새 인덱스용으로 간주한 250MB의 디스크 공간을 정렬에 사용합니다.  
  
         대상 위치의 추가 디스크 공간은 [index create memory 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 값 = 2MB와 같습니다.  
  
         SORT_IN_TEMPDB를 OFF로 설정한 경우의 전체 임시 디스크 공간 크기~2MB.  
  
 **tempdb**를 사용하는 경우 클러스터형 및 비클러스터형 인덱스를 만드는 데 총 1018MB(816+202)가 필요합니다. **tempdb** 를 사용하면 인덱스를 만드는 데 사용되는 임시 디스크 공간이 늘어나지만 **tempdb** 가 사용자 데이터베이스와 다른 디스크 집합에 있을 때 인덱스를 만드는 데 필요한 시간이 줄어들 수 있습니다. **tempdb**사용에 대한 자세한 내용은 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)을 참조하세요.  
  
 **tempdb**를 사용하지 않는 경우 클러스터형 및 비클러스터형 인덱스를 만드는 데 총 818MB(816+2)가 필요합니다.  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>온라인 클러스터형 인덱스 작업의 디스크 공간 계산  
 온라인으로 클러스터형 인덱스를 만들거나, 삭제하거나 또는 다시 작성할 때는 임시 매핑 인덱스를 작성하고 관리하는 데 추가로 디스크 공간이 필요합니다. 이 임시 매핑 인덱스는 테이블의 각 행에 대해 하나의 레코드를 포함하고 있으며 해당 내용은 이전 및 새 책갈피 열의 합집합입니다.  
  
 온라인 클러스터형 인덱스 작업에 필요한 디스크 공간을 계산하려면 오프라인 인덱스 작업에 대한 단계를 따르고 그 결과를 아래에 나와 있는 단계의 결과에 추가하십시오.  
  
-   임시 매핑 인덱스에 대한 공간을 확인합니다.  
  
     이 예에서 이전 책갈피는 힙(8바이트)의 RID(행 ID)이고 새 책갈피는 클러스터링 키( **uniqueifier**를 포함하여 24바이트)입니다. 이전 책갈피와 새 책갈피 사이에 겹치는 열은 없습니다.  
  
     임시 매핑 인덱스 크기 = 1백만*(8바이트+24바이트)/80%~40MB  
  
     SORT_IN_TEMPDB를 OFF로 설정한 경우에는 대상 위치에서 필요한 디스크 공간에, SORT_IN_TEMPDB를 ON으로 설정한 경우에는 **tempdb** 에 이 디스크 공간을 추가해야 합니다.  
  
 자세한 내용은 [인덱스 DDL 작업의 디스크 공간 요구 사항](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)을 참조하세요.  
  
## <a name="disk-space-summary"></a>디스크 공간 요약  
 다음 표는 디스크 공간 계산 결과를 요약한 것입니다.  
  
|인덱스 작업|다음 구조의 위치에 대한 디스크 공간 요구 사항|  
|---------------------|---------------------------------------------------------------------------|  
|SORT_IN_TEMPDB = ON인 경우 오프라인 인덱스 작업|작업 중 전체 공간: 1018MB<br /><br /> -기존 테이블 및 인덱스: 363MB\*<br /><br /> -<br />                    **tempdb**: 202MB*<br /><br /> -새 인덱스: 453MB<br /><br /> 작업 후 필요한 전체 공간: 453MB|  
|SORT_IN_TEMPDB = OFF인 경우 오프라인 인덱스 작업|작업 중 전체 공간: 816MB<br /><br /> -기존 테이블 및 인덱스: 363MB*<br /><br /> -새 인덱스: 453MB<br /><br /> 작업 후 필요한 전체 공간: 453MB|  
|SORT_IN_TEMPDB = ON인 경우 온라인 인덱스 작업|작업 중 전체 공간: 1058MB<br /><br /> -기존 테이블 및 인덱스: 363MB\*<br /><br /> -<br />                    **tempdb** (매핑 인덱스 포함): 242MB*<br /><br /> -새 인덱스: 453MB<br /><br /> 작업 후 필요한 전체 공간: 453MB|  
|SORT_IN_TEMPDB = OFF인 경우 온라인 인덱스 작업|작업 중 전체 공간: 856MB<br /><br /> -기존 테이블 및 인덱스: 363MB*<br /><br /> -임시 매핑 인덱스: 40MB\*<br /><br /> -새 인덱스: 453MB<br /><br /> 작업 후 필요한 전체 공간: 453MB|  
  
 *이 공간은 인덱스 작업이 커밋된 후 할당 취소됩니다.  
  
 이 예에서는 동시 사용자 업데이트 및 삭제 작업으로 인해 만들어진 버전 레코드용으로 **tempdb** 에서 추가로 필요한 임시 디스크 공간을 고려하지 않았습니다.  
  
## <a name="related-content"></a>관련 내용  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [인덱스 작업에 필요한 트랜잭션 로그 디스크 공간](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
  
