---
title: 실행 계획 논리 및 물리 연산자 참조 | Microsoft 문서
ms.custom: ''
ms.date: 10/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.showplan.leftouterjoin.f1
- sql13.swb.showplan.remotedelete.f1
- sql13.swb.showplan.parallelism.f1
- sql13.swb.showplan.indexspool.f1
- sql13.swb.showplan.result.f1
- sql13.swb.showplan.bitmapcreate.f1
- sql13.swb.showplan.remotescan.f1
- sql13.swb.showplan.union.f1
- sql13.swb.showplan.bitmap.f1
- sql13.swb.showplan.RIDLookup
- sql13.swb.showplan.innerjoin.f1
- sql13.swb.showplan.dynamic.f1
- sql13.swb.showplan.distributestreams.f1
- sql13.swb.showplan.clusteredindexdelete.f1
- sql13.swb.showplan.keylookup.f1
- sql13.swb.showplan.partialaggregate.f1
- sql13.swb.showplan.distinctsort.f1
- sql13.swb.showplan.collapse.f1
- sql13.swb.showplan.print.f1
- sql13.swb.showplan.crossjoin.f1
- sql13.swb.showplan.convert.f1
- sql13.swb.showplan.split.f1
- sql13.swb.showplan.top.f1
- sql13.swb.showplan.update.f1
- sql13.swb.showplan.keyset.f1
- sql13.swb.showplan.fetchquery.f1
- sql13.swb.showplan.mergejoin.f1
- sql13.swb.showplan.branchrepartition.f1
- sql13.swb.showplan.tableinsert.f1
- sql13.swb.showplan.clusteredindexseek.f1
- sql13.swb.showplan.indexupdate.f1
- sql13.swb.showplan.indexinsert.f1
- sql13.swb.showplan.clusteredindexupdate.f1
- sql13.swb.showplan.streamaggregate.f1
- sql13.swb.showplan.columnstoreindexdelete.f1
- sql13.swb.showplan.snapshot.f1
- sql13.swb.showplan.remotequery.f1
- sql13.swb.showplan.constantscan.f1
- sql13.swb.showplan.rank.f1
- sql13.swb.showplan.rightsemijoin.f1
- sql13.swb.showplan.delete.f1
- sql13.swb.showplan.sequence.f1
- sql13.swb.showplan.locate.f1
- sql13.swb.showplan.aggregate.f1
- sql13.swb.showplan.rightouterjoin.f1
- sql13.swb.showplan.columnstoreindexupdate.f1
- sql13.swb.showplan.clusteredindexinsert.f1
- sql13.swb.showplan.rowcountspool.f1
- sql13.swb.showplan.columnstoreindexscan.f1
- sql13.swb.showplan.leftantisemijoin.f1
- sql13.swb.showplan.sort.f1
- sql13.swb.showplan.leftsemijoin.f1
- sql13.swb.showplan.columnstoreindexinsert.f1
- sql13.swb.showplan.indexscan.f1
- sql13.swb.showplan.columnstoreindexmerge.f1
- sql13.swb.showplan.lazyspool.f1
- sql13.swb.showplan.rightantisemijoin.f1
- sql13.swb.showplan.bookmarklookup.f1
- sql13.swb.showplan.remoteinsert.f1
- sql13.swb.showplan.intrinsic.f1
- sql13.swb.showplan.arithmeticexpression.f1
- sql13.swb.showplan.populationquery.f1
- sql13.swb.showplan.filter.f1
- sql13.swb.showplan.if.f1
- sql13.swb.showplan.hashmatchteam.f1
- sql13.swb.showplan.tablevaluedfunction.f1
- sql13.swb.showplan.assign.f1
- sql13.swb.showplan.nestedloops.f1
- sql13.swb.showplan.buildhash.f1
- sql13.swb.showplan.mergeinterval.f1
- sql13.swb.showplan.hashmatch.f1
- sql13.swb.showplan.parametertablescan.f1
- sql13.swb.showplan.tablemerge.f1
- sql13.swb.showplan.switch.f1
- sql13.swb.showplan.sql.f1
- sql13.swb.showplan.repartitionstreams.f1
- sql13.swb.showplan.logrowscan.f1
- sql13.swb.showplan.assert.f1
- sql13.swb.showplan.computescalar.f1
- sql13.swb.showplan.broadcast.f1
- sql13.swb.showplan.indexseek.f1
- sql13.swb.showplan.gatherstreams.f1
- sql13.swb.showplan.remoteindexscan.f1
- sql13.swb.showplan.segment.f1
- sql13.swb.showplan.tableupdate.f1
- sql13.swb.showplan.clusteredindexscan.f1
- sql13.swb.showplan.cache.f1
- sql13.swb.showplan.spool.f1
- sql13.swb.showplan.indexdelete.f1
- sql13.swb.showplan.distinct.f1
- sql13.swb.showplan.deletedscan.f1
- sql13.swb.showplan.eagerspool.f1
- sql13.swb.showplan.hashmatchroot.f1
- sql13.swb.showplan.setfunction.f1
- sql13.swb.showplan.clusteredindexmerge.f1
- sql13.swb.showplan.flowdistinct.f1
- sql13.swb.showplan.tabledelete.f1
- sql13.swb.showplan.tablescan.f1
- sql13.swb.showplan.refreshquery.f1
- sql13.swb.showplan.tablespool.f1
- sql13.swb.showplan.insertedscan.f1
- sql13.swb.showplan.insert.f1
- sql13.swb.showplan.remoteindexseek.f1
- sql13.swb.showplan.fullouterjoin.f1
- sql13.swb.showplan.declare.f1
- sql13.swb.showplan.udx.f1
- sql13.swb.showplan.while.f1
- sql13.swb.showplan.remoteupdate.f1
- sql13.swb.showplan.concatenation.f1
- sql13.swb.showplan.computescalar
- sql13.swb.showplan.foreignkeyreferencescheck
helpviewer_keywords:
- execution plans [SQL Server], operators
- ActualRows attribute
- reading execution plan output
- ActualRewinds attribute
- ActualEndOfScans attribute
- query tuning [SQL Server]
- mapping operators [SQL Server]
- operators [Database Engine query tuning]
- logical operators [SQL Server], execution plans
- logical operators [SQL Server], listed
- physical operators [SQL Server]
- ActualRebinds attribute
- execution plans [SQL Server], reading output
ms.assetid: e43fd0fe-5ea7-4ffe-8d52-759ef6a7c361
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2fb9b4f90b40b70c67e27233f84ee7b2a99635cf
ms.sourcegitcommit: 15b780aa5abe3f42cd70b6edf7d5a645e990b618
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/07/2019
ms.locfileid: "54069093"
---
# <a name="showplan-logical-and-physical-operators-reference"></a>실행 계획 논리 및 물리 연산자 참조
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  연산자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 쿼리 또는 DML(데이터 조작 언어) 문이 실행되는 방식을 설명합니다. 쿼리 최적화 프로그램은 연산자를 사용하여 쿼리 계획을 작성함으로써 쿼리에 지정된 결과를 만들거나 DML 문에 지정된 작업을 수행합니다. 쿼리 계획은 물리 연산자로 구성된 트리입니다. SET SHOWPLAN 문, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 그래픽 실행 계획 옵션 또는 SQL Server Profiler의 Showplan 이벤트 클래스를 사용하여 쿼리 계획을 볼 수 있습니다.  
  
 연산자는 논리 연산자와 물리 연산자로 분류됩니다.  
  
 **논리 연산자**  
 논리 연산자는 문을 처리할 때 사용되는 관계형 대수 연산을 설명합니다. 즉, 논리 연산자는 어떤 작업을 수행해야 하는지 개념적으로 설명합니다.  
  
 **물리 연산자**  
 물리 연산자는 논리 연산자가 설명한 작업을 구현합니다. 각 물리 연산자는 연산을 수행하는 개체 또는 루틴입니다. 예를 들어 일부 물리 연산자는 테이블, 인덱스 또는 뷰에서 열이나 행에 액세스합니다. 다른 물리 연산자는 계산, 집계, 데이터 무결성 검사 또는 조인 같은 다른 작업을 수행합니다. 물리 연산자는 비용과 관련이 있습니다.  
  
 물리 연산자는 초기화하고 데이터를 수집하며 종료합니다. 특히 물리 연산자는 다음 3개의 메서드 호출에 응답할 수 있습니다.  
  
-   **Init()**: **Init()** 메서드는 물리 연산자가 초기화하고 필요한 데이터 구조를 설정하도록 합니다. 일반적으로 물리 연산자는 하나의 **Init()** 호출을 받지만 여러 개의 호출을 받을 수도 있습니다.  
  
-   **GetNext()**: **GetNext()** 메서드는 물리 연산자가 처음 또는 다음 데이터 행을 가져오도록 합니다. 물리 연산자는 **GetNext()** 호출을 받지 않을 수도 있고 여러 개의 호출을 받을 수도 있습니다.  
  
-   **Close()**: **Close()** 메서드는 물리 연산자가 정리 작업을 수행하고 종료하도록 합니다. 물리 연산자는 하나의 **Close()** 호출만 받습니다.  
  
**GetNext()** 메서드는 하나의 데이터 행을 반환하며 호출 횟수는 SET STATISTICS PROFILE ON 또는 SET STATISTICS XML ON을 사용하여 생성된 실행 계획 출력에 **ActualRows**로 나타납니다. 이러한 SET 옵션에 대한 자세한 내용은 [SET STATISTICS PROFILE&#40;Transact-SQL&#41;](../t-sql/statements/set-statistics-profile-transact-sql.md) 및 [SET STATISTICS XML&#40;Transact-SQL&#41;](../t-sql/statements/set-statistics-xml-transact-sql.md)을 참조하세요.  
  
실행 계획 출력에 나타나는 **ActualRebinds** 및 **ActualRewinds** 개수는 **Init()** 메서드가 호출된 횟수를 나타냅니다. 연산자가 루프 조인의 내부 측면에 있지 않으면 **ActualRebinds** 는 1이고 **ActualRewinds** 는 0입니다. 연산자가 루프 조인의 내부 측면에 있으면 다시 바인딩 횟수와 되감기 횟수의 합계가 조인 외부 측면에서 처리된 행 수와 같아야 합니다. 다시 바인딩은 조인의 상호 관련된 매개 변수가 하나 이상 변경되었으며 내부 측면을 다시 평가해야 함을 의미합니다. 되감기는 상호 관련된 매개 변수가 변경되지 않았으며 이전 내부 결과 집합을 다시 사용할 수 있음을 의미합니다.  
  
**ActualRebinds** 및 **ActualRewinds** 는 SET STATISTICS XML ON을 사용하여 생성된 XML 실행 계획 출력에 표시되며 **Nonclustered Index Spool**, **Remote Query**, **Row Count Spool**, **Sort**, **Table Spool**및 **Table-valued Function** 연산자에 대해서만 채워집니다. **ActualRebinds** 및 **ActualRewinds** 는 **StartupExpression** 특성이 TRUE로 설정되어 있을 때 **Assert** 및 **Filter** 연산자에 대해서도 채워질 수 있습니다.  
  
**ActualRebinds** 와 **ActualRewinds** 가 XML 실행 계획에 있을 경우 **EstimateRebinds** 및 **EstimateRewinds**와 같습니다. 두 값이 없으면 예상 행 수(**EstimateRows**)가 실제 행 수(**ActualRows**)와 같으며 실제 그래픽 실행 계획 출력에 실제 다시 바인딩 횟수와 실제 되감기 횟수가 모두 0으로 표시됩니다.  
  
관련 카운터인 **ActualEndOfScans**는 SET STATISTICS XML ON을 사용하여 실행 계획 출력이 생성된 경우에만 사용할 수 있습니다. 이 카운터는 물리 연산자가 데이터 스트림의 끝에 도달할 때마다 1씩 증가합니다. 물리 연산자는 데이터 스트림의 끝에 도달하지 않거나 1회 이상 여러 번 도달할 수 있습니다. 다시 바인딩 및 되감기와 마찬가지로 검색 끝 수도 연산자가 루프 조인의 내부 측면에 있는 경우에만 둘 이상이 될 수 있습니다. 검색 끝 수는 다시 바인딩 횟수와 되감기 횟수의 합계보다 작거나 같아야 합니다.  
  
## <a name="mapping-physical-and-logical-operators"></a>물리 및 논리 연산자 매핑  
 쿼리 최적화 프로그램은 쿼리 계획을 논리 연산자로 이루어진 트리로 만듭니다. 쿼리 최적화 프로그램은 쿼리 계획을 만든 다음 각 논리 연산자에 대해 가장 효율적인 물리 연산자를 선택합니다. 쿼리 최적화 프로그램은 비용에 기반을 둔 방법을 사용하여 논리 연산자를 구현할 물리 연산자를 결정합니다.  
  
 일반적으로 여러 물리 연산자가 하나의 논리 연산자를 구현할 수 있습니다. 그러나 간혹 하나의 물리 연산자가 여러 논리 연산자를 구현하는 경우도 있습니다.  
  
## <a name="operator-descriptions"></a>연산자 설명  
 이 섹션에서는 논리 및 물리 연산자에 대해 설명합니다.  
  
|그래픽 실행 계획 아이콘|실행 계획 연산자|설명|  
|-----------------------------------|-----------------------|-----------------|  
|![적응형 조인 연산자 아이콘](../relational-databases/media/AdaptiveJoin.gif "적응형 조인 연산자 아이콘")|**적응형 조인**|**적응형 조인** 연산자를 사용하면 해시 조인 또는 중첩된 루프 조인 메서드 선택을 첫 번째 입력이 검사된 후까지 지연할 수 있습니다. | 
|없음|**집계**|**Aggregate** 연산자는 MIN, MAX, SUM, COUNT 또는 AVG를 포함하는 식을 계산합니다. **Aggregate** 연산자는 논리 또는 물리 연산자입니다.| 
|![Arithmetic expression 연산자 아이콘](../relational-databases/media/arithmetic-expression-32x-2.gif "Arithmetic expression operator icon")|**Arithmetic Expression**|**Arithmetic Expression** 연산자는 한 행의 기존 값에서 새 값을 계산합니다. **에서는** Arithmetic Expression [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]이 사용되지 않습니다.| 
|없음|**Async Concat**|**Async Concat** 연산자는 원격 쿼리(분산 쿼리)에서만 사용됩니다. Asnyc Concat은 부모 노드 하나와 *n* 개의 자식 노드를 포함합니다. 일반적으로 일부 자식 노드는 분산 쿼리에 참여하는 원격 컴퓨터에 해당합니다. **Asnyc Concat**은 모든 자식에게 동시에 `open()` 호출을 수행한 다음 각 자식에게 비트맵을 적용합니다. 값이 1인 각 비트에 대해 **Async Concat** 은 요청 시 출력 행을 부모 노드로 보냅니다.| 
|![Assert 연산자 아이콘](../relational-databases/media/assert-32x.gif "Assert operator icon")|**StartupExpression**|**Assert** 연산자는 조건을 확인합니다. 예를 들어 참조 무결성을 확인하거나 스칼라 하위 쿼리에서 한 개의 행을 반환하게 합니다. **Assert** 연산자는 각 입력 행에 대해 실행 계획의 **Argument** 열의 식을 계산합니다. 이 식이 NULL이면 **Assert** 연산자를 통해 행이 전달되고 쿼리 실행을 계속합니다. 이 식이 NULL이 아니면 해당 오류가 발생합니다. **Assert** 연산자는 물리 연산자입니다.| 
|![Assign 언어 요소 아이콘](../relational-databases/media/assign-32.gif "Assign language element icon")|**Assign**|**Assign** 연산자는 식 값 또는 상수 값을 변수에 할당합니다. **Assign** 는 언어 요소입니다.| 
|![Bitmap 연산자 아이콘](../relational-databases/media/bitmap-32x.gif "Bitmap operator icon")|**Bitmap Create**|**Bitmap Create** 연산자는 비트맵이 작성된 실행 계획 출력에 나타납니다. **Bitmap Create** 는 논리 연산자입니다.| 
|![Bitmap 연산자 아이콘](../relational-databases/media/bitmap-32x.gif "Bitmap operator icon")|**Bitmap**|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 **Bitmap** 연산자를 사용하여 병렬 쿼리 계획에 비트맵 필터링을 구현합니다. 비트맵 필터링은 **Parallelism** 연산자 같은 다른 연산자로 행을 전달하기 전에 조인 레코드를 생성할 수 없는 키 값을 가진 행을 제거하여 쿼리의 실행 속도를 높입니다. 비트맵 필터는 연산자 트리의 한 부분에 있는 테이블의 값 집합에 대한 압축된 표현을 사용하여 트리의 다른 부분에 있는 다른 테이블에서 행을 필터링합니다. 쿼리 초기 단계에서 필요 없는 행을 제거하면 이후 연산자에서 작업할 행 수가 더 적어지고 쿼리의 전체적인 성능이 향상됩니다. 최적화 프로그램은 비트맵이 유용할 만큼 충분히 선택 가능성이 높아지는 시점과 필터를 적용할 연산자를 판단합니다. **Bitmap** 는 물리 연산자입니다.| 
|![Bookmark lookup 연산자 아이콘](../relational-databases/media/bookmark-lookup-32x.gif "Bookmark lookup operator icon")|**Bookmark Lookup**|**Bookmark Lookup** 연산자는 책갈피(행 ID 또는 클러스터링 키)를 사용하여 테이블이나 클러스터형 인덱스에서 해당 행을 조회합니다. **Argument** 열에는 테이블이나 클러스터형 인덱스에서 행을 조회할 때 사용하는 책갈피 레이블이 포함됩니다. **Argument** 열에는 행을 조회하는 테이블 또는 클러스터형 인덱스의 이름도 포함됩니다. WITH PREFETCH 절이 **Argument** 열에 나타나는 경우에 쿼리 프로세서에서는 테이블 또는 클러스터형 인덱스에서 책갈피를 조회할 때 비동기 사전 인출(미리 읽기)을 사용하는 것을 최적의 방법으로 결정합니다.<br /><br /> [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]부터는 **Bookmark Lookup**이 사용되지 않습니다. 대신 **Key Lookup** 및 **RID Lookup**이 책갈피 조회 기능을 제공합니다.| 
|없음|**Branch Repartition**|병렬 쿼리 계획에는 반복자라는 개념 영역이 존재하기도 합니다. 이 영역에 있는 모든 반복자는 병렬 스레드에 의해 실행될 수 있습니다. 영역 자체는 직렬로 실행되어야 합니다. 개별 영역 내에 있는 일부 **Parallelism** 반복자를 **Branch Repartition**이라고 합니다. 이러한 두 영역의 경계에 있는 **Parallelism** 반복자를 **Segment Repartition**이라고 합니다. **Branch Repartition** 과 **Segment Repartition** 은 논리 연산자입니다.| 
|없음|**Broadcast**|**Broadcast** 에는 자식 노드가 하나 있고 부모 노드가 *n* 개 있습니다. **Broadcast** 는 요청 시 여러 소비자에게 입력 행을 보냅니다. 각 소비자는 모든 행을 받습니다. 예를 들어 모든 소비자가 해시 조인의 양쪽에 생성되면 *n* 개의 해시 테이블 복사본이 생성됩니다.| 
|![Build hash 연산자 아이콘](../relational-databases/media/build-hash.gif "Build hash operator icon")|**Build Hash**|xVelocity 메모리 최적화 columnstore 인덱스에 대한 일괄 해시 테이블의 빌드를 나타냅니다.| 
|없음|**Cache**|**Cache** 는 **Spool** 연산자의 특수 버전입니다. 이 연산자는 한 행의 데이터만 저장합니다. **Cache** 는 논리 연산자입니다. **에서는** Cache [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]가 사용되지 않습니다.| 
|![Clustered index delete 연산자 아이콘](../relational-databases/media/clustered-index-delete-32x.gif "Clustered index delete operator icon")|**Clustered Index Delete**|**Clustered Index Delete** 연산자는 쿼리 실행 계획의 Argument 열에 지정된 클러스터형 인덱스에서 행을 삭제합니다. Argument 열에 WHERE:() 조건자가 있으면 조건자에 부합되는 행만 삭제됩니다.**Clustered Index Delete** 는 물리 연산자입니다.| 
|![Clustered index insert 연산자 아이콘](../relational-databases/media/clustered-index-insert-32x.gif "Clustered index insert operator icon")|**Clustered Index Insert**|**Clustered Index Insert** 실행 계획 연산자는 해당 입력의 행을 Argument 열에 지정된 클러스터형 인덱스에 삽입합니다. Argument 열에는 각 열의 설정 값을 나타내는 SET:() 조건자도 포함됩니다. **Clustered Index Insert** 에 삽입 값에 대한 자식이 없는 경우 삽입된 행을 **Insert** 연산자 자체에서 가져옵니다.**Clustered Index Insert** 는 물리 연산자입니다.| 
|![Clustered index merge 연산자](../relational-databases/media/clustered-index-merge-32x.gif "Clustered index merge operator")|**Clustered Index Merge**|**Clustered Index Merge** 연산자는 병합 데이터 스트림을 클러스터형 인덱스에 적용합니다. 이 연산자는 연산자의 **Argument** 열에 지정된 클러스터형 인덱스에서 행을 삭제, 업데이트 또는 삽입합니다. 연산자의 **Argument** 열에서 지정한 **ACTION** 열의 런타임 값에 따라 실제 작업이 수행됩니다. **Clustered Index Merge** 는 물리 연산자입니다.| 
|![Clustered index scan 연산자 아이콘](../relational-databases/media/clustered-index-scan-32x.gif "Clustered index scan operator icon")|**Clustered Index Scan**|**Clustered Index Scan** 연산자는 쿼리 실행 계획의 Argument 열에 지정된 클러스터형 인덱스를 검색합니다. 선택 사항인 WHERE:() 조건자가 있는 경우에는 조건자에 부합되는 행만 반환됩니다. Argument 열에 ORDERED 절이 있으면 쿼리 프로세서가 행의 출력이 클러스터형 인덱스에 의해 정렬되는 순서로 반환되도록 요청한 것입니다. ORDERED 절이 없으면 저장소 엔진은 출력을 정렬하지 않고 최적의 방법으로 인덱스를 검색합니다. **Clustered Index Scan** 은 논리 및 물리 연산자입니다.| 
|![Clustered index seek 연산자 아이콘](../relational-databases/media/clustered-index-seek-32x.gif "Clustered index seek operator icon")|**Clustered Index Seek**|**Clustered Index Seek** 연산자는 인덱스의 검색 기능을 사용하여 클러스터형 인덱스에서 행을 검색합니다. **Argument** 열에는 사용할 클러스터형 인덱스의 이름 및 SEEK:() 조건자가 있습니다. 저장소 엔진은 이 인덱스를 사용하여 SEEK:() 조건자에 부합되는 행만 처리합니다. 또한 저장소 엔진은 SEEK:() 조건자에 부합되는 행에 대해서만 평가를 수행하는 WHERE:() 조건자를 포함할 수 있지만 이는 선택적이며 이 작업을 완료하는 데는 인덱스를 사용하지 않습니다.<br /><br /> **Argument** 열에 ORDERED 절이 있으면 쿼리 프로세서는 클러스터형 인덱스가 정렬한 순서대로 행을 반환합니다. ORDERED 절이 없으면 저장소 엔진은 출력을 정렬하지 않고 최적의 방법으로 인덱스를 검색합니다. 출력 순서를 유지하는 것보다 정렬하지 않고 출력하는 것이 더 효율적일 수 있습니다. 키워드 LOOKUP을 사용하면 책갈피 조회가 수행됩니다. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전에서는 **Key Lookup** 연산자가 책갈피 조회 기능을 제공합니다. **Clustered Index Seek** 은 논리/물리 연산자입니다.| 
|![Clustered index update 연산자 아이콘](../relational-databases/media/clustered-index-update-32x.gif "Clustered index update operator icon")|**Clustered Index Update**|**Clustered Index Update** 연산자는 **Argument** 열에 지정된 클러스터형 인덱스의 입력 행을 업데이트합니다. WHERE:() 조건자가 있는 경우에는 조건자에 부합되는 행만 업데이트됩니다. SET:() 조건자가 있는 경우에는 업데이트된 각 열이 이 값으로 설정됩니다. DEFINE:() 조건자가 있는 경우에는 이 연산자가 정의하는 값이 나열됩니다. 이러한 값은 SET 절 또는 이 연산자의 다른 곳과 이 쿼리 내의 다른 곳에서 참조될 수 있습니다. **Clustered Index Update** 은 논리 및 물리 연산자입니다.| 
|![Collapse 연산자 아이콘](../relational-databases/media/collapse-32x.gif "Collapse operator icon")|**축소**|**Collapse** 연산자는 업데이트 처리를 최적화합니다. 업데이트 처리는 **Split** 연산자를 사용하여 삭제와 삽입으로 분리할 수 있습니다. **Argument** 열에는 키 열 목록을 지정하는 GROUP BY:() 절이 포함됩니다. 쿼리 프로세서가 동일한 키 값을 삭제 및 삽입하는 인접 행을 발견하면 별개의 두 작업을 보다 효율적인 한 개의 업데이트 작업으로 교체합니다. **Collapse** 은 논리 및 물리 연산자입니다.| 
|![Columnstore 인덱스 검색](../relational-databases/media/columnstoreindexscan.gif "Columnstore 인덱스 검색")|**Columnstore 인덱스 검색**|**Columnstore Index Scan** 연산자는 쿼리 실행 계획의 **Argument** 열에 지정된 Columnstore 인덱스를 검색합니다.| 
|![Compute scalar 연산자 아이콘](../relational-databases/media/compute-scalar-32x.gif "Compute scalar operator icon")|**Compute Scalar**|**Compute Scalar** 연산자는 식을 계산하여 계산된 스칼라 값을 만듭니다. 이 값은 사용자에 반환되거나 그 외에 쿼리에서 참조되거나 둘 다일 수 있습니다. 예를 들어 두 작업은 모두 필터 조건자 또는 조인 조건자에서 수행됩니다. **Compute Scalar** 는 논리 및 물리 연산자입니다.<br /><br /> SET STATISTICS XML에 의해 생성된 실행 계획에 나타나는**Compute Scalar** 연산자는 **RunTimeInformation** 요소를 포함할 수 없습니다. **에서**실제 실행 계획 포함 **옵션을 선택하면 그래픽 실행 계획의**속성 **창에** 실제 행 수 **,** 실제 다시 바인딩 횟수 **및** 실제 되감기 횟수 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]가 표시되지 않을 수도 있습니다. 이 경우 컴파일된 쿼리 계획에서 이러한 연산자가 사용된 경우에도 런타임 쿼리 계획의 다른 연산자가 해당 작업을 수행한 것입니다. 또한 SET STATISTICS PROFILE로 만든 실행 계획 출력의 실행 수는 SET STATISTICS XML로 만든 실행 계획의 다시 바인딩 및 다시 감기의 합과 같습니다.| 
|![Concatenation 연산자 아이콘](../relational-databases/media/concatenation-32x.gif "Concatenation operator icon")|**Concatenation**|**Concatenation** 연산자는 여러 개의 입력을 검색하고 검색된 각 행을 반환합니다. **Concatenation** 은 일반적으로 [!INCLUDE[tsql](../includes/tsql-md.md)] UNION ALL 구조를 구현하는 데 사용됩니다. **Concatenation** 물리 연산자에는 두 개 이상의 입력과 한 개의 출력이 있습니다. Concatenation은 첫 번째 입력 스트림에서 출력 스트림으로 행을 복사한 다음 이 연산을 각 추가 입력 스트림에 대해 반복합니다. **Concatenation** 은 논리 및 물리 연산자입니다.| 
|![Constant scan 연산자 아이콘](../relational-databases/media/constant-scan-32x.gif "Constant scan operator icon")|**Constant Scan**|**Constant Scan** 연산자는 하나 이상의 상수 행을 쿼리에 사용하며 **Compute Scalar** 연산자는 **Constant Scan** 연산자로 생성된 행에 열을 추가하기 위해 **Constant Scan** 뒤에 사용되는 경우가 많습니다.| 
|![Convert(데이터베이스 엔진) 언어 요소 아이콘](../relational-databases/media/convert-32x.gif "Convert (Database Engine) language element icon")|**변환**|**Convert** 연산자는 스칼라 데이터 형식을 다른 형식으로 변환합니다. **Convert** 는 언어 요소입니다.| 
|없음|**Cross Join**|**Cross Join** 논리 연산자는 첫 번째(최상위) 입력의 각 행을 두 번째(최하위) 입력의 각 행과 조인합니다. **Cross Join** 는 논리 연산자입니다.| 
|없음|**커서**|**Cursor** 논리 및 물리 연산자는 커서 작업이 수반되는 쿼리 또는 업데이트가 실행되는 방식을 설명하기 위해 사용합니다. 물리 연산자는 커서를 처리하는 데 사용하는 물리적 구현 알고리즘(예: 키 집합 커서의 사용)을 설명합니다. 커서 실행의 각 단계마다 물리 연산자가 수반됩니다. 논리 연산자는 커서의 속성(예: 커서가 읽기 전용임)을 설명합니다.<br /><br /> 논리 연산자에는 Asynchronous, Optimistic, Primary, Read Only, Scroll Locks, Secondary 및 Synchronous가 있습니다.<br /><br /> 물리 연산자에는 Dynamic, Fetch Query, Keyset, Population Query, Refresh Query 및 Snapshot이 있습니다.| 
|![Cursor catchall 커서 연산자 아이콘](../relational-databases/media/cursor-catch-all.gif "Cursor catchall cursor operator icon")|**캐치올**|그래픽 실행 계획을 생성하는 논리에서 반복자에 적합한 아이콘을 찾지 못하면 캐치올 아이콘이 표시됩니다. 캐치올 아이콘이 반드시 오류 상태를 나타내는 것은 아닙니다. 캐치올 아이콘은 파랑(반복자), 주황(커서) 및 녹색( [!INCLUDE[tsql](../includes/tsql-md.md)] 언어 요소)의 3가지 유형이 있습니다.| 
|![Declare 언어 요소 아이콘](../relational-databases/media/declare-32x.gif "Declare language element icon")|**Declare**|**Declare** 연산자는 쿼리 계획에 지역 변수를 할당합니다. **Declare** 는 언어 요소입니다.| 
|![Delete(데이터베이스 엔진) 연산자 아이콘](../relational-databases/media/delete-32x.gif "Delete (Database Engine) operator icon")|**Delete**|**Delete** 연산자는 **Argument** 열의 선택적 조건자에 부합되는 개체 행에서 삭제됩니다.| 
|![Delete scan 연산자 아이콘](../relational-databases/media/delete-scan-32x.gif "Delete scan operator icon")|**Deleted Scan**|**Deleted Scan** 연산자는 트리거 내에서 삭제된 테이블을 검색합니다.| 
|없음|**Distinct Sort**|**Distinct Sort** 논리 연산자는 입력을 검색하며 중복 요소를 제거하고 **Argument** 열의 DISTINCT ORDER BY:() 조건자에 지정된 열을 기준으로 정렬합니다. **Distinct Sort** 는 논리 연산자입니다.| 
|없음|**Distinct**|**Distinct** 연산자는 행 집합 또는 값 컬렉션에서 중복 요소를 제거합니다. **Distinct** 는 논리 연산자입니다.| 
|![Distribute streams parallelism 연산자 아이콘](../relational-databases/media/parallelism-distribute-stream.gif "Distribute streams parallelism operator icon")|**Distribute Streams**|**Distribute Streams** 연산자는 병렬 쿼리 계획에서만 사용됩니다. **Distribute Streams** 연산자는 레코드의 단일 입력 스트림을 사용하여 여러 개의 출력 스트림을 만듭니다. 레코드 내용과 형식은 변경되지 않습니다. 입력 스트림의 각 레코드는 출력 스트림 중 하나에 표시됩니다. 이 연산자는 입력 레코드의 상대적인 순서를 출력 스트림에서 자동으로 유지합니다. 대개 특정 입력 레코드가 어떤 출력 스트림에 포함될지 결정하는 데는 해시가 사용됩니다.<br /><br /> 출력이 분할되는 경우에는 **Argument** 열에 PARTITION COLUMNS:() 조건자와 분할 열이 포함됩니다. **Distribute Streams** 는 논리 연산자입니다.| 
|![Dynamic 커서 연산자 아이콘](../relational-databases/media/dynamic-32x.gif "Dynamic cursor operator icon")|**Dynamic**|**Dynamic** 연산자는 다른 커서가 변경한 모든 내용을 볼 수 있는 커서를 사용합니다.| 
|![Fetch query 커서 연산자 아이콘](../relational-databases/media/fetch-query-32x.gif "Fetch query cursor operator icon")|**Fetch Query**|이 **Fetch Query** 연산자는 커서에 대해 인출이 실행될 때 행을 검색합니다.| 
|![Filter(데이터베이스 엔진) 연산자 아이콘](../relational-databases/media/filter-32x.gif "Filter (Database Engine) operator icon")|**Assert**|**Filter** 연산자는 입력을 검색하고 **Argument** 열에 표시되는 필터 식(조건자)에 부합되는 행만 반환합니다.| 
|없음|**Flow Distinct**|**Flow Distinct** 논리 연산자는 입력을 검색하며 중복 요소를 제거합니다. **Distinct** 연산자는 출력을 만들기 전에 모든 입력을 사용하지만 **FlowDistinct** 연산자는 각 행을 입력으로부터 가져올 때 반환합니다(행이 중복 요소인 관계로 삭제되지 않는 경우).| 
|![외래 키 참조 확인 연산자 아이콘](../relational-databases/media/fk-references-32x.gif "외래 키 참조 확인 연산자 아이콘")|**외래 키 참조 확인**|**외래 키 참조 확인** 연산자는 수정된 행을 참조 테이블의 행과 비교하여 참조 무결성을 손상시키지 않는지 확인하여 참조 무결성 검사를 제 위치에서 수행합니다. 동일한 기본 키 또는 고유 키에 253개가 넘는 외래 키 참조가 있는 경우 **외래 키 참조 확인** 연산자가 사용됩니다. **외래 키 참조 확인**은 논리적이고 물리적인 연산자입니다.| 
|없음|**Full Outer Join**|**Full Outer Join** 논리 연산자는 두 번째(최하위) 입력의 각 행과 조인된 첫 번째(최상위) 입력의 조인 조건자에 부합되는 각 행을 반환합니다. 다음 항목으로부터 행을 반환하기도 합니다.<br /><br /> -두 번째 입력과 일치하는 요소가 없는 첫 번째 입력<br /><br /> -첫 번째 입력과 일치하는 요소가 없는 두 번째 입력<br /><br /> 일치되는 값이 없는 입력은 Null 값으로 반환됩니다. **Full Outer Join** 는 논리 연산자입니다.| 
|![Gather streams parallelism 연산자 아이콘](../relational-databases/media/parallelism-32x.gif "Gather streams parallelism operator icon")|**Gather Streams**|**Gather Streams** 연산자는 병렬 쿼리 계획에서만 사용됩니다. **Gather Streams** 연산자는 몇 개의 입력 스트림을 사용하고 해당 입력 스트림을 결합하여 레코드의 단일 출력 스트림을 만듭니다. 레코드 내용과 형식은 변경되지 않습니다. 이 연산자가 순서를 그대로 유지하는 경우에는 모든 입력 스트림이 정렬되어야 합니다. 출력이 정렬되는 경우에는 **Argument** 열에 ORDER BY:() 조건자와 정렬될 열 이름이 포함됩니다. **Gather Streams** 는 논리 연산자입니다.| 
|![Hash match 연산자 아이콘](../relational-databases/media/hash-match-32x.gif "Hash match operator icon")|**Hash Match**|**Hash Match** 연산자는 빌드 입력으로부터 각 행에 대한 해시 값을 계산하여 해시 테이블을 작성합니다. HASH:() 조건자는 해시 값을 만들기 위해 사용하는 열 목록과 함께 **Argument** 열에 포함됩니다. 이 조건자는 각 검색 행에 대해 동일한 해시 함수를 사용하여 해시 값을 계산하고 해시 테이블에서 일치하는 항목을 찾습니다. 잔여 조건자( **Argument** 열에서 RESIDUAL:()로 식별됨)가 있으면 이 역시 만족해야 일치 항목으로 판단됩니다. 수행되는 논리 연산에 따라 다음과 같이 동작이 달라집니다.<br /><br /> -모든 조인에 대해 첫 번째(최상위) 입력을 사용하여 해시 테이블을 작성하고 두 번째(최하위) 입력을 사용하여 해시 테이블을 검색합니다. 출력은 조인 유형으로 지정된 대로 일치(또는 불일치)됩니다. 여러 조인에서 같은 조인 열을 사용하는 경우에는 이러한 연산이 해시 팀으로 그룹화됩니다.<br /><br /> -distinct 또는 aggregate 연산자에 대해서는 입력을 사용하여 해시 테이블을 작성합니다. 이때 중복 요소는 제거하고 모든 집계 식을 계산합니다. 해시 테이블이 작성되면 테이블을 검색하고 모든 항목을 출력합니다.<br /><br /> -union 연산자에 대해서는 첫 번째 입력을 사용하여 해시 테이블을 작성합니다. 이때 중복 요소는 제거합니다. 다음 두 번째 입력(중복 요소가 없어야 함)을 사용하여 해시 테이블을 검색하고 일치되는 항목이 없는 모든 행을 반환한 뒤 해시 테이블을 검색하여 모든 항목을 반환합니다.<br /><br /> **Hash Match** 는 물리 연산자입니다.| 
|![If 언어 요소 아이콘](../relational-databases/media/if-32x.gif "If language element icon")|**If**|**If** 연산자는 식을 기준으로 조건부 처리를 수행합니다. **If** 는 언어 요소입니다.| 
|없음|**Inner Join**|**Inner Join** 논리 연산자는 첫 번째(최상위) 입력과 두 번째(최하위) 입력의 조인에 부합되는 각 행을 반환합니다.| 
|![Insert(데이터베이스 엔진) 연산자 아이콘](../relational-databases/media/insert-32x.gif "Insert (Database Engine) operator icon")|**Insert**|**Insert** 논리 연산자는 입력의 각 행을 **Argument** 열에 지정된 개체에 삽입합니다. 물리 연산자는 **Table Insert**, **Index Insert**또는 **Clustered Index Insert** 연산자입니다.| 
|![Inserted scan 연산자 아이콘](../relational-databases/media/inserted-scan-32x.gif "Inserted scan operator icon")|**Inserted Scan**|**Inserted Scan** 연산자는 **inserted** 테이블을 검색합니다. **Inserted Scan** 은 논리 및 물리 연산자입니다.| 
|![Intrinsic 언어 요소 아이콘](../relational-databases/media/intrinsic-32x.gif "Intrinsic language element icon")|**Intrinsic**|**Intrinsic** 연산자는 내부 [!INCLUDE[tsql](../includes/tsql-md.md)] 함수를 호출합니다. **Intrinsic** 는 언어 요소입니다.| 
|![Iterator catchall 연산자 아이콘](../relational-databases/media/iterator-catch-all.gif "Iterator catchall operator icon")|**Iterator**|그래픽 실행 계획을 생성하는 논리에서 반복자에 적합한 아이콘을 찾지 못하면 **Iterator** 캐치올 아이콘이 표시됩니다. 캐치올 아이콘이 반드시 오류 상태를 나타내는 것은 아닙니다. 캐치올 아이콘은 파랑(반복자), 주황(커서) 및 녹색( [!INCLUDE[tsql](../includes/tsql-md.md)] 언어 구문)의 3가지 유형이 있습니다.| 
|![Bookmark lookup 연산자 아이콘](../relational-databases/media/bookmark-lookup-32x.gif "Bookmark lookup operator icon")|**Key Lookup**|**Key Lookup** 연산자는 클러스터형 인덱스가 있는 테이블의 책갈피 조회입니다. **Argument** 열에는 클러스터형 인덱스의 이름과 클러스터형 인덱스에서 행을 조회할 때 사용되는 클러스터링 키가 포함됩니다. **Key Lookup** 은 항상 **Nested Loops** 연산자와 함께 사용됩니다. WITH PREFETCH 절이 **Argument** 열에 나타나는 경우에 쿼리 프로세서에서는 클러스터형 인덱스에서 책갈피를 조회할 때 비동기 사전 인출(미리 읽기)을 사용하는 것을 최적의 방법으로 결정합니다.<br /><br /> 쿼리 계획에서 **Key Lookup** 연산자를 사용하는 것은 쿼리에서 성능 튜닝의 장점을 활용할 수 있음을 나타냅니다. 예를 들어 포함 인덱스를 추가하여 쿼리 성능을 향상시킬 수 있습니다.| 
|![Keyset 커서 연산자 아이콘](../relational-databases/media/keyset-32x.gif "Keyset cursor operator icon")|**Keyset**|**Keyset** 연산자는 다른 사용자의 업데이트 내용은 볼 수 있지만 삽입 내용은 볼 수 없는 커서를 사용합니다.| 
|![Language element 캐치올 아이콘](../relational-databases/media/language-construct-catch-all.gif "Language element catchall icon")|**Language 요소**|그래픽 실행 계획을 생성하는 논리에서 반복자에 적합한 아이콘을 찾지 못하면 **Language Element** 캐치올 아이콘이 표시됩니다. 캐치올 아이콘이 반드시 오류 상태를 나타내는 것은 아닙니다. 캐치올 아이콘은 파랑(반복자), 주황(커서) 및 녹색( [!INCLUDE[tsql](../includes/tsql-md.md)] 언어 구문)의 3가지 유형이 있습니다.| 
|없음|**Left Anti Semi Join**|**Left Anti Semi Join** 연산자는 두 번째(최하위) 입력에 일치 행이 없는 경우 첫 번째(최상위) 입력으로부터 각 행을 반환합니다. **Argument** 열에 조인 조건자가 없으면 각 행이 일치하는 행입니다. **Left Anti Semi Join** 는 논리 연산자입니다.| 
|없음|**Left Outer Join**|**Left Outer Join** 연산자는 첫 번째(최상위) 입력과 두 번째(최하위) 입력의 조인에 부합되는 각 행을 반환합니다. 또한 첫 번째 입력에서 두 번째 입력에 일치 행이 없는 행을 모두 반환합니다. 두 번째 입력에서 일치되지 않는 행은 Null 값으로 반환됩니다. **Argument** 열에 조인 조건자가 없으면 각 행이 일치하는 행입니다. **Left Outer Join** 는 논리 연산자입니다.| 
|없음|**Left Semi Join**|**Left Semi Join** 연산자는 첫 번째(최상위) 입력에 일치하는 행이 있는 경우 두 번째(최하위) 입력의 각 행을 반환합니다. **Argument** 열에 조인 조건자가 없으면 각 행이 일치하는 행입니다. **Left Semi Join** 는 논리 연산자입니다.| 
|![Log row scan 연산자 아이콘](../relational-databases/media/log-row-scan-32x.gif "Log row scan operator icon")|**Log Row Scan**|**Log Row Scan** 연산자는 트랜잭션 로그를 검색합니다. **Log Row Scan** 은 논리 및 물리 연산자입니다.| 
|![Merge interval 연산자 아이콘](../relational-databases/media/merge-interval-32x.gif "Merge interval operator icon")|**Merge Interval**|**Merge Interval** 연산자는 겹칠 수도 있는 여러 개의 간격을 병합하여 최소한의 겹치지 않는 간격을 생성하는데, 이 간격은 인덱스 항목 검색에 사용됩니다. 이 연산자는 주로 이 연산자가 병합하는 간격(행에서 열로 표시됨)을 만드는 **Constant Scan** 연산자보다 한 개 이상의 **Compute Scalar** 연산자 위에 나타납니다. **Merge Interval** 은 논리 및 물리 연산자입니다.| 
|![Merge join 연산자 아이콘](../relational-databases/media/merge-join-32x.gif "Merge join operator icon")|**병합 조인**|**Merge Join** 연산자는 내부 조인, 왼쪽 우선 외부 조인, 왼쪽 세미 조인, 왼쪽 앤티 세미 조인, 오른쪽 우선 외부 조인, 오른쪽 세미 조인, 오른쪽 앤티 세미 조인 및 합집합 논리 연산을 수행합니다.<br /><br /> **Argument** 열에서 **Merge Join** 연산자는 일 대 다 조인을 수행하는 경우에는 MERGE:() 조건자를 포함하고 다 대 다 조인을 수행하는 경우에는 MANY-TO-MANY MERGE:() 조건자를 포함합니다. **Argument** 열에는 연산을 수행하기 위해 사용되는 쉼표로 구분된 열 목록도 포함됩니다. **Merge Join** 연산자에는 쿼리 계획에 명시적인 정렬 연산을 삽입하여 해당 열을 기준으로 정렬된 2개의 입력이 필요합니다. Merge Join은 명시적인 정렬이 필요하지 않은 경우 예를 들면 데이터베이스에 적합한 B-트리 인덱스가 있거나 병합 조인과 롤업을 통한 그룹화와 같은 여러 개의 연산에 대해 정렬 순서를 사용할 수 있는 경우에 특히 효과적입니다. **Merge Join** 은 물리 연산자입니다.| 
|![Nested loops 연산자 아이콘](../relational-databases/media/nested-loops-32x.gif "Nested loops operator icon")|**Nested Loops**|**Nested Loops** 연산자는 내부 조인, 왼쪽 우선 외부 조인, 왼쪽 세미 조인 및 왼쪽 앤티 세미 조인 논리 연산을 수행합니다. 중첩 루프 조인에서는 대개 인덱스를 사용하여 내부 테이블에서 외부 테이블의 각 행을 검색합니다. 쿼리 프로세서는 예상 비용에 따라 내부 입력을 통한 인덱스 검색의 위치 정확성을 높이기 위해 외부 입력을 정렬할지 여부를 결정합니다. 수행 중인 논리 연산에 따라 **Argument** 열의 조건자(선택 사항)를 충족하는 모든 행이 반환됩니다. **Nested Loops** 는 물리 연산자입니다.| 
|![Nonclustered index delete 연산자 아이콘](../relational-databases/media/nonclust-index-delete-32x.gif "Nonclustered index delete operator icon")|**Nonclustered Index Delete**|**Nonclustered Index Delete** 연산자는 **Argument** 열에 지정된 비클러스터형 인덱스에서 입력 행을 삭제합니다. **Nonclustered Index Delete** 는 물리 연산자입니다.| 
|![Nonclustered index insert 연산자 아이콘](../relational-databases/media/nonclust-index-insert-32x.gif "Nonclustered index insert operator icon")|**Index Insert**|**Index Insert** 연산자는 입력으로부터의 행을 **Argument** 열에 지정된 비클러스터형 인덱스에 삽입합니다. **Argument** 열에는 각 열의 설정 값을 나타내는 SET:() 조건자도 포함됩니다. **Index Insert** 는 물리 연산자입니다.| 
|![Nonclustered index scan 연산자 아이콘](../relational-databases/media/nonclustered-index-scan-32x.gif "Nonclustered index scan operator icon")|**Index Scan**|**Index Scan** 연산자는 **Argument** 열에 지정한 비클러스터형 인덱스의 모든 행을 검색합니다. 선택 사항인 WHERE:() 조건자가 **Argument** 열에 나타나면 조건자에 부합되는 행만 반환됩니다. **Index Scan** 은 논리 및 물리 연산자입니다.| 
|![Nonclustered index seek 연산자 아이콘](../relational-databases/media/index-seek-32x.gif "Nonclustered index seek operator icon")|**Index Seek**|**Index Seek** 연산자는 인덱스 검색 기능을 사용하여 비클러스터형 인덱스에서 행을 검색합니다. **Argument** 열에는 사용할 비클러스터형 인덱스의 이름 및 SEEK:() 조건자도 포함됩니다. 저장소 엔진은 이 인덱스를 사용하여 SEEK:() 조건자에 부합되는 행만 처리합니다. 필요에 따라 저장소 엔진이 SEEK:() 조건자에 부합되는 모든 행에 대한 평가를 수행할 WHERE:() 조건자가 포함될 수도 있습니다(이 수행을 위해 인덱스를 사용하지는 않음). **Argument** 열에 ORDERED 절이 있으면 쿼리 프로세서는 클러스터형 인덱스가 정렬한 순서대로 행을 반환합니다. ORDERED 절이 없으면 저장소 엔진이 인덱스를 최적의 방법(출력 정렬은 보장하지 않음)으로 검색합니다. 출력 순서를 유지하는 것보다는 정렬되지 않은 출력을 만드는 것이 더 효율적일 수 있습니다. **Index Seek** 은 논리 및 물리 연산자입니다.| 
|![Nonclustered index spool 연산자 아이콘](../relational-databases/media/index-spool-32x.gif "Nonclustered index spool operator icon")|**Index Spool**|**Index Spool** 물리 연산자는 **Argument** 열에 SEEK:() 조건자를 포함합니다. **Index Spool** 연산자는 입력 행을 검색하고 각 행의 복사본을 숨겨진 스풀 파일( **tempdb** 데이터베이스에 저장되어 쿼리 사용 기간 중에만 존재함)에 배치하며 행에 대해 비클러스터형 인덱스를 작성합니다. 이렇게 하면 인덱스의 검색 기능을 사용하여 SEEK:() 조건자에 부합되는 행만 출력할 수 있습니다. 예를 들어 **Nested Loops** 연산자로 연산자를 다시 돌리지만 다시 바인딩할 필요가 없을 경우 입력 사항을 다시 검색하는 대신 스풀된 데이터를 사용합니다.| 
|![Nonclustered index update 연산자 아이콘](../relational-databases/media/nonclust-index-update-32x.gif "Nonclustered index update operator icon")|**Nonclustered Index Update**|**Nonclustered Index Update** 물리 연산자는 **Argument** 열에 지정된 비클러스터형 인덱스에 입력된 내용에서 행을 업데이트합니다. SET:() 조건자가 있는 경우에는 업데이트된 각 열이 이 값으로 설정됩니다. **Nonclustered Index Update** 는 물리 연산자입니다.| 
|![Online index insert 연산자 아이콘](../relational-databases/media/online-index-32x.gif "Online index insert operator icon")|**Online Index Insert**|**Online Index Insert** 물리 연산자는 인덱스, 만들기, 변경 또는 삭제 작업이 온라인으로 수행됨을 나타냅니다. 즉, 사용자가 인덱스 작업 동안 기본 테이블 데이터를 사용할 수 있습니다.| 
|없음|**Parallelism**|<a name="exchange"></a>**Parallelism** 연산자(또는 교환 반복기)는 Distribute Streams, Gather Streams 및 Repartition Streams 논리 연산을 수행합니다. **Argument** 열에는 PARTITION COLUMNS:() 조건자와 쉼표로 구분된 분할될 열 목록이 함께 포함될 수 있습니다. 또한 **Argument** 열에는 분할 동안 정렬 순서를 지정할 열을 나열하는 ORDER BY:() 조건자도 포함될 수 있습니다. **Parallelism** 은 물리 연산자입니다. Parallelism 연산자에 대한 자세한 내용은 [Craig Freedman의 블로그 시리즈](https://blogs.msdn.microsoft.com/craigfr/tag/parallelism/)를 참조하세요.<br /><br />**참고:** 쿼리가 병렬 쿼리로 컴파일되었지만 런타임에 직렬 쿼리로 실행되는 경우 SET STATISTICS XML이나 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 **실제 실행 계획 포함** 옵션을 사용하여 생성된 실행 계획 출력에는 **Parallelism** 연산자의 **RunTimeInformation** 요소가 포함되지 않습니다. SET STATISTICS PROFILE 출력에서 실제 행 개수와 실제 실행 수는 **Parallelism** 연산자에 대해 0으로 표시됩니다. 두 조건 중 하나가 발생할 경우 **Parallelism** 연산자가 쿼리 컴파일 중에만 사용되었으며 런타임 쿼리 계획에는 사용되지 않았음을 의미합니다. 서버에 동시 로드 양이 많으면 병렬 쿼리 계획이 직렬로 실행될 수 있습니다.| 
|![Parameter table scan 연산자 아이콘](../relational-databases/media/parameter-table-scan-32x.gif "Parameter table scan operator icon")|**Parameter Table Scan**|**Parameter Table Scan** 연산자는 현재 쿼리에서 매개 변수의 역할을 하는 테이블을 검색합니다. 일반적으로 이 연산자는 저장 프로시저 안에서 INSERT 쿼리에 사용합니다. **Parameter Table Scan** 은 논리 및 물리 연산자입니다.| 
|없음|**Partial Aggregate**|**Partial Aggregate** 는 병렬 계획에 사용됩니다. Partial Aggregate는 최대한 많은 입력 행에 집계 함수를 적용하여 디스크 쓰기("spill"이라고 함)가 필요가 없도록 합니다. **Hash Match** 는 파티션 집계를 구현하는 유일한 물리 연산자(반복자)입니다. **Partial Aggregate** 는 논리 연산자입니다.| 
|![Population query 커서 연산자 아이콘](../relational-databases/media/poulation-query-32x.gif "Population query cursor operator icon")|**Population Query**|**Population Query** 연산자는 커서가 열려 있을 때 커서의 작업 테이블을 채웁니다.| 
|![Refresh query 커서 연산자 아이콘](../relational-databases/media/refresh-query-32x.gif "Refresh query cursor operator icon")|**Refresh Query**|**Refresh Query** 연산자는 인출 버퍼에서 행에 대한 현재 데이터를 인출합니다.| 
|![Remote delete 연산자 아이콘](../relational-databases/media/remote-delete-32x.gif "Remote delete operator icon")|**Remote Delete**|**Remote Delete** 연산자는 원격 개체로부터의 입력 행을 삭제합니다. **Remote Delete** 은 논리 및 물리 연산자입니다.| 
|![remote index seek 실행 계획 연산자](../relational-databases/media/remote-index-scan-32x.gif "remote index seek 실행 계획 연산자")|**Remote Index Scan**|**Remote Index Scan** 연산자는 Argument 열에 지정한 원격 인덱스를 검색합니다. **Remote Insert Scan** 은 논리/물리 연산자입니다.| 
|![remote index seek 실행 계획 연산자](../relational-databases/media/remote-index-seek-32x.gif "remote index seek 실행 계획 연산자")|**Remote Index Seek**|**Remote Index Seek** 연산자는 원격 인덱스 개체의 검색 기능을 사용하여 행을 검색합니다. **Argument** 열에는 사용할 원격 인덱스의 이름 및 SEEK:()가 있습니다. **Remote Index Seek** 는 논리/물리 연산자입니다.| 
|![Remote insert 연산자 아이콘](../relational-databases/media/remote-insert-32x.gif "Remote insert operator icon")|**Remote Insert**|**Remote Insert** 연산자는 입력 행을 원격 개체에 삽입합니다. **Remote Insert** 는 논리/물리 연산자입니다.| 
|![Remote query 연산자 아이콘](../relational-databases/media/remote-query-32x.gif "Remote query operator icon")|**Remote Query**|**Remote Query** 연산자는 쿼리를 원격 원본으로 전송합니다. 원격 서버로 보내진 쿼리의 텍스트는 **Argument** 열에 표시됩니다. **Remote Query** 은 논리 및 물리 연산자입니다.| 
|![Remote scan 연산자 아이콘](../relational-databases/media/remote-scan-32x.gif "Remote scan operator icon")|**Remote Scan**|**Remote Scan** 연산자는 원격 개체를 검색합니다. 원격 개체 이름은 **Argument** 열에 표시됩니다. **Remote Scan** 은 논리 및 물리 연산자입니다.| 
|![Remote update 연산자 아이콘](../relational-databases/media/remote-update-32x.gif "Remote update operator icon")|**Remote Update**|**Remote Update** 연산자는 원격 개체에서 입력 행을 업데이트합니다. **Remote Update** 은 논리 및 물리 연산자입니다.| 
|![Repartition streams parallelism 연산자 아이콘](../relational-databases/media/parallelism-repartition-stream.gif "Repartition streams parallelism operator icon")|**Repartition Streams**|**Repartition Streams** 연산자(또는 교환 반복기)는 여러 개의 스트림을 사용하며 여러 개의 레코드 스트림을 만듭니다. 레코드 내용과 형식은 변경되지 않습니다. 쿼리 최적화 프로그램이 비트맵 필터를 사용하면 출력 스트림의 행 수가 줄어듭니다. 입력 스트림의 각 레코드가 한 개의 출력 스트림에 배치됩니다. 이 연산자가 순서를 그대로 유지하는 경우에는 모든 입력 스트림이 정렬되어 여러 개의 정렬된 출력 스트림으로 병합되어야 합니다. 출력이 분할되는 경우에는 **Argument** 열에 PARTITION COLUMNS:() 조건자와 분할 열이 포함됩니다. 출력이 정렬되는 경우에는 **Argument** 열에 ORDER BY:() 조건자와 정렬될 열이 포함됩니다. **Repartition Streams** 는 논리 연산자입니다. 이 연산자는 병렬 쿼리 계획에서만 사용됩니다.| 
|![Result 언어 요소 아이콘](../relational-databases/media/result-32x.gif "Result language element icon")|**결과**|**Result** 연산자는 쿼리 계획의 끝에 반환되는 데이터입니다. 이는 일반적으로 실행 계획의 루트 요소입니다. **Result** 는 언어 요소입니다.| 
|![RID lookup 연산자 아이콘](../relational-databases/media/rid-nonclust-locate-32x.gif "RID lookup operator icon")|**RID Lookup**|**RID Lookup** 은 제공된 RID(행 식별자)를 사용하여 힙을 조회하는 책갈피 조회입니다. **Argument** 열에는 테이블의 행을 조회하는 데 사용되는 책갈피 레이블 및 행을 조회할 테이블의 이름이 포함됩니다. **RID Lookup** 은 항상 NESTED LOOP JOIN과 함께 사용됩니다. **RID Lookup** 는 물리 연산자입니다. 책갈피 조회에 대한 자세한 내용은 MSDN SQL Server 블로그의 "[책갈피 조회(Bookmark Lookup)](https://go.microsoft.com/fwlink/?LinkId=132568)"를 참조하십시오.| 
|![Row count spool 연산자 아이콘](../relational-databases/media/remote-count-spool-32x.gif "Row count spool operator icon")|**Row Count Spool**|**Row Count Spool** 연산자는 입력을 검색하여 얼마나 많은 행이 있는지 계산하고 데이터는 포함되지 않은 상태로 그 수만큼의 행을 반환합니다. 이 연산자는 행에 포함된 데이터보다는 행 자체의 존재 유무를 검사하는 것이 중요한 경우에 사용합니다. 예를 들어 **Nested Loops** 연산자는 Left Semi Join 연산을 수행하고 조인 조건자는 내부 입력에 적용되는 경우 Row Count Spool이 **Nested Loops** 연산자의 내부 입력의 최상위에 배치될 수 있습니다. 그러면 내부의 실제 데이터가 필요하지 않기 때문에 **Nested Loops** 연산자가 Row Count Spool에 의해 출력되는 행 수를 보고 외부 행의 반환 여부를 결정할 수 있습니다. **Row Count Spool** 은 물리 연산자입니다.| 
|없음|**Right Anti Semi Join**|**Right Anti Semi Join** 연산자는 첫 번째(최상위) 입력에 일치하는 행이 없는 경우 두 번째(최하위) 입력의 각 행을 출력합니다. 일치하는 행은 **Argument** 열의 조건자에 부합되는 행으로 정의됩니다(조건자가 없으면 각 행이 일치 행임). **Right Anti Semi Join** 는 논리 연산자입니다.| 
|없음|**Right Outer Join**|**Right Outer Join** 연산자는 두 번째(최하위) 입력 중에서 첫 번째(최상위) 입력과 일치하는 각 행을 반환합니다. 또한 첫 번째 입력과 일치하지 않는 두 번째 입력의 모든 행도 NULL로 조인하여 반환합니다. **Argument** 열에 조인 조건자가 없으면 각 행이 일치하는 행입니다. **Right Outer Join** 는 논리 연산자입니다.| 
|없음|**Right Semi Join**|**Right Semi Join** 연산자는 첫 번째(최상위) 입력에 일치하는 행이 있는 경우 두 번째(최하위) 입력의 각 행을 반환합니다. **Argument** 열에 조인 조건자가 없으면 각 행이 일치하는 행입니다. **Right Semi Join** 는 논리 연산자입니다.| 
|![Segment 연산자 아이콘](../relational-databases/media/segment-32x.gif "Segment operator icon")|**Segment**|**Segment** 는 물리 및 논리 연산자입니다. 이 연산자는 하나 이상의 열 값에 따라 입력 집합을 세그먼트로 나눕니다. 이러한 열은 **Segment** 연산자의 인수로 표시됩니다. 그런 다음 연산자는 한 번에 한 세그먼트씩 출력합니다.| 
|![Sequence 연산자 아이콘](../relational-databases/media/sequence-32x.gif "Sequence operator icon")|**시퀀스**|**Sequence** 연산자는 광범위한 업데이트 계획을 실행합니다. 각 입력은 위에서 아래 방향으로 차례로 실행됩니다. 각 입력은 대개 서로 다른 개체의 업데이트이며 마지막(최하위) 입력으로부터의 행만 반환됩니다. **Sequence** 은 논리 및 물리 연산자입니다.| 
|![Sequence project 연산자 아이콘](../relational-databases/media/sequence-project-32x.gif "Sequence project operator icon")|**Sequence Project**|**Sequence Project** 연산자는 열을 추가하여 정렬된 집합에 대한 계산을 수행합니다. 이 연산자는 하나 이상의 열 값에 따라 입력 집합을 세그먼트로 나눕니다. 그런 다음 연산자는 한 번에 한 세그먼트씩 출력합니다. 이런 열은 **Sequence Project** 연산자에서 인수로 표시됩니다. **Sequence Project** 은 논리 및 물리 연산자입니다.| 
|없음|**Segment Repartition**|병렬 쿼리 계획에는 반복자라는 개념 영역이 존재하기도 합니다. 이 영역에 있는 모든 반복자는 병렬 스레드에 의해 실행될 수 있습니다. 영역 자체는 직렬로 실행되어야 합니다. 개별 영역 내에 있는 일부 **Parallelism** 반복자를 **Branch Repartition**이라고 합니다. 이러한 두 영역의 경계에 있는 **Parallelism** 반복자를 **Segment Repartition**이라고 합니다. **Branch Repartition** 과 **Segment Repartition** 은 논리 연산자입니다.| 
|![Snapshot 커서 연산자 아이콘](../relational-databases/media/snapshot-32x.gif "Snapshot cursor operator icon")|**스냅숏**|**Snapshot** 연산자는 다른 연산자가 만든 변경 내용을 확인하지 않는 커서를 만듭니다.| 
|![Sort 연산자 아이콘](../relational-databases/media/sort-32x.gif "Sort operator icon")|**Sort**|**Sort** 연산자는 모든 들어오는 행을 정렬합니다. **Argument** 열에는 이 작업으로 중복 요소가 제거되면 DISTINCT ORDER BY:() 조건자가 포함되거나 정렬될 열의 쉼표로 구분된 목록이 있으면 ORDER BY:() 조건자가 포함됩니다. 열이 오름차순으로 정렬되는 경우에는 ASC 값, 내림차순으로 정렬되는 경우에는 DESC 값이 열의 접두사로 사용됩니다. **Sort** 는 논리 및 물리 연산자입니다.| 
|![Split 연산자 아이콘](../relational-databases/media/split-32x.gif "Split operator icon")|**Split**|**Split** 연산자는 업데이트 과정을 최적화하는 데 사용됩니다. 즉, 각 업데이트 작업을 삭제 및 삽입 작업으로 분할합니다. **Split** 은 논리 및 물리 연산자입니다.| 
|![Spool 연산자 아이콘](../relational-databases/media/spool-32x.gif "Spool operator icon")|**Eager Spool**|**Eager Spool** 연산자는 전체 입력을 받아 각 행을 **tempdb** 데이터베이스에 저장된 숨겨진 임시 개체에 저장합니다. 예를 들어 **Nested Loops** 연산자로 연산자를 다시 돌리지만 다시 바인딩할 필요가 없을 경우 입력 사항을 다시 검색하는 대신 스풀된 데이터를 사용합니다. 다시 바인딩해야 하는 경우에는 스풀된 데이터를 삭제하고 다시 바인딩된 입력을 다시 검색하여 스풀 개체를 다시 작성합니다. **Eager Spool** 연산자는 "신속하게" 스풀 파일을 만듭니다. 스풀의 부모 연산자가 첫 번째 행을 요청하면 스풀 연산자는 입력 연산자로부터 모든 행을 받아 스풀에 저장합니다. **Eager Spool** 은 논리 연산자입니다.| 
|![Spool 연산자 아이콘](../relational-databases/media/spool-32x.gif "Spool operator icon")|**Lazy Spool**|**Lazy Spool** 논리 연산자는 입력된 각 행을 **tempdb** 데이터베이스에 저장된 숨겨진 임시 개체에 저장합니다. 예를 들어 **Nested Loops** 연산자로 연산자를 다시 돌리지만 다시 바인딩할 필요가 없을 경우 입력 사항을 다시 검색하는 대신 스풀된 데이터를 사용합니다. 다시 바인딩해야 하는 경우에는 스풀된 데이터를 삭제하고 다시 바인딩된 입력을 다시 검색하여 스풀 개체를 다시 작성합니다. **Lazy Spool** 연산자는 스풀 파일을 "지연" 방식으로 작성합니다. 즉, 스풀의 부모 연산자가 행을 요청할 때마다 스풀 연산자는 한 번에 모든 행을 사용하는 대신 입력 연산자로부터 하나의 행을 받아 스풀에 저장합니다. Lazy Spool은 논리 연산자입니다.| 
|![Spool 연산자 아이콘](../relational-databases/media/spool-32x.gif "Spool operator icon")|**Spool**|**Spool** 연산자는 **tempdb** 데이터베이스에 중간 쿼리 결과를 저장합니다.| 
|![Stream aggregate 연산자 아이콘](../relational-databases/media/stream-aggregate-32x.gif "Stream aggregate operator icon")|**Stream Aggregate**|**Stream Aggregate** 연산자는 하나 이상의 열로 행을 그룹화한 후 쿼리가 반환한 하나 이상의 집계 식을 계산합니다. 이 연산자의 출력은 쿼리에서 이후 연산자에 의해 참조되거나 클라이언트에 반환되거나 둘 다 수행될 수 있습니다. **Stream Aggregate** 연산자를 사용하려면 입력이 그룹 내의 열을 기준으로 정렬되어야 합니다. 최적화 프로그램은 앞서 **Sort** 연산자 또는 정렬된 Index Seek나 Index Scan을 통해 데이터를 아직 정렬하지 않은 경우 이 연산자보다 먼저 **Sort** 연산자를 사용합니다. SHOWPLAN_ALL 문 또는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 그래픽 실행 계획에서는 GROUP BY 조건자에 있는 열이 **Argument** 열에 나열되고 집계 식이 **Defined Values** 열에 나열됩니다. **Stream Aggregate** 는 물리 연산자입니다.| 
|![Switch 연산자 아이콘](../relational-databases/media/switch-32x.gif "Switch operator icon")|**스위치**|**Switch** 는 *n* 개의 입력을 갖는 특수한 유형의 연결 반복기입니다. 각 **Switch** 연산자에 식이 연결되어 있습니다. 식의 반환 값(0과 *n*-1 사이)에 따라 **Switch** 는 적절한 입력 스트림을 출력 스트림으로 복사합니다. **Switch** 의 용도 중 하나는 **TOP** 연산자 같은 특정 연산자와 빠른 전진 커서가 관련된 쿼리 계획을 구현하는 것입니다. **Switch** 는 논리 연산자이면서 물리 연산자입니다.| 
|![Table delete 연산자 아이콘](../relational-databases/media/table-delete-32x.gif "Table delete operator icon")|**Table Delete**|**Table Delete** 물리 연산자는 **Argument** 열에 지정된 테이블에서 행을 삭제합니다.| 
|![Table insert 연산자 아이콘](../relational-databases/media/table-insert-32x.gif "Table insert operator icon")|**Table Insert**|**Table Insert** 연산자는 입력의 행을 쿼리 실행 계획의 **Argument** 열에 지정된 테이블에 삽입합니다. **Argument** 열에는 각 열의 설정 값을 나타내는 SET:() 조건자도 포함됩니다. **Table Insert** 에 삽입 값에 대한 자식이 없는 경우 삽입된 행을 Insert 연산자 자체에서 가져옵니다. **Table Insert** 는 물리 연산자입니다.| 
|![Table merge 연산자](../relational-databases/media/table-merge-32x.gif "Table merge operator")|**Table Merge**|**Table Merge** 연산자는 병합 데이터 스트림을 힙에 적용합니다. 이 연산자는 연산자의 **Argument** 열에서 지정한 테이블의 행을 삭제, 업데이트 또는 삽입합니다. 연산자의 **Argument** 열에서 지정한 **ACTION** 열의 런타임 값에 따라 실제 작업이 수행됩니다. **Table Merge** 는 물리 연산자입니다.| 
|![Table scan 연산자 아이콘](../relational-databases/media/table-scan-32x.gif "Table scan operator icon")|**Table Scan**|**Table Scan** 연산자는 쿼리 실행 계획의 **Argument** 열에 지정된 테이블의 모든 행을 검색합니다. WHERE:() 조건자가 **Argument** 열에 나타나면 조건자에 부합되는 행만 반환됩니다. **Table Scan** 은 논리 및 물리 연산자입니다.| 
|![Table spool 연산자 아이콘](../relational-databases/media/table-spool-32x.gif "Table spool operator icon")|**Table Spool**|**Table Spool** 연산자는 입력을 검색하고 각 행의 복사본을 숨겨진 스풀 테이블에 배치합니다. 이 스풀 테이블은 [tempdb](../relational-databases/databases/tempdb-database.md) 데이터베이스에 저장되어 쿼리 사용 기간 중에만 존재합니다. 예를 들어 **Nested Loops** 연산자로 연산자를 다시 돌리지만 다시 바인딩할 필요가 없을 경우 입력 사항을 다시 검색하는 대신 스풀된 데이터를 사용합니다. **Table Spool** 은 물리 연산자입니다.| 
|![Table spool 연산자 아이콘](../relational-databases/media/table-spool-32x.gif "Table spool operator icon")|**Window Spool**|**Window Spool** 연산자는 각 행을 행과 관련된 창을 나타내는 행 집합으로 확장합니다. 쿼리에서 OVER 절은 쿼리 결과 집합과 창 함수를 포함하는 창을 정의한 다음 창의 각 행에 대한 값을 계산합니다. **Window Spool** 은 논리 및 물리 연산자입니다.| 
|![Table update 연산자 아이콘](../relational-databases/media/table-update-32x.gif "Table update operator icon")|**Table Update**|**Table Update** 물리 연산자는 쿼리 실행 계획의 **Argument** 열에 지정된 테이블의 입력 행을 업데이트합니다. SET:() 조건자는 각 업데이트된 열의 값을 결정합니다. 이러한 값은 SET 절 또는 이 연산자의 다른 곳과 이 쿼리 내의 다른 곳에서 참조될 수 있습니다.| 
|![Table-valued function 연산자 아이콘](../relational-databases/media/table-valued-function-32x.gif "Table-valued function operator icon")|**Table-valued Function**|**Table-valued Function** 연산자는 테이블 반환 함수( [!INCLUDE[tsql](../includes/tsql-md.md)] 또는 CLR)를 계산하고 결과 행을 [tempdb](../relational-databases/databases/tempdb-database.md) 데이터베이스에 저장합니다. 부모 반복자에서 행을 요청하면 **테이블 반환 함수** 는 **tempdb**에서 해당 행을 반환합니다.<br /><br /> 테이블 반환 함수를 호출하는 쿼리는 **테이블 반환 함수** 반복자로 쿼리 계획을 생성합니다. 다양한 매개 변수 값으로**테이블 반환 함수** 를 계산할 수 있습니다.<br /><br /> -<br /> **테이블 반환 함수 XML 판독기** 는 매개 변수로 XML BLOB을 입력하여 XML 문서순으로 정렬된 XML 노드를 나타내는 행 집합을 생성합니다. 다른 입력 매개 변수를 사용하여 XML 문서의 일부만 반환하도록 XML 노드를 제한할 수도 있습니다.<br /><br /> -**XPath 필터가 포함된 테이블 반환 함수 XML 판독기** 는 XPath 식을 만족하는 XML 노드로 출력을 제한하는 특수한 유형의 **XML 판독기 테이블 반환 함수** 입니다.<br /><br /> **테이블 반환 함수** 는 논리/물리 연산자입니다.| 
|없음|**Top N Sort**|**Top N Sort** 는 전체 결과 집합이 아니라 첫 번째 **N** 행만 필요하다는 점을 제외하면 *Sort* 반복자와 비슷합니다. *N*의 값이 작으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 실행 엔진이 메모리에서 전체 정렬 작업을 수행하려 하고 *N*의 값이 크면 *N* 을 매개 변수로 사용하지 않는 일반적인 정렬 방법으로 다시 정렬합니다.| 
|![Top 연산자 아이콘](../relational-databases/media/top-32x.gif "Top operator icon")|**Top**|**Top** 연산자는 입력을 검색하고 정렬 순서 등을 기준으로 행의 지정된 첫째 번호나 백분율만 반환합니다. **Argument** 열에는 타이를 검사할 열 목록이 포함될 수 있습니다. 업데이트 계획에서는 행 개수 제한을 보장하기 위해 **Top** 연산자를 사용합니다. **Top** 은 논리 및 물리 연산자입니다.| 
|![Extended 연산자(UDX) 아이콘](../relational-databases/media/udx-32x.gif "Extended operator (UDX) icon")|**UDX**|확장 연산자(UDX)는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 여러 XQuery 및 XPath 연산 중 하나를 구현합니다. 모든 UDX 연산자는 논리/물리 연산자입니다.<br /><br /> 확장 연산자(UDX) **FOR XML** 은 XML 표현으로 입력되는 관계형 행 집합을 하나의 BLOB 열에 직렬화하여 한 행으로 출력합니다. 이 연산자는 입력 순서에 따라 결과가 달라지는 XML 집계 연산자입니다.<br /><br /> 확장 연산자(UDX) **XML SERIALIZER** 는 입력 순서에 따라 결과가 달라지는 XML 집계 연산자입니다. 이 연산자는 XML 문서 순서대로 입력된 XML 노드 또는 XQuery 스칼라 행을 하나의 XML BLOB 열로 직렬화하여 한 XML 행으로 출력합니다.<br /><br /> 확장 연산자(UDX) **XML FRAGMENT SERIALIZER** 는 XQuery 삽입 데이터 수정 확장에 삽입되는 XML 조각 입력 행을 처리하는 데 사용되는 특별한 유형의 **XML SERIALIZER** 입니다.<br /><br /> 확장 연산자(UDX) **XQUERY STRING** 은 XML 노드로 입력된 입력 행의 XQuery 문자열 값을 계산합니다. 이 연산자는 입력 순서에 따라 결과가 달라지는 문자열 집계 연산자입니다. 입력된 문자열 값을 포함하는 XQuery 스칼라를 한 행으로 출력합니다.<br /><br /> 확장 연산자(UDX) **XQUERY LIST DECOMPOSER** 는 XQuery 목록 분해 연산자입니다. 이 연산자는 XML 노드를 입력받아 각 행의 입력이 XSD 목록 유형인 경우 목록 요소 값을 포함하는 XQuery 스칼라를 각각 하나 이상의 행으로 생성합니다.<br /><br /> 확장 연산자(UDX) **XQUERY DATA** 는 XML 노드를 입력받아 입력 값에 대한 XQuery fn:data() 함수를 계산합니다. 이 연산자는 입력 순서에 따라 결과가 달라지는 문자열 집계 연산자입니다. **fn:data()** 의 결과를 포함하는 XQuery 스칼라를 열로 구성한 하나의 행을 출력합니다.<br /><br /> 확장 연산자(UDX) **XQUERY CONTAINS** 는 XML 노드를 입력받아 입력 값에 대한 XQuery fn:contains() 함수를 계산합니다. 이 연산자는 입력 순서에 따라 결과가 달라지는 문자열 집계 연산자입니다. **fn:contains()** 의 결과를 포함하는 XQuery 스칼라를 열로 구성한 하나의 행을 출력합니다.<br /><br /> 확장 연산자 **UPDATE XML NODE** 는 XML 유형에 대한 **modify()** 메서드로 XQuery 대체 데이터 수정 확장의 XML 노드를 업데이트합니다.| 
|없음|**Union**|**Union** 논리 연산자는 여러 개의 입력을 검색하여 검색된 각 행을 출력하고 중복 요소는 제거합니다. **Union** 은 논리 연산자입니다.| 
|![Update(데이터베이스 엔진) 연산자 아이콘](../relational-databases/media/update-32x.gif "Update (Database Engine) operator icon")|**Update**|**Update** 연산자는 쿼리 실행 계획의 **Argument** 열에 지정된 개체의 입력 내용에 따라 각 행을 업데이트합니다. **Update** 는 논리 연산자입니다. 물리 연산자는 **Table Update**, **Index Update**또는 **Clustered Index Update**입니다.| 
|![While 언어 요소 아이콘](../relational-databases/media/while-32x.gif "While language element icon")|**While**|**While** 연산자는 [!INCLUDE[tsql](../includes/tsql-md.md)] while 루프를 구현합니다. **While** 은 언어 요소입니다.| 
  
