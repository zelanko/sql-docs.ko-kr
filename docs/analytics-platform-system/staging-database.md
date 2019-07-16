---
title: 준비 데이터베이스-병렬 데이터 웨어하우스를 사용 하 여 | Microsoft Docs
description: SQL Server 병렬 데이터 웨어하우스 (PDW)는 스테이징 데이터베이스를 사용 하 여 로드 프로세스 중에 일시적으로 데이터를 저장 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 824ad4dedee0224023f50b6855b2de1e53581304
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960030"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>병렬 데이터 웨어하우스 (PDW)에서 준비 데이터베이스를 사용 하 여
SQL Server 병렬 데이터 웨어하우스 (PDW)는 스테이징 데이터베이스를 사용 하 여 로드 프로세스 중에 일시적으로 데이터를 저장 합니다. 기본적으로 SQL Server PDW 대상 데이터베이스를 사용 하 여 준비 데이터베이스와 테이블 조각화를 유발할 수 있습니다. 테이블 조각화를 줄이기 위해 사용자 정의 준비 데이터베이스를 만들 수 있습니다. 또는 로드 실패에서 롤백 문제가 없는 경우 임시 테이블을 건너뛰고 대상 테이블에 직접 로드 하 여 성능을 향상 하는 fastappend 로드 모드를 사용할 수 있습니다.  
  
## <a name="StagingDatabase"></a>준비 데이터베이스 기본 사항  
A *준비 데이터베이스* 데이터베이스가 사용자가 만든 PDW 어플라이언스에 로드 되는 동안 일시적으로 데이터를 저장 하는 합니다. 부하에 대해 준비 데이터베이스를 지정 하면 어플라이언스 먼저 준비 데이터베이스에 데이터를 복사 하 고 대상 데이터베이스에 영구 테이블에 준비 데이터베이스의 임시 테이블에서 데이터를 복사 합니다.  
  
부하에 대해 준비 데이터베이스를 지정 하지 않으면 SQL ServerPDW 대상 데이터베이스에 임시 테이블을 만들고 사용 하 여 영구 대상 테이블에 로드 된 데이터를 삽입 하기 전에 로드 된 데이터를 저장 합니다.  
  
로드를 사용 하는 경우는 *fastappend 모드*, SQL ServerPDW 임시 테이블을 완전히 사용을 건너뛰고 대상 테이블에 직접 데이터를 추가 합니다. Fastappend 모드에는 응용 프로그램의 관점에서 임시 테이블을 테이블 데이터는 로드 하는 ELT 시나리오에 대 한 로드 성능이 향상 됩니다. 예를 들어는 ELT 프로세스 수 임시 테이블로 데이터를 로드, 데이터 정리, duping 취소를 처리 및 대상 팩트 테이블에 데이터를 삽입 한 다음 이 경우 필요 없는 PDW에 대 한 내부 임시 테이블에 데이터를 먼저 로드할 응용 프로그램의 임시 테이블에 데이터를 삽입 하기 전에 합니다. Fastappend 모드 로드 성능이 크게 향상 되는 추가 로드 단계를 피할 수 있습니다. Fastappend 모드를 사용 하려면 복구 실패 했거나 중단 된 부하에서 고유한 로드 프로세스에서 처리 해야 하는 다중 트랜잭션 모드를 사용 해야 합니다.  
  
**준비 데이터베이스 혜택**  
  
준비 데이터베이스의 이점은 테이블 조각화를 줄일 것입니다. 준비 데이터베이스를 사용 하지 않는 경우 데이터는 대상 데이터베이스의 임시 테이블에 로드 됩니다. 임시 테이블을 생성 및 대상 데이터베이스에서 삭제 하는 경우 임시 테이블 및 영구 테이블에 대 한 페이지 인터리브 됩니다. 테이블 조각화는 시간이 지남에 따라 발생 하 고 성능이 저하 됩니다. 반면, 준비 데이터베이스를 임시 테이블 만들고 영구 테이블 보다 별도 파일 공간에서 삭제 되도록 합니다.  
  
**데이터베이스 테이블 구조를 준비합니다.**  
  
각 데이터베이스 테이블의 저장소 구조는 대상 테이블에 따라 달라 집니다.  
  
-   힙 또는 클러스터형된 columnstore 인덱스에 로드를 준비 테이블은 힙.  
  
-   클러스터형된 rowstore 인덱스에 로드를 준비 테이블은 클러스터형된 rowstore 인덱스.  
  
## <a name="Permissions"></a>Permissions  
준비 데이터베이스 만들기 권한 (임시 테이블 만들기)에 필요 합니다. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>준비 데이터베이스를 만들기 위한 모범 사례  
  
1.  어플라이언스 당 하나의 스테이징 데이터베이스만 있을 것입니다. 모든 대상 데이터베이스에 대 한 모든 로드 작업에서 준비 데이터베이스를 공유할 수 있습니다.  
  
2.  준비 데이터베이스의 크기가 고객에 해당 합니다. 처음에 어플라이언스를 먼저 채운 경우 스테이징 데이터베이스를 초기 로드 작업을 수용할 만큼 넓은 여야 합니다. 이 작업을 로드 여러 로드를 동시에 발생할 수 있으므로 큰 경우가 많습니다. 초기 로드 작업이 완료 후 프로덕션에서 시스템은 각 로드 작업의 크기가 더 작게 할 수 있습니다. 로드 작은 경우에 작은 로드 크기에 맞게 준비 데이터베이스의 크기를 줄일 수 있습니다. 크기를 줄이려면 스테이징 데이터베이스를 삭제 하는 더 작은 크기 할당을 사용 하 여 다시 만들어야 하거나 사용할 수 있습니다 합니다 [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 문입니다.  
  
    준비 데이터베이스를 만들 때 다음 지침을 따르세요.  
  
    -   복제 된 테이블 크기 계산 노드당 동시에 로드 하는 모든 복제 된 테이블의 예상된 크기를 해야 합니다. 크기는 일반적으로 25-30GB.  
  
    -   분산된 테이블 크기를 사용 하는 동시에 로드 하는 모든 분산된 테이블의 어플라이언스 당 예상된 크기를 여야 합니다.  
  
    -   로그 크기를 복제 된 테이블 크기를 일반적으로 비슷합니다.  
  
## <a name="Examples"></a>예제  
  
### <a name="a-create-a-staging-database"></a>A. 준비 데이터베이스 만들기 
다음 예제에서는 모든 로드 어플라이언스에 사용에 대 한 스테이징 데이터베이스, Stagedb를를 만듭니다. 복제 된 5 개의 각 5GB가 동시에 로드 하는 크기의 테이블을 예측 한다고 가정 합니다. 이 동시성 복제 된 크기에 대 한 최소 25GB를 할당 하면 됩니다. 테이블 크기 100 distributed 6에 예상 가정 200, 400, 500, 500 및 550GB 동시에 로드 됩니다. 이 동시성 2250 GB 이상 분산된 테이블 크기에 할당 됩니다.  
  
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
  
