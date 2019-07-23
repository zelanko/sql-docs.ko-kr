---
title: 전체 텍스트 인덱스 성능 향상 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a755ba9aa8915734768c56c096ea917a6e0c5564
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021224"
---
# <a name="improve-the-performance-of-full-text-indexes"></a>전체 텍스트 인덱스 성능 향상
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
이 항목에서는 전체 텍스트 인덱스 및 쿼리 성능 저하의 몇 가지 일반적인 원인에 대해 설명합니다. 또한 이러한 문제를 완화하고 성능을 향상시킬 수 있는 몇 가지 제안 사항도 제공합니다.
  
##  <a name="causes"></a> Common causes of performance issues
### <a name="hardware-resource-issues"></a>하드웨어 리소스 문제
전체 텍스트 인덱싱 및 전체 텍스트 쿼리의 성능은 메모리, 디스크 속도, CPU 속도 및 컴퓨터 아키텍처와 같은 하드웨어 리소스의 영향을 받습니다.  

전체 텍스트 인덱싱 성능이 저하되는 주요 원인으로는 다음과 같은 하드웨어 리소스 제한을 들 수 있습니다.  
  
-   **CPU**. 필터 데몬 호스트 프로세스(fdhost.exe) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스(sqlservr.exe)에 의한 CPU 사용률이 100%에 가까운 경우 CPU는 병목 상태입니다.  
  
-   **메모리**. 실제 메모리가 부족할 경우 메모리 병목 상태가 발생할 수 있습니다.  

-   **디스크**. 평균 디스크 대기 큐 길이가 디스크 헤드 수보다 두 배 이상 많은 경우 디스크에 병목 상태가 존재합니다. 기본적인 해결 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 파일 및 로그와 별개인 전체 텍스트 카탈로그를 만드는 것입니다. 로그, 데이터베이스 파일 및 전체 텍스트 카탈로그를 서로 다른 디스크에 저장합니다. 또한 더 빠른 디스크를 설치하고 RAID를 사용하면 인덱싱 성능을 향상시키는 데 도움이 될 수 있습니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 전체 텍스트 엔진이 sqlservr.exe 프로세스에 속하기 때문에 AWE 메모리가 사용됩니다.  

### <a name="full-text-batching-issues"></a>전체 텍스트 일괄 처리 문제
 시스템에 하드웨어 병목 상태가 존재하지 않을 경우 전체 텍스트 검색의 인덱싱 성능은 주로 다음 사항에 따라 달라집니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 전체 텍스트 일괄 처리를 만드는 데 걸리는 시간  
  
-   필터 데몬에서 이러한 일괄 처리를 완료할 수 있는 시간  

### <a name="full-text-index-population-issues"></a>전체 텍스트 인덱스 채우기 문제
-   **채우기 유형**. 전체 채우기와 달리 증분, 수동 및 자동 변경 내용 추적 채우기는 하드웨어 리소스를 극대화하여 더 빠른 속도를 낼 수 없습니다. 따라서 이 항목의 튜닝 제안이 증분, 수동 또는 자동 변경 내용 추적 채우기를 사용하는 경우 전체 텍스트 인덱싱 성능을 향상시키지 않을 수 있습니다.  
  
-   **마스터 병합**. 채우기가 완료되면 인덱스 조각을 하나의 마스터 전체 텍스트 인덱스로 병합하는 최종 병합 프로세스가 실행됩니다. 이렇게 하면 많은 인덱스 조각 대신 마스터 인덱스만 쿼리하면 되기 때문에 쿼리 성능이 향상되며 개선된 평가 통계를 사용하여 관련성 등급을 지정할 수 있습니다. 그러나 인덱스 조각을 병합할 때 많은 양의 데이터를 읽고 써야 하기 때문에 마스터 병합에 많은 I/O 사용량이 필요할 수 있지만 이로 인해 들어오는 쿼리가 차단되지는 않습니다.  
  
    많은 양의 데이터를 마스터 병합하면 장기 실행 트랜잭션이 생성될 수 있으며 이로 인해 검사점이 사용되는 동안 트랜잭션 로그의 잘림이 지연될 수 있습니다. 이 경우 전체 복구 모델에서 트랜잭션 로그의 크기가 대폭 증가할 수 있습니다. 전체 복구 모델이 사용되는 데이터베이스에서 큰 전체 텍스트 인덱스를 다시 구성하기 전에 장기 실행 트랜잭션에 대비하여 트랜잭션 로그에 충분한 공간을 확보하는 것이 가장 좋은 방법입니다. 자세한 내용은 [트랜잭션 로그 파일의 크기 관리](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)를 참조하세요.  
  
##  <a name="tuning"></a> 전체 텍스트 인덱스 성능 향상  
전체 텍스트 인덱스의 성능을 극대화하려면 다음과 같은 방법을 구현하는 것이 가장 좋습니다.  
  
-   모든 CPU 프로세서 또는 코어를 최대로 활용하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) '**max full-text crawl range**'를 시스템의 CPU 개수로 설정합니다. 이 구성 옵션에 대한 자세한 내용은 [max full-text crawl range 서버 구성 옵션](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)을 참조하세요.  
  
-   기본 테이블에 클러스터형 인덱스가 있는지 확인합니다. 클러스터형 인덱스의 첫 번째 열에 정수 데이터 형식을 사용합니다. 클러스터형 인덱스의 첫 번째 열에 GUID를 사용하지 않아야 합니다. 클러스터형 인덱스에 다중 범위 채우기가 있을 경우 채우기 속도가 가장 빨라질 수 있습니다. 전체 텍스트 키로 사용하는 열을 정수 데이터 형식으로 설정하는 것이 좋습니다.  
  
-   [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 문을 사용하여 기본 테이블의 통계를 업데이트합니다. 더욱 중요한 것은 전체 채우기에 대한 클러스터형 인덱스 또는 전체 텍스트 키의 통계를 업데이트하는 것입니다. 이렇게 하면 다중 범위 채우기에서 테이블에 적절한 파티션을 생성하는 데 도움이 됩니다.  
  
-   대형 다중 CPU 컴퓨터에 대해 전체 채우기를 수행하려면 fdhost.exe 프로세스 및 운영 체제 용도로 메모리를 충분히 남기도록 **max server memory** 값을 설정하여 버퍼 풀 크기를 임시로 제한하는 것이 좋습니다. 자세한 내용은 이 항목 후반에 나오는 "필터 데몬 호스트 프로세스(fdhost.exe)의 메모리 요구 사항 예상"을 참조하십시오.

-   타임스탬프 열 기반의 증분 채우기를 사용할 경우 증분 채우기의 성능을 향상시키려면 **timestamp** 열에 보조 인덱스를 빌드합니다.  
  
##  <a name="full"></a> 전체 채우기 성능 문제 해결  
### <a name="review-the-full-text-crawl-logs"></a>전체 텍스트 크롤링 로그 검토
 성능 문제를 진단하려면 전체 텍스트 탐색 로그를 검토합니다.
 
탐색 중에 오류가 발생하면 전체 텍스트 검색 탐색 로깅 기능은 일반 텍스트 파일인 탐색 로그를 만들고 유지 관리합니다. 각 탐색 로그는 특정 전체 텍스트 카탈로그에 해당합니다. 기본적으로 지정된 인스턴스(이 예제에서는 기본 인스턴스)에 대한 크롤링 로그는 `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG` 폴더에 있습니다.
 
탐색 로그 파일은 다음 명명 구성표를 따릅니다.  
  
`SQLFT<DatabaseID\><FullTextCatalogID\>.LOG[<n\>]`
  
크롤링 로그 파일 이름의 변수 부분은 다음과 같습니다.
-   \<**DatabaseID**> - 데이터베이스의 ID입니다. <**dbid**>는 앞에 오는 0을 사용하는 5자리 숫자입니다.  
-   <**FullTextCatalogID**> - 전체 텍스트 카탈로그 ID입니다. \<**catid**>는 앞에 오는 0을 사용하는 5자리 숫자입니다.  
-   <**n**> - 동일한 전체 텍스트 카탈로그의 탐색 로그가 하나 이상 있음을 나타내는 정수입니다.  
  
 예를 들어 `SQLFT0000500008.2`는 데이터베이스 ID = 5, 전체 텍스트 카탈로그 ID = 8인 데이터베이스의 탐색 로그 파일입니다. 파일 이름 끝에 있는 2는 이 데이터베이스/카탈로그 쌍의 탐색 로그 파일이 두 개 있음을 나타냅니다.  

### <a name="check-physical-memory-usage"></a>실제 메모리 사용률 확인  
 전체 텍스트 채우기를 수행하는 동안 fdhost.exe 또는 sqlservr.exe의 메모리가 부족하거나 아예 없을 수 있습니다.
-   전체 텍스트 탐색 로그에 fdhost.exe가 자주 다시 시작되는 것으로 나타나거나 오류 코드 8007008이 반환된 것으로 나타날 경우 이러한 프로세스 중 하나에 메모리 부족 문제가 발생한 것입니다.
-   fdhost.exe가 특히 대형 다중 CPU 컴퓨터에서 덤프를 생성하는 경우 이는 메모리 부족 때문일 수 있습니다.  
-   전체 텍스트 탐색에 사용되는 메모리 버퍼에 대한 자세한 내용은 [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)를 참조하세요.  
  
 메모리 부족 문제의 원인은 다음과 같습니다.  
  
-   **메모리 부족**. 전체 채우기 과정 중에 사용할 수 있는 실제 메모리 양이 0바이트인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버퍼 풀이 시스템의 실제 메모리를 대부분 사용 중일 수 있습니다.  
  
     sqlservr.exe 프로세스는 버퍼 풀에 가능한 메모리를 구성된 최대 서버 메모리까지 모두 사용하려고 합니다. **max server memory** 에 할당된 양이 너무 많은 경우 메모리가 부족해져 fdhost.exe 프로세스에 공유 메모리를 할당하지 못하게 될 수 있습니다.  
  
     **버퍼 풀의** max server memory [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 값을 적절히 설정하면 이 문제를 해결할 수 있습니다. 자세한 내용은 이 항목 후반에 나오는 "필터 데몬 호스트 프로세스(fdhost.exe)의 메모리 요구 사항 예상"을 참조하십시오. 전체 텍스트 인덱싱에 사용되는 일괄 처리 크기를 줄여도 도움이 됩니다.  

-   **메모리 경합**. 다중 CPU 컴퓨터에서 전체 텍스트 채우기를 수행하는 과정에서 fdhost.exe와 sqlservr.exe 사이에 버퍼 풀 메모리를 위한 경합이 발생할 수 있습니다. 이로 인한 공유 메모리 부족으로 일괄 처리가 다시 시도되고, 메모리 스레시가 발생하며, fdhost.exe 프로세스에서 덤프가 생성됩니다.  

-   **페이징 문제**. 페이지 파일 크기가 충분하지 않은 경우(예: 증가가 제한된 소형 페이지 파일이 있는 시스템에서)에도 fdhost.exe 또는 sqlservr.exe 실행 시 메모리 부족이 발생할 수 있습니다. 탐색 로그에 메모리 관련 오류가 표시되지 않은 경우 과도한 페이징으로 인한 성능 저하 상태일 수 있습니다.  
  
### <a name="estimate-the-memory-requirements-of-the-filter-daemon-host-process-fdhostexe"></a>필터 데몬 호스트 프로세스(fdhost.exe)의 메모리 요구 사항 예상  
 채우기용으로 fdhost.exe 프로세스에서 필요로 하는 메모리 양은 사용되는 전체 텍스트 탐색 범위 수, ISM(인바운드 공유 메모리) 크기, 최대 ISM 인스턴스 수 등에 따라 다릅니다.  
  
 필터 데몬 호스트에서 사용되는 메모리(바이트)는 다음 수식을 사용하여 대략적으로 계산할 수 있습니다.  
  
`number_of_crawl_ranges * ism_size * max_outstanding_isms * 2`  
  
 이 수식에서 변수 기본값은 다음과 같습니다.  
  
|**변수**|**기본값**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|CPU 수|  
|*ism_size*|x86 컴퓨터의 경우 1MB<br /><br /> x64 컴퓨터의 경우 4MB, 8MB 또는 16MB(총 실제 메모리에 따라 다름)|  
|*max_outstanding_isms*|x86 컴퓨터의 경우 25<br /><br /> x64 컴퓨터의 경우 5|  
  
 다음 표에서는 fdhost.exe의 메모리 요구 사항을 계산하는 방법에 대한 지침을 제공합니다. 이 표의 수식에 사용되는 값은 다음과 같습니다.  
  
-   *F*는 fdhost.exe에 필요한 예상 메모리(MB)입니다.  
  
-   *T*는 시스템에서 사용 가능한 실제 총 메모리(MB)입니다.  
  
-   *M*,(최적의 **max server memory** 설정)  
  
다음 수식에 대한 자세한 내용은 표 다음에 나오는 참고 사항을 참조하세요.  
  
|플랫폼|fdhost.exe에 필요한 예상 메모리(MB) - *F*^1|max server memory 계산 수식 - *M*^2|  
|--------------|-----------------------------------------------------------|-----------------------------------------------------|  
|x86|*F* = *탐색 범위 수* \* 50|*M* =minimum(*T*, 2000) - F - 500|  
|x64|*F* = *탐색 범위 수* \* 10 \* 8|*M* = *T* - *F* - 500|  

**수식 관련 참고 사항**
1.  여러 전체 채우기가 진행 중인 경우 *F1*, *F2*와 같이 각 채우기 작업에 대한 fdhost.exe 메모리 요구 사항을 개별적으로 계산합니다. 그런 다음, *M*을 _T_ **-** sigma **(** _F_i **)** 로 계산합니다.  
2.  500MB는 시스템의 다른 프로세스에 필요한 예상 메모리 양입니다. 시스템이 추가 작업을 수행 중인 경우 그에 따라 이 값을 늘리십시오.  
3.  를 참조하세요.*ism_size* 는 x64 플랫폼의 경우 8MB로 가정합니다.  
  
 #### <a name="example-estimate-the-memory-requirements-of-fdhostexe"></a>예: fdhost.exe에 필요한 예상 메모리  
  
 이 예제는 8GB RAM과 4개의 듀얼 코어 프로세서가 장착된 64비트 컴퓨터에 해당합니다. 첫 번째 계산에서는 fdhost.exe에 필요한 메모리인*F*를 예측합니다. 탐색 범위 수는 `8`입니다.  
  
 `F = 8*10*8=640`  
  
 다음 계산에서는 **max server memory**의 최적 값-*M*을 구합니다. 이 시스템에서 사용 가능한 실제 총 메모리(MB)(*T*)는 `8192`입니다.  
  
 `M = 8192-640-500=7052`  
  
 #### <a name="example-setting-max-server-memory"></a>예: 최대 서버 메모리 설정  
  
 이 예에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 및 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하여 **max server memory** 를 위의 예에서 *M* 에 대한 계산한 값 `7052`로 설정합니다.  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
서버 메모리 옵션에 대한 자세한 내용은 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조하세요.
  
### <a name="check-cpu-usage"></a>CPU 사용량 확인  
평균 CPU 사용량이 30% 미만이면 전체 채우기 성능이 최적의 상태가 아닙니다. CPU 사용량에 영향을 주는 몇 가지 요소는 다음과 같습니다.  
  
-   긴 페이지 대기 시간  
  
     페이지 대기 시간이 긴지 확인하려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     다음 표에서는 몇 가지 흥미로운 대기 유형을 설명합니다.  
  
    |대기 유형|설명|가능한 해결 방법|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH(_EX 또는 _UP)|IO 병목 상태를 나타내며, 이 경우 일반적으로 평균 디스크 큐 길이가 깁니다.|전체 텍스트 인덱스를 다른 디스크의 다른 파일 그룹으로 이동하면 IO 병목 상태가 줄어들 수 있습니다.|  
    |PAGELATCH_EX(또는 _UP)|동일한 데이터베이스 파일에 쓰기를 시도하고 있는 스레드 간에 경합이 많이 발생하고 있음을 나타냅니다.|전체 텍스트 인덱스가 상주하는 파일 그룹에 파일을 추가하면 이러한 경합을 완화할 수 있습니다.|  
  
     자세한 내용은 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)를 참조하세요.  
  
-   비효율적인 기본 테이블 검색  
  
     전체 채우기는 기본 테이블을 검색하여 일괄 처리를 생성합니다. 이러한 테이블 검색은 다음과 같은 경우 비효율적일 수 있습니다.  
  
    -   기본 테이블에 전체 텍스트 인덱싱을 수행 중인 행 외부 열의 비율이 높을 경우 일괄 처리를 생성하기 위해 기본 테이블을 검색하면 병목 상태가 발생할 수 있습니다. 이 경우에는 **varchar(max)** 또는 **nvarchar(max)** 를 사용하여 비교적 작은 행 내부 데이터를 이동하는 것이 좋습니다.  
  
    -   기본 테이블이 심하게 조각화된 경우 검색이 비효율적일 수 있습니다. 행 외부 데이터 및 인덱스 조각화를 계산하는 방법은 [sys.dm_db_partition_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 및 [sys.dm_db_index_physical_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 참조하세요.  
  
         조각화를 완화하기 위해 클러스터형 인덱스를 다시 구성하거나 다시 작성할 수 있습니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
##  <a name="filters"></a> 문서의 느린 인덱싱 문제 해결

> [!NOTE]
> 이 섹션에서는 다른 문서 유형이 포함된 문서(예: Microsoft Word 문서)를 인덱싱하는 고객에게만 적용되는 문제에 대해 설명합니다.

전체 텍스트 엔진은 전체 텍스트 인덱스를 채울 때 다중 스레드 필터 및 단일 스레드 필터라는 두 가지 필터 유형을 사용합니다.
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 문서와 같은 일부 문서는 다중 스레드 필터를 사용하여 필터링됩니다.
-   그러나 Adobe Acrobat PDF(Portable Document Format) 문서와 같은 다른 문서는 단일 스레드 필터를 사용하여 필터링됩니다.  
  
 보안상의 이유로 필터는 필터 데몬 호스트 프로세스에 의해 로드됩니다. 서버 인스턴스는 모든 다중 스레드 필터에 대해 다중 스레드 프로세스를 사용하고 모든 단일 스레드 필터에 대해 단일 스레드 프로세스를 사용합니다. 다중 스레드 필터를 사용하는 문서에 단일 스레드 필터를 사용하는 포함 문서가 있을 경우 전체 텍스트 엔진은 해당 포함 문서에 대해 단일 스레드 프로세스를 시작합니다. 예를 들어 PDF 문서가 포함된 Word 문서가 있을 경우 전체 텍스트 엔진은 Word 콘텐츠에 대해 다중 스레드 프로세스를 사용하고 PDF 콘텐츠에 대해 단일 스레드 프로세스를 시작합니다. 그러나 이러한 환경에서는 단일 스레드 필터가 제대로 작동하지 않을 수 있으며 이로 인해 필터링 프로세스가 불안정해질 수 있습니다. 이러한 포함 작업이 자주 수행되는 특정 환경에서는 불안정화로 인해 해당 프로세스가 충돌할 수 있습니다. 충돌이 발생하면 전체 텍스트 엔진은 실패한 문서(예: 포함된 PDF 콘텐츠가 있는 Word 문서)를 단일 스레드 필터링 프로세스로 모두 다시 라우트합니다. 다시 라우팅 작업이 자주 발생하면 전체 텍스트 인덱싱 프로세스의 성능이 저하됩니다.  
  
이 문제를 해결하려면 컨테이너 문서(이 예제의 경우 Word 문서)의 필터를 단일 스레드 필터로 표시합니다. 필터를 단일 스레드 필터로 표시하려면 필터의 **ThreadingModel** 레지스트리 값을 **Apartment Threaded**로 설정합니다. 단일 스레드 아파트에 대한 자세한 내용은 [COM 스레딩 모델 이해 및 사용](https://go.microsoft.com/fwlink/?LinkId=209159)백서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [max full-text crawl range 서버 구성 옵션](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)   
 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)   
 [전체 텍스트 인덱싱 문제 해결](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
  
