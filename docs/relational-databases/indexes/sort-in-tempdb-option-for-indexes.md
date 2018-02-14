---
title: "인덱스에 대한 SORT_IN_TEMPDB 옵션 | Microsoft 문서"
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SORT_IN_TEMPDB option
- disk space [SQL Server], indexes
- space [SQL Server], indexes
- tempdb database [SQL Server], indexes
- indexes [SQL Server], tempdb database
- index creation [SQL Server], tempdb database
ms.assetid: 754a003f-fe51-4d10-975a-f6b8c04ebd35
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dc20b72e294451f4c1475d04d63b037c86fd562d
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="sortintempdb-option-for-indexes"></a>인덱스에 대한 SORT_IN_TEMPDB 옵션
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  인덱스를 만들거나 다시 만들 때 SORT_IN_TEMPDB 옵션을 ON으로 설정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 **tempdb** 를 사용하여 인덱스를 만드는 데 사용되는 중간 정렬 결과를 저장하도록 지시할 수 있습니다. 이 옵션을 사용하면 인덱스를 만드는 데 사용되는 임시 디스크 공간이 늘어나지만 **tempdb** 가 사용자 데이터베이스와 다른 디스크 집합에 있을 때 인덱스를 만들거나 다시 만드는 데 필요한 시간이 줄어듭니다. **tempdb**에 대한 자세한 내용은 [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)를 참조하십시오.  
  
## <a name="phases-of-index-building"></a>인덱스를 만드는 단계  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 인덱스를 만들 때 다음 단계가 수행됩니다.  
  
-   먼저 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 기본 테이블의 데이터 페이지를 검색하여 키 값을 찾고 각 데이터 행의 인덱스 리프 행을 만듭니다. 내부 정렬 버퍼가 리프 인덱스 항목으로 채워지면 항목이 정렬되고 중간 정렬 실행으로 디스크에 기록됩니다. 그러면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 정렬 버퍼가 다시 채워질 때까지 데이터 페이지 검색을 계속합니다. 기본 테이블의 모든 행이 처리될 때까지 이러한 여러 데이터 페이지의 검색 패턴에 따라 정렬이 수행되고 정렬 실행 쓰기가 계속됩니다.  
  
     클러스터형 인덱스에서 인덱스의 리프 행은 테이블의 데이터 행이므로 중간 정렬 실행은 모든 데이터 행을 포함합니다. 비클러스터형 인덱스에서 리프 행은 키가 아닌 열을 포함할 수 있지만 일반적으로 클러스터형 인덱스보다 작습니다. 인덱스 키가 클 경우 또는 인덱스에 키가 아닌 열이 여러 개 포함된 경우 비클러스터형 정렬 실행이 클 수 있습니다. 키가 아닌 열 포함에 대한 자세한 내용은 [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)를 참조하십시오.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 정렬된 단일 스트림으로 인덱스 리프 행의 정렬된 실행을 병합합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 정렬 병합 구성 요소는 각 정렬 실행의 첫 페이지에서 시작하여 모든 페이지에서 가장 낮은 키를 찾은 다음 인덱스 만들기 구성 요소에 리프 행을 전달합니다. 다음으로 가장 낮은 키를 처리하는 식으로 이 과정이 계속됩니다. 마지막 리프 인덱스 행이 정렬 실행 페이지에서 추출되면 프로세스는 해당 정렬 실행에서 다음 페이지로 전환됩니다. 정렬 실행 익스텐트의 모든 페이지가 처리되면 익스텐트가 해제됩니다. 각 리프 인덱스 행이 인덱스 만들기 구성 요소에 전달되면 버퍼의 리프 인덱스 페이지에 포함됩니다. 각 리프 페이지는 채워진 후에 쓰여집니다. 리프 페이지가 쓰여지면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 도 인덱스의 상위 수준을 만듭니다. 각 상위 수준 인덱스 페이지는 채워진 후에 쓰여집니다.  
  
## <a name="sortintempdb-option"></a>SORT_IN_TEMPDB 옵션  
 SORT_IN_TEMPDB를 기본값인 OFF로 설정한 경우 기본적으로 정렬 실행은 대상 파일 그룹에 저장됩니다. 인덱스를 만드는 첫째 단계 동안 기본 테이블 페이지의 읽기와 정렬 실행의 쓰기가 번갈아 수행되어 디스크의 한 영역에서 다른 영역으로 디스크 읽기/쓰기 헤드가 이동됩니다. 이 헤드는 데이터 페이지가 검색될 때 데이터 페이지 영역에 있습니다. 정렬 버퍼가 채워지고 현재 정렬 실행이 디스크에 쓰여져야 할 때 이러한 헤드는 빈 영역으로 이동했다가 테이블 페이지 검색이 다시 시작될 때 데이터 페이지 영역으로 다시 돌아갑니다. 읽기/쓰기 헤드 이동은 둘째 단계에서 더 많이 수행됩니다. 이 단계에서 정렬 프로세스는 일반적으로 각 정렬 실행 영역을 번갈아 읽습니다. 대상 파일 그룹에 정렬 실행과 새 인덱스 페이지가 작성되는데 이는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 각 정렬 실행을 번갈아 읽으면서 동시에 주기적으로 인덱스 익스텐트로 점프하여 채워질 때 새 인덱스 페이지를 써야 함을 의미합니다.  
  
 SORT_IN_TEMPDB 옵션을 ON으로 설정하고 **tempdb** 가 대상 파일 그룹의 개별 디스크 집합에 있으면 첫째 단계 중에 데이터 페이지의 읽기는 **tempdb**의 정렬 작업 영역에 대한 쓰기와는 다른 디스크에서 발생합니다. 그러므로 마지막 인덱스를 작성하기 위한 쓰기를 수행할 때 일반적으로 데이터 키의 디스크 읽기가 디스크에서 좀 더 연속적으로 진행되며 일반적으로 **tempdb** 디스크에 대한 쓰기 역시 연속적으로 진행됩니다. 다른 사용자가 해당 데이터베이스를 사용하고 별도의 디스크 주소를 액세스하는 경우에도 읽기 및 쓰기의 전반적인 패턴은 SORT_IN_TEMPDB가 지정되는 것이 지정되지 않을 때보다 좀 더 효율적으로 나타납니다.  
  
 SORT_IN_TEMPDB 옵션은 특히 CREATE INDEX 작업이 병렬로 처리되지 않은 경우 인덱스 익스텐트의 근접성을 향상시킬 수 있습니다. 정렬 작업 영역 익스텐트는 데이터베이스에서 이 익스텐트가 차지하는 위치에 관계없이 해제됩니다. 정렬 작업 영역이 대상 파일 그룹에 포함된 경우 정렬 작업 익스텐트가 해제되면 익스텐트 구조가 작성될 때 인덱스 구조를 보유하기 위한 익스텐트 요청에 의해 정렬 작업 익스텐트가 확보될 수 있습니다. 이로 인해 어느 수준까지 인덱스 익스텐트의 위치가 무작위로 지정될 수 있습니다. 정렬 익스텐트가 **tempdb**에 별도로 보관되는 경우 해제되는 순서는 인덱스 익스텐트의 위치에 영향을 주지 않습니다. 또한 중간 정렬 실행이 대상 파일 그룹 대신 **tempdb** 에 저장되면 대상 파일 그룹에 사용 가능한 공간이 더 많아지므로 인덱스 익스텐트가 근접하게 될 확률이 높아집니다.  
  
 SORT_IN_TEMPDB 옵션은 현재 문에만 영향을 줍니다. 인덱스가 **tempdb**에서 정렬되어 있는지 여부를 기록하는 메타데이터는 없습니다. 예를 들어 SORT_IN_TEMPDB 옵션을 사용하여 비클러스터형 인덱스를 만들고 이후에 이 옵션을 지정하지 않고 클러스터형 인덱스를 만드는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 비클러스터형 인덱스를 다시 만들 때 이 옵션을 사용하지 않습니다.  
  
> [!NOTE]  
>  정렬 작업이 필요하지 않거나 메모리에서 정렬을 수행할 수 있으면 SORT_IN_TEMPDB 옵션이 무시됩니다.  
  
## <a name="disk-space-requirements"></a>디스크 공간 요구 사항  
 SORT_IN_TEMPDB 옵션을 ON으로 설정하면 **tempdb** 에는 중간 정렬 실행을 보관하기 위한 충분한 빈 디스크 공간이 있어야 하며 대상 파일 그룹에는 새 인덱스를 보관하기 위한 충분한 빈 디스크 공간이 있어야 합니다. 빈 공간이 충분하지 않고, 디스크에 공간이 없거나 자동 증가 옵션이 해제된 경우처럼 데이터베이스가 자동 증가되어 더 많은 공간을 확보하지 못하는 경우 CREATE INDEX 문은 실패합니다.  
  
 SORT_IN_TEMPDB를 OFF로 설정한 경우 대상 파일 그룹의 빈 디스크 공간은 최종 인덱스의 크기와 거의 같아야 합니다. 첫째 단계에서 정렬 실행이 작성되고 최종 인덱스와 거의 같은 양의 공간이 요구됩니다. 둘째 단계에서 각 정렬 실행 익스텐트는 처리된 후 해제됩니다. 따라서 정렬 실행 익스텐트가 최종 인덱스 페이지를 보유하기 위해 익스텐트가 확보되는 비율과 거의 동일한 비율로 해제되므로 전반적인 공간 요구 사항은 최종 인덱스의 크기를 많이 초과하지 않게 됩니다. 이로 인해 발생하는 한 가지 부작용은 빈 공간의 양이 최종 인덱스의 크기와 아주 근접할 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 일반적으로 정렬 실행 익스텐트가 해제되자마자 이 정렬 실행 익스텐트를 다시 사용한다는 것입니다. 정렬 실행 익스텐트는 무작위로 해제되므로 이 시나리오에 해당하는 인덱스 익스텐트의 근접성을 감소시킵니다. SORT_IN_TEMPDB를 OFF로 설정하면 새롭게 할당 취소된 정렬 실행 익스텐트가 아니라 연속된 풀에서 인덱스 익스텐트를 할당할 수 있도록 대상 파일 그룹에 충분한 빈 공간이 있을 경우 인덱스 익스텐트의 근접성이 향상됩니다.  
  
 비클러스터형 인덱스를 만들 때 다음과 같이 사용 가능한 공간이 있어야 합니다.  
  
-   SORT_IN_TEMPDB를 ON으로 설정한 경우 **tempdb** 에는 정렬 실행을 저장하기 위한 충분한 사용 가능한 공간이 있어야 하며 대상 파일 그룹에는 최종 인덱스 구조를 저장하기 위한 충분한 빈 공간이 있어야 합니다. 정렬 실행은 인덱스의 리프 행을 포함합니다.  
  
-   SORT_IN_TEMPDB를 OFF로 설정한 경우 대상 파일 그룹에는 최종 인덱스 구조를 저장하기 위한 빈 공간이 충분히 있어야 합니다. 인덱스 익스텐트의 근접성은 사용 가능한 빈 공간이 늘어날 때 향상될 수 있습니다.  
  
 비클러스터형 인덱스가 없는 테이블에 클러스터형 인덱스를 만드는 경우 다음과 같이 사용 가능한 공간이 있어야 합니다.  
  
-   SORT_IN_TEMPDB를 ON으로 설정한 경우 **tempdb** 에는 정렬 실행을 저장하기 위한 사용 가능한 공간이 충분히 있어야 합니다. 여기에는 테이블의 데이터 행이 포함됩니다. 대상 파일 그룹에는 최종 인덱스 구조를 저장하기 위한 충분한 빈 공간이 있어야 합니다. 여기에는 테이블의 데이터 행과 인덱스 B-트리가 포함됩니다. 키 크기를 크게 사용하거나 채우기 비율을 낮은 값으로 설정하는 등 예상 계수를 조정해야 할 수 있습니다.  
  
-   SORT_IN_TEMPDB를 OFF로 설정한 경우 대상 파일 그룹에는 최종 테이블을 저장하기 위한 빈 공간이 충분히 있어야 합니다. 여기에는 인덱스 구조가 포함됩니다. 테이블 및 인덱스 익스텐트의 근접성은 사용 가능한 빈 공간이 늘어날 때 향상될 수 있습니다.  
  
 비클러스터형 인덱스가 있는 테이블에 클러스터형 인덱스를 만드는 경우 사용 가능한 공간이 있어야 합니다.  
  
-   SORT_IN_TEMPDB를 ON으로 설정한 경우 **tempdb** 에는 가장 큰 인덱스(일반적으로 클러스터형 인덱스)의 정렬 실행 집합을 저장하기 위한 충분한 빈 공간이 있어야 하며 대상 파일 그룹에는 모든 인덱스의 최종 구조를 저장하기 위한 충분한 빈 공간이 있어야 합니다. 여기에는 테이블의 데이터 행이 있는 클러스터형 인덱스가 포함됩니다.  
  
-   SORT_IN_TEMPDB를 OFF로 설정한 경우 대상 파일 그룹에는 최종 테이블을 저장하기 위한 빈 공간이 충분히 있어야 합니다. 여기에는 모든 인덱스의 구조가 포함됩니다. 테이블 및 인덱스 익스텐트의 근접성은 사용 가능한 빈 공간이 늘어날 때 향상될 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
## <a name="related-content"></a>관련 내용  
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
 [인덱스 DDL 작업의 디스크 공간 요구 사항](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
  
