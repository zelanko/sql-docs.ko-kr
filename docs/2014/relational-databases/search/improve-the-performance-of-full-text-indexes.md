---
title: 전체 텍스트 인덱스 성능 향상 | Microsoft 문서
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], full-text search
- full-text queries [SQL Server], performance
- crawls [full-text search]
- full-text indexes [SQL Server], performance
- full-text search [SQL Server], performance
- batches [SQL Server], full-text search
ms.assetid: ef39ef1f-f0b7-4582-8e9c-31d4bd0ad35d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 42aa89a111697f17f23613761eeeb462494bdd27
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011256"
---
# <a name="improve-the-performance-of-full-text-indexes"></a>전체 텍스트 인덱스 성능 향상
  전체 텍스트 인덱싱 및 전체 텍스트 쿼리의 성능은 메모리, 디스크 속도, CPU 속도 및 컴퓨터 아키텍처와 같은 하드웨어 리소스의 영향을 받습니다.  
  
##  <a name="causes"></a> 성능 문제의 일반적인 원인  
 전체 텍스트 인덱싱 성능이 저하되는 주요 원인으로는 다음과 같은 하드웨어 리소스 제한을 들 수 있습니다.  
  
-   필터 데몬 호스트 프로세스(fdhost.exe) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스(sqlservr.exe)에 의한 CPU 사용률이 100%에 가까운 경우 CPU는 병목 상태입니다.  
  
-   평균 디스크 대기 큐 길이가 디스크 헤드 수보다 두 배 이상 많은 경우 디스크에 병목 상태가 존재합니다. 기본적인 해결 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일 및 로그와 별개인 전체 텍스트 카탈로그를 만드는 것입니다. 로그, 데이터베이스 파일 및 전체 텍스트 카탈로그를 서로 다른 디스크에 저장합니다. 또한 더 빠른 디스크를 구입하고 RAID를 사용하면 인덱싱 성능을 향상시키는 데 도움이 될 수 있습니다.  
  
-   실제 메모리(3GB 한도)가 부족할 경우 메모리가 병목 상태일 수 있습니다. 실제 메모리 제한은 모든 시스템에서 발생 가능하며 32비트 시스템의 경우 가상 메모리 가중으로 인해 전체 텍스트 인덱싱 속도가 느려질 수 있습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 전체 텍스트 엔진이 sqlservr.exe에 속하기 때문에 AWE 메모리가 사용됩니다.  
  
 시스템에 하드웨어 병목 상태가 존재하지 않을 경우 전체 텍스트 검색의 인덱싱 성능은 주로 다음 사항에 따라 달라집니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 전체 텍스트 일괄 처리를 만드는 데 걸리는 시간  
  
-   필터 데몬에서 이러한 일괄 처리를 완료할 수 있는 시간  
  
> [!NOTE]  
>  전체 채우기와 달리 증분, 수동 및 자동 변경 내용 추적 채우기는 하드웨어 리소스를 극대화하여 더 빠른 속도를 낼 수 없습니다. 따라서 이러한 튜닝 제안이 전체 텍스트 인덱싱의 성능을 향상시키지 않을 수도 있습니다.  
  
 채우기가 완료되면 인덱스 조각을 하나의 마스터 전체 텍스트 인덱스로 병합하는 최종 병합 프로세스가 실행됩니다. 이렇게 하면 많은 인덱스 조각 대신 마스터 인덱스만 쿼리하면 되기 때문에 쿼리 성능이 향상되며 개선된 평가 통계를 사용하여 관련성 등급을 지정할 수 있습니다. 인덱스 조각을 병합할 때 많은 양의 데이터를 읽고 써야 하기 때문에 마스터 병합에 많은 I/O 사용량이 필요할 수 있지만 이로 인해 들어오는 쿼리가 차단되지는 않습니다.  
  
> [!IMPORTANT]  
>  많은 양의 데이터를 마스터 병합하면 장기 실행 트랜잭션이 생성될 수 있으며 이로 인해 검사점이 사용되는 동안 트랜잭션 로그의 잘림이 지연될 수 있습니다. 이 경우 전체 복구 모델에서 트랜잭션 로그의 크기가 대폭 증가할 수 있습니다. 전체 복구 모델이 사용되는 데이터베이스에서 큰 전체 텍스트 인덱스를 다시 구성하기 전에 장기 실행 트랜잭션에 대비하여 트랜잭션 로그에 충분한 공간을 확보하는 것이 가장 좋은 방법입니다. 자세한 내용은 [트랜잭션 로그 파일의 크기 관리](../logs/manage-the-size-of-the-transaction-log-file.md)를 참조하세요.  
  
  
  
##  <a name="tuning"></a> 전체 텍스트 인덱스의 성능 튜닝  
 전체 텍스트 인덱스의 성능을 극대화하려면 다음과 같은 방법을 구현하는 것이 가장 좋습니다.  
  
-   를 사용 하려면 모든 프로세서 또는 코어를 최대로 설정 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)'`max full-text crawl ranges`' 시스템에서 Cpu의 수입니다. 이 구성 옵션에 대한 자세한 내용은 [max full-text crawl range 서버 구성 옵션](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)을 참조하세요.  
  
-   기본 테이블에 클러스터형 인덱스가 있는지 확인합니다. 클러스터형 인덱스의 첫 번째 열에 정수 데이터 형식을 사용합니다. 클러스터형 인덱스의 첫 번째 열에 GUID를 사용하지 않아야 합니다. 클러스터형 인덱스에 다중 범위 채우기가 있을 경우 채우기 속도가 가장 빨라질 수 있습니다. 전체 텍스트 키로 사용하는 열을 정수 데이터 형식으로 설정하는 것이 좋습니다.  
  
-   [UPDATE STATISTICS](/sql/t-sql/statements/update-statistics-transact-sql) 문을 사용하여 기본 테이블의 통계를 업데이트합니다. 더욱 중요한 것은 전체 채우기에 대한 클러스터형 인덱스 또는 전체 텍스트 키의 통계를 업데이트하는 것입니다. 이렇게 하면 다중 범위 채우기에서 테이블에 적절한 파티션을 생성하는 데 도움이 됩니다.  
  
-   증분 채우기의 성능을 향상시키려면 `timestamp` 열에 보조 인덱스를 작성합니다.  
  
-   대형 다중 CPU 컴퓨터에 대해 전체 채우기를 수행하려면 fdhost.exe 프로세스 및 운영 체제 용도로 메모리를 충분히 남기도록 `max server memory` 값을 설정하여 버퍼 풀 크기를 임시로 제한하는 것이 좋습니다. 자세한 내용은 이 항목 후반에 나오는 "필터 데몬 호스트 프로세스(fdhost.exe)의 메모리 요구 사항 예상"을 참조하십시오.  
  
  
  
##  <a name="full"></a> 전체 채우기 성능 문제 해결  
 성능 문제를 진단하려면 전체 텍스트 탐색 로그를 검토합니다. 탐색 로그에 대한 자세한 내용은 [전체 텍스트 인덱스 채우기](../indexes/indexes.md)를 참조하세요.  
  
 전체 채우기 성능이 만족스럽지 못할 경우 다음 문제 해결 과정을 순서대로 따르는 것이 좋습니다.  
  
### <a name="physical-memory-usage"></a>실제 메모리 사용률  
 전체 텍스트 채우기를 수행하는 동안 fdhost.exe 또는 sqlservr.exe의 메모리가 부족하거나 아예 없을 수 있습니다. 전체 텍스트 탐색 로그에 fdhost.exe가 자주 다시 시작되는 것으로 나타나거나 오류 코드 8007008이 반환된 것으로 나타날 경우 이러한 프로세스 중 하나에 메모리 부족 문제가 발생한 것입니다. fdhost.exe가 특히 대형 다중 CPU 컴퓨터에서 덤프를 생성하는 경우 이는 메모리 부족 때문일 수 있습니다.  
  
> [!NOTE]  
>  전체 텍스트 탐색에 사용되는 메모리 버퍼에 대한 자세한 내용은 [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)를 참조하세요.  
  
 가능한 원인은 다음과 같습니다.  
  
-   전체 채우기 과정 중에 사용할 수 있는 실제 메모리 양이 0바이트인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀이 시스템의 실제 메모리를 대부분 사용 중일 수 있습니다.  
  
     sqlservr.exe 프로세스는 버퍼 풀에 가능한 메모리를 구성된 최대 서버 메모리까지 모두 사용하려고 합니다. `max server memory`에 할당된 양이 너무 많은 경우 메모리가 부족하여 fdhost.exe 프로세스에 공유 메모리를 할당할 수 없습니다.  
  
    > [!NOTE]  
    >  다중 CPU 컴퓨터에서 전체 텍스트 채우기를 수행하는 과정에서 fdhost.exe와 sqlservr.exe 사이에 버퍼 풀 메모리를 위한 경합이 발생할 수 있습니다. 이로 인한 공유 메모리 부족으로 일괄 처리가 다시 시도되고, 메모리 스레시가 발생하며, fdhost.exe 프로세스에서 덤프가 생성됩니다.  
  
     이 문제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀의 `max server memory` 값을 적절히 설정하면 해결할 수 있습니다. 자세한 내용은 이 항목 후반에 나오는 "필터 데몬 호스트 프로세스(fdhost.exe)의 메모리 요구 사항 예상"을 참조하십시오. 전체 텍스트 인덱싱에 사용되는 일괄 처리 크기를 줄여도 도움이 됩니다.  
  
-   페이징 문제  
  
     페이지 파일 크기가 충분하지 않은 경우(예: 증가가 제한된 소형 페이지 파일이 있는 시스템에서)에도 fdhost.exe 또는 sqlservr.exe 실행 시 메모리 부족이 발생할 수 있습니다.  
  
     탐색 로그에 메모리 관련 오류가 표시되지 않은 경우 과도한 페이징으로 인한 성능 저하 상태일 수 있습니다.  
  
  
  
### <a name="estimating-the-memory-requirements-of-the-filter-daemon-host-process-fdhostexe"></a>필터 데몬 호스트 프로세스(fdhost.exe)의 메모리 요구 사항 예상  
 채우기용으로 fdhost.exe 프로세스에서 필요로 하는 메모리 양은 사용되는 전체 텍스트 탐색 범위 수, ISM(인바운드 공유 메모리) 크기, 최대 ISM 인스턴스 수 등에 따라 다릅니다.  
  
 필터 데몬 호스트에서 사용되는 메모리(바이트)는 다음 수식을 사용하여 대략적으로 계산할 수 있습니다.  
  
 *number_of_crawl_ranges* \`ism_size`*max_outstanding_isms*\* 2  
  
 이 수식에서 변수 기본값은 다음과 같습니다.  
  
|**변수**|**기본값**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|CPU 수|  
|*ism_size*|x86 컴퓨터의 경우 1MB<br /><br /> x64 컴퓨터의 경우 4MB, 8MB 또는 16MB(총 실제 메모리에 따라 다름)|  
|*max_outstanding_isms*|x86 컴퓨터의 경우 25<br /><br /> x64 컴퓨터의 경우 5|  
  
 다음 표에서는 fdhost.exe의 메모리 요구 사항을 계산하는 방법에 대한 지침을 제공합니다. 이 표의 수식에 사용되는 값은 다음과 같습니다.  
  
-   *F*는 fdhost.exe에 필요한 예상 메모리(MB)입니다.  
  
-   *T*는 시스템에서 사용 가능한 실제 총 메모리(MB)입니다.  
  
-   *M*, 최적의 `max server memory` 설정 합니다.  
  
> [!IMPORTANT]  
>  수식에 대 한 중요 한 정보를 참조 하세요 <sup>1</sup>를 <sup>2</sup>, 및 <sup>3</sup>아래.  
  
|플랫폼|MB-fdhost.exe 메모리 요구 사항을 추정*F*<sup>1</sup>|최대 서버 메모리-계산 수식*M*<sup>2</sup>|  
|--------------|---------------------------------------------------------------------|---------------------------------------------------------------|  
|x86|_F_ **=** _탐색 범위 수가_ **&#42;** 50|_M_ **=minimum(** _T_ **,** 2000 **)-*`F`*-** 500|  
|x64|_F_ **=** _탐색 범위 수가_ **&#42;** 10 **&#42;** 8|_M_ **=** _T_ **-** _F_ **-** 500|  
  
 <sup>1</sup> 여러 전체 채우기가 진행에서 하는 경우에 각각 한 fdhost.exe 메모리 요구 사항을 계산 개별적으로 *F1*하십시오 *F2*등입니다. 그런 다음, *M*을 _T_**-** sigma **(**_F_i **)** 로 계산합니다.  
  
 <sup>2</sup> 500MB는 시스템의 다른 프로세스에 필요한 메모리를 예상 합니다. 시스템이 추가 작업을 수행 중인 경우 그에 따라 이 값을 늘리십시오.  
  
 <sup>3</sup> . *ism_size* x64 8mb로 가정 플랫폼입니다.  
  
 **예: Fdhost.exe에 필요한 예상 메모리 요구 사항 예상**  
  
 이 예는 8GB RAM과 4개의 듀얼 코어 프로세서가 장착된 AMD64 컴퓨터에 해당합니다. 첫 번째 계산에서는 fdhost.exe에 필요한 메모리인*F*를 예측합니다. 탐색 범위 수는 `8`입니다.  
  
 `F = 8*10*8=640`  
  
 다음 계산에 대 한 최적의 값을 가져옵니다 `max server memory` - *M*합니다. *T*실제 총 메모리 (mb)-이 시스템에서 사용 가능한*T*-은 `8192`합니다.  
  
 `M = 8192-640-500=7052`  
  
 **예: Max server memory 설정**  
  
 이 예제에서는 합니다 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 및 [다시 구성](/sql/t-sql/language-elements/reconfigure-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] 설정 하는 문을 `max server memory` 계산 되는 값을 *M* 앞의 예제 , `7052`:  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
 **최대 서버 메모리 구성 옵션을 설정 하려면**  
  
-   [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
  
### <a name="factors-that-can-reduce-cpu-consumption"></a>CPU 사용량을 줄일 수 있는 요소  
 평균 CPU 사용량이 30% 미만이면 전체 채우기 성능이 최적의 상태가 아닌 것으로 간주됩니다. 이 섹션에서는 CPU 사용량에 영향을 주는 몇 가지 요소에 대해 설명합니다.  
  
-   긴 페이지 대기 시간  
  
     페이지 대기 시간이 긴지 확인하려면 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    Execute SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     다음 표에서는 몇 가지 흥미로운 대기 유형을 설명합니다.  
  
    |대기 유형|Description|가능한 해결 방법|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH(_EX 또는 _UP)|IO 병목 상태를 나타내며, 이 경우 일반적으로 평균 디스크 큐 길이가 깁니다.|전체 텍스트 인덱스를 다른 디스크의 다른 파일 그룹으로 이동하면 IO 병목 상태가 줄어들 수 있습니다.|  
    |PAGELATCH_EX(또는 _UP)|동일한 데이터베이스 파일에 쓰기를 시도하고 있는 스레드 간에 경합이 많이 발생하고 있음을 나타냅니다.|전체 텍스트 인덱스가 상주하는 파일 그룹에 파일을 추가하면 이러한 경합을 완화할 수 있습니다.|  
  
     자세한 내용은 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)를 참조하세요.  
  
-   비효율적인 기본 테이블 검색  
  
     전체 채우기는 기본 테이블을 검색하여 일괄 처리를 생성합니다. 이러한 테이블 검색은 다음과 같은 경우 비효율적일 수 있습니다.  
  
    -   기본 테이블에 전체 텍스트 인덱싱을 수행 중인 행 외부 열의 비율이 높을 경우 일괄 처리를 생성하기 위해 기본 테이블을 검색하면 병목 상태가 발생할 수 있습니다. 이 경우에는 `varchar(max)` 또는 `nvarchar(max)`를 사용하여 비교적 작은 행 내부 데이터를 이동하는 것이 좋습니다.  
  
    -   기본 테이블이 심하게 조각화된 경우 검색이 비효율적일 수 있습니다. 행 외부 데이터 및 인덱스 조각화를 계산하는 방법은 [sys.dm_db_partition_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql) 및 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)를 참조하세요.  
  
         조각화를 완화하기 위해 클러스터형 인덱스를 다시 구성하거나 다시 작성할 수 있습니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
  
  
##  <a name="filters"></a> 필터로 인 한 인덱싱 성능 저하 문제 해결  
 전체 텍스트 엔진은 전체 텍스트 인덱스를 채울 때 다중 스레드 및 단일 스레드라는 두 가지 필터 유형을 사용합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 문서와 같은 일부 문서는 다중 스레드 필터를 사용하여 필터링됩니다. 그러나 Adobe Acrobat PDF(Portable Document Format) 문서와 같은 다른 문서는 단일 스레드 필터를 사용하여 필터링됩니다.  
  
 보안상의 이유로 필터는 필터 데몬 호스트 프로세스에 의해 로드됩니다. 서버 인스턴스는 모든 다중 스레드 필터에 대해 다중 스레드 프로세스를 사용하고 모든 단일 스레드 필터에 대해 단일 스레드 프로세스를 사용합니다. 다중 스레드 필터를 사용하는 문서에 단일 스레드 필터를 사용하는 포함 문서가 있을 경우 전체 텍스트 엔진은 해당 포함 문서에 대해 단일 스레드 프로세스를 시작합니다. 예를 들어 PDF 문서가 포함된 Word 문서가 있을 경우 전체 텍스트 엔진은 Word 콘텐츠에 대해 다중 스레드 프로세스를 사용하고 PDF 콘텐츠에 대해 단일 스레드 프로세스를 시작합니다. 그러나 이러한 환경에서는 단일 스레드 필터가 제대로 작동하지 않을 수 있으며 이로 인해 필터링 프로세스가 불안정해질 수 있습니다. 이러한 포함 작업이 자주 수행되는 특정 환경에서는 필터링 프로세스 불안정화로 인해 해당 프로세스가 충돌할 수 있습니다. 충돌이 발생하면 전체 텍스트 엔진은 실패한 문서(예: 포함된 PDF 콘텐츠가 있는 Word 문서)를 단일 스레드 필터링 프로세스로 모두 다시 라우팅합니다. 다시 라우팅 작업이 자주 발생하면 전체 텍스트 인덱싱 프로세스의 성능이 저하됩니다.  
  
 이 문제를 해결하려면 컨테이너 문서(이 경우 Word)의 필터를 단일 스레드 필터로 표시합니다. 필터 레지스트리 값을 변경하여 지정된 필터를 단일 스레드 필터로 표시할 수 있습니다. 필터는 단일 스레드 필터로 표시를 설정 해야 합니다 **ThreadingModel** 필터 레지스트리 값 `Apartment Threaded`합니다. 단일 스레드 아파트에 대한 자세한 내용은 [COM 스레딩 모델 이해 및 사용](https://go.microsoft.com/fwlink/?LinkId=209159)백서를 참조하세요.  
  
  
  
## <a name="see-also"></a>관련 항목  
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [max full-text crawl range 서버 구성 옵션](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [전체 텍스트 인덱스 채우기](populate-full-text-indexes.md)   
 [전체 텍스트 인덱스 만들기 및 관리](create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)   
 [sys.dm_fts_memory_pools&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)   
 [전체 텍스트 인덱싱 문제 해결](troubleshoot-full-text-indexing.md)  
  
  
