---
title: 준비 데이터베이스 사용
description: SQL Server PDW (병렬 데이터 웨어하우스)는 준비 데이터베이스를 사용 하 여 로드 프로세스 중에 데이터를 일시적으로 저장 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400279"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>PDW (병렬 데이터 웨어하우스)에서 준비 데이터베이스 사용
SQL Server PDW (병렬 데이터 웨어하우스)는 준비 데이터베이스를 사용 하 여 로드 프로세스 중에 데이터를 일시적으로 저장 합니다. 기본적으로 SQL Server PDW는 대상 데이터베이스를 준비 데이터베이스로 사용 하 여 테이블 조각화를 발생 시킬 수 있습니다. 테이블 조각화를 줄이기 위해 사용자 정의 준비 데이터베이스를 만들 수 있습니다. 또는 로드 오류에서 롤백하는 것이 중요 하지 않은 경우에는 fastappend 로드 모드를 사용 하 여 임시 테이블을 건너뛰고 대상 테이블에 직접 로드 하 여 성능을 향상 시킬 수 있습니다.  
  
## <a name="staging-database-basics"></a><a name="StagingDatabase"></a>준비 데이터베이스 기본 사항  
*준비 데이터베이스* 는 데이터를 어플라이언스로 로드 하는 동안 일시적으로 저장 하는 사용자가 만든 PDW 데이터베이스입니다. 준비 데이터베이스를 로드 하도록 지정 하면 어플라이언스는 먼저 데이터를 준비 데이터베이스로 복사한 다음 준비 데이터베이스의 임시 테이블에서 대상 데이터베이스의 영구 테이블로 데이터를 복사 합니다.  
  
준비 데이터베이스가 로드에 대해 지정 되지 않은 경우 SQL ServerPDW는 대상 데이터베이스에 임시 테이블을 만들고이를 사용 하 여 로드 된 데이터를 저장 한 후에 로드 된 데이터를 영구 대상 테이블에 삽입 합니다.  
  
부하가 *fastappend 모드*를 사용 하는 경우 SQL serverpdw는 임시 테이블을 모두 사용 하 여 건너뛰고 대상 테이블에 직접 데이터를 추가 합니다. Fastappend 모드는 응용 프로그램의 관점에서 임시 테이블인 테이블로 데이터를 로드 하는 ELT 시나리오의 로드 성능을 향상 시킵니다. 예를 들어 ELT 프로세스는 데이터를 임시 테이블에 로드 하 고 정리 및 duping 하 여 데이터를 처리 한 다음 대상 팩트 테이블에 데이터를 삽입할 수 있습니다. 이 경우 PDW는 응용 프로그램의 임시 테이블에 데이터를 삽입 하기 전에 먼저 내부 임시 테이블로 데이터를 로드할 필요가 없습니다. Fastappend 모드는 로드 성능을 크게 향상 시키는 추가 로드 단계를 방지 합니다. Fastappend 모드를 사용 하려면 다중 트랜잭션 모드를 사용 해야 합니다. 즉, 실패 하거나 중단 된 로드에서의 복구가 사용자의 부하 프로세스에 의해 처리 되어야 합니다.  
  
**데이터베이스의 이점 준비**  
  
준비 데이터베이스의 주요 장점은 테이블 조각화를 줄이는 것입니다. 준비 데이터베이스를 사용 하지 않는 경우 데이터는 대상 데이터베이스의 임시 테이블로 로드 됩니다. 임시 테이블을 생성 하 고 대상 데이터베이스에서 삭제 하면 임시 테이블 및 영구 테이블에 대 한 페이지가 인터리브 됩니다. 시간이 지남에 따라 테이블 조각화가 발생 하 고 성능이 저하 됩니다. 이와 대조적으로 준비 데이터베이스를 사용 하면 임시 테이블을 영구 테이블과는 별도의 파일 공간으로 만들고 삭제할 수 있습니다.  
  
**준비 데이터베이스 테이블 구조**  
  
각 데이터베이스 테이블의 저장소 구조는 대상 테이블에 따라 달라 집니다.  
  
-   힙 또는 클러스터형 columnstore 인덱스에 대 한 로드의 경우 준비 테이블은 힙입니다.  
  
-   Rowstore 클러스터형 인덱스에 대 한 로드의 경우 준비 테이블은 rowstore 클러스터형 인덱스입니다.  
  
## <a name="permissions"></a><a name="Permissions"></a>권한에  
준비 데이터베이스에 대 한 CREATE 권한 (임시 테이블을 만드는 경우)이 필요 합니다. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="best-practices-for-creating-a-staging-database"></a><a name="CreatingStagingDatabase"></a>준비 데이터베이스를 만드는 방법에 대 한 모범 사례  
  
1.  어플라이언스 당 하나의 준비 데이터베이스만 있어야 합니다. 모든 대상 데이터베이스에 대 한 모든 로드 작업에서 준비 데이터베이스를 공유할 수 있습니다.  
  
2.  준비 데이터베이스의 크기는 고객 마다 다릅니다. 처음에 어플라이언스를 채울 때 준비 데이터베이스는 초기 로드 작업을 수용할 만큼 충분히 커야 합니다. 여러 로드를 동시에 수행할 수 있으므로 이러한 로드 작업은 매우 편 합니다. 초기 로드 작업이 완료 되 고 시스템이 프로덕션 환경에 있는 경우 각 로드 작업의 크기가 더 작아질 수 있습니다. 로드가 적으면 준비 데이터베이스의 크기를 줄여서 더 작은 로드 크기를 수용할 수 있습니다. 크기를 줄이려면 준비 데이터베이스를 삭제 하 고 더 작은 크기의 할당으로 다시 만들 수 있습니다. 또는 [ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 문을 사용할 수도 있습니다.  
  
    준비 데이터베이스를 만들 때는 다음 지침을 따르십시오.  
  
    -   복제 된 테이블 크기는 동시에 로드 되는 모든 복제 된 테이블의 예상 크기 (계산 노드당) 여야 합니다. 크기는 일반적으로 25-30 GB입니다.  
  
    -   분산 테이블 크기는 동시에 로드 되는 모든 분산 테이블의 예상 크기 (어플라이언스 당) 여야 합니다.  
  
    -   로그 크기는 일반적으로 복제 된 테이블 크기와 비슷합니다.  
  
## <a name="examples"></a><a name="Examples"></a>예  
  
### <a name="a-create-a-staging-database"></a>A. 준비 데이터베이스 만들기 
다음 예에서는 어플라이언스의 모든 로드에 사용할 준비 데이터베이스 Stagedb를 만듭니다. 크기가 5 GB 인 복제 된 테이블 5 개가 각각 동시에 로드 되는 것을 예상 합니다. 이 동시성으로 인해 복제 된 크기에 대해 최소 25gb가 할당 됩니다. 100, 200, 400, 500, 500 및 550 GB 크기의 분산 된 테이블이 동시에 로드 되는 것을 예상 하 고 있다고 가정 합니다. 이 동시성으로 인해 분산 테이블 크기에 대해 2250 GB 이상이 할당 됩니다.  
  
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
  
