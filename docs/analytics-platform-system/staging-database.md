---
title: 준비 데이터베이스-병렬 데이터 웨어하우스를 사용 하 여 | Microsoft Docs
description: 준비 데이터베이스를 사용 하 여 로드 프로세스 중에 일시적으로 데이터를 저장 하는 SQL Server 병렬 데이터 웨어하우스 (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 73822c1495fa5f83d9a8ba37325a025999f94530
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544661"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>병렬 데이터 웨어하우스 (PDW)에서 준비 데이터베이스를 사용 하 여
준비 데이터베이스를 사용 하 여 로드 프로세스 중에 일시적으로 데이터를 저장 하는 SQL Server 병렬 데이터 웨어하우스 (PDW). 기본적으로 SQL Server PDW 대상 데이터베이스를 사용 하 여 준비 데이터베이스와 테이블 조각화 될 수 있습니다. 테이블 조각화를 줄이려면 사용자 정의 준비 데이터베이스를 만들 수 있습니다. 또는의 로드 오류는 롤백 문제가 없는 경우 임시 테이블을 건너뛰는 중 대상 테이블에 직접 로드 하 여 성능을 향상 하는 fastappend 로드 모드를 사용할 수 있습니다.  
  
## <a name="StagingDatabase"></a>준비 데이터베이스 기본 사항  
A *준비 데이터베이스* 어플라이언스에 로드 될 동안 일시적으로 데이터를 저장 하는 사용자가 만든 PDW 데이터베이스입니다. 부하에 대해 준비 데이터베이스를 지정 하면 어플라이언스에 먼저 데이터 준비 데이터베이스에 복사한 다음 대상 데이터베이스에 영구 테이블에는 준비 데이터베이스의 임시 테이블에서 데이터를 복사 합니다.  
  
준비 데이터베이스 부하에 대해을 지정 하지 않으면 SQL ServerPDW 대상 데이터베이스에서 임시 테이블을 만들고 하는 영구 대상 테이블에 로드 된 데이터를 삽입 하기 전에 로드 된 데이터를 저장 하는 데 사용 합니다.  
  
로드를 사용 하는 경우는 *fastappend 모드*, SQL ServerPDW 모두 임시 테이블을 사용 하 여 건너뛰고 데이터가 대상 테이블에 직접 추가 합니다. Fastappend 모드에는 응용 프로그램 관점에서 임시 테이블은 테이블에 데이터가 로드 되는 위치 ELT 시나리오에 대 한 부하 성능이 향상 됩니다. 예를 들어 ELT 프로세스 수를 임시 테이블에 데이터를 로드, 정리 및 duping 취소 하 여 데이터 처리 및 다음 대상 팩트 테이블에 데이터를 삽입할 합니다. 이 경우에 필요 없는 PDW에 대 한 첫 번째 로드를 내부 임시 테이블 데이터를 응용 프로그램의 임시 테이블에 데이터를 삽입 하기 전에. Fastappend 모드 부하 성능이 크게 향상 되는, 추가 부하 단계를 방지 합니다. Fastappend 모드를 사용 하려면 복구 실패 했거나 중단 부하에서은 자신의 로드 프로세스에서 처리 되어야 즉 다중 트랜잭션 모드를 사용 해야 합니다.  
  
**준비 데이터베이스의 이점**  
  
준비 데이터베이스의 주요 이점은 테이블 조각화를 줄이려면입니다. 준비 데이터베이스를 사용 하지 않는 경우 데이터는 대상 데이터베이스에서 임시 테이블에 로드 됩니다. 임시 테이블을 생성 및 삭제는 대상 데이터베이스에서 임시 테이블 및 영구 테이블에 대 한 페이지 인터리브 됩니다. 시간이 지남에 따라 테이블 조각화 발생 하 고 성능이 저하 됩니다. 반면, 준비 데이터베이스 하면 임시 테이블이 생성 하 및 영구 테이블 보다는 별도 파일 공간에 삭제 됩니다.  
  
**준비 데이터베이스 테이블 구조**  
  
각 데이터베이스 테이블에 대 한 저장소 구조는 대상 테이블에 따라 달라 집니다.  
  
-   힙 또는 클러스터형된 columnstore 인덱스에 대 한 부하를 준비 테이블은 힙입니다.  
  
-   Rowstore 클러스터형된 인덱스에 대 한 부하를 준비 테이블은 클러스터형된 rowstore 인덱스입니다.  
  
## <a name="Permissions"></a>Permissions  
준비 데이터베이스 만들기 권한이 있으면 (임시 테이블 작성용)이 있어야 합니다. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>준비 데이터베이스를 만들기 위한 최선의 방법  
  
1.  어플라이언스 당 하나의 준비 데이터베이스 여야 합니다. 모든 대상 데이터베이스에 대 한 모든 로드 작업에서 준비 데이터베이스를 공유할 수 있습니다.  
  
2.  준비 데이터베이스의 크기는 고객 다릅니다. 처음에 기기를 처음 채울 때 준비 데이터베이스는 초기 로드 작업을 수용할 수 있어야 합니다. 이 작업을 로드는 여러 로드를 동시에 발생할 수 있으므로 큰 경우가 많습니다. 초기 로드 작업을 완료 한 후 시스템을 프로덕션 환경에서 각 부하 작업 크기가 작을 것입니다. 부하는 small 때 더 작은 부하 크기에 맞게 준비 데이터베이스의 크기를 줄일 수 있습니다. 크기를 줄이려면 준비 데이터베이스를 삭제 하 고 더 작은 크기 할당 다시 만들 수 있습니다 또는 있습니다 사용할 수는 [ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md) 문.  
  
    준비 데이터베이스를 만들 때 다음 지침을 따르세요.  
  
    -   복제 된 테이블 크기 계산 노드당 동시에 로드 하는 모든 복제 된 테이블의 예상된 크기 여야 합니다. 크기는 일반적으로 25-30 GB입니다.  
  
    -   분산된 테이블 크기의 예상된 크기는 동시에 로드 하는 모든 분산된 테이블의 어플라이언스 당 이어야 합니다.  
  
    -   로그 크기는 복제 된 테이블 크기 일반적으로 비슷합니다.  
  
## <a name="Examples"></a>예제  
  
### <a name="a-create-a-staging-database"></a>1. 준비 데이터베이스 만들기 
다음 예에서는 데이터베이스를 만든 준비 Stagedb, 어플라이언스에 대 한 모든 부하와 함께 사용할 합니다. 복제 된 5가 5 GB를 동시에 로드 하는 크기의 테이블을 예측 한다고 가정 합니다. 이 동시성으로 인해 25GB 적어도 복제 된 크기에 대 한 할당 됩니다. 6 개 100 크기의 테이블을 분산 하는 예측 결과 가정 200, 400, 500, 500 및 550GB 동시에 로드 됩니다. 이 동시성으로 인해 2250 GB 이상 분산된 테이블 크기에 대 한 할당 됩니다.  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
