---
title: 성능 카운터 (SSAS) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 66e88fcaebab11f547874ba1defacc24c76fe31a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="performance-counters-ssas"></a>성능 카운터(SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  성능 모니터를 사용하면 성능 카운터를 사용하여 Microsoft SQL SSAS(Server Analysis Services) 인스턴스의 성능을 모니터링할 수 있습니다.  
  
 성능 모니터는 리소스 사용을 추적하는 MMC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management  Control)  스냅인입니다. 이 MMC 스냅인은 명령 프롬프트에 **PerfMon** 을 입력하거나 제어판에서 **관리 도구**, **성능 모니터**를 차례로 클릭하여 시작할 수 있습니다. 성능 모니터를 사용하면 미리 정의한 개체 및 카운터를 사용하여 서버와 프로세스 성능 및 작업을 추적하고 사용자 정의 카운터를 사용하여 이벤트를 모니터링할 수 있습니다. 성능 모니터는 이벤트에 대한 데이터(예: 메모리 사용량, 활성 트랜잭션 수 또는 CPU 작업) 대신에 개수를 수집합니다. 특정 카운터에 대해 운영자에게 경고 메시지를 보내도록 임계값을 설정할 수도 있습니다.  
  
 성능 모니터는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 원격 및 로컬 인스턴스를 모니터링할 수 있습니다. 자세한 내용은 [성능 모니터 사용](http://technet.microsoft.com/library/cc749115.aspx)을 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]와 함께 사용할 수 있는 카운터에 대한 설명을 보려면 성능에서 **카운터 추가** 대화 상자를 열고 성능 개체를 선택한 다음 **설명 표시**를 클릭하십시오. 가장 중요한 카운터는 CPU  사용량,  메모리 사용량,  디스크 IO  속도입니다. 이 중요한 카운터부터 사용해 보고 모니터링을 통해 향상될 수 있는 다른 사항에 대해 더 나은 생각이 떠오를 때 보다 세부적인 카운터를 시도하는 것이 좋습니다. 포함할 카운터에 대한 자세한 내용은 [SQL  Server  2008  R2작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오.  
  
 카운터는 관련된 카운터를 더 쉽게 찾을 수 있도록 그룹화되어 있습니다.  
  
## <a name="counters-by-groups"></a>그룹별 카운터  
  
|그룹|Description|  
|-----------|-----------------|  
|[캐시](#bkmk_Cache)|Analysis  Services  집계 캐시와 관련된 통계입니다.|  
|[연결](#bkmk_Connection)|Microsoft  Analysis  Services  연결과 관련된 통계입니다.|  
|[데이터 마이닝 예측](#bkmk_DataMiningPrediction)|데이터 마이닝 모델 처리와 관련된 통계입니다.|  
|[데이터 마이닝 모델 처리](#bkmk_DataMiningModelProcessing)|데이터 마이닝 모델에서 예측을 만드는 것과 관련된 통계입니다.|  
|[잠금](#bkmk_Locks)|Microsoft  Analysis  Services  내부 서버 잠금과 관련된 통계입니다.|  
|[MDX](#bkmk_MDX)|Microsoft  Analysis  Services  MDX  계산과 관련된 통계입니다.|  
|[메모리](#bkmk_Memory)|Microsoft  Analysis  Services  내부 서버 메모리와 관련된 통계입니다.|  
|[자동 관리 캐싱](#bkmk_ProactiveCaching)|Microsoft  Analysis  Services  자동 관리 캐싱과 관련된 통계입니다.|  
|[집계 처리](#bkmk_ProcAggregations)|MOLAP  데이터 파일의 집계 처리와 관련된 통계입니다.|  
|[인덱스 처리](#bkmk_ProcIndexes)|MOLAP  데이터 파일의 인덱스 처리와 관련된 통계입니다.|  
|[처리](#bkmk_Processing)|데이터 처리와 관련된 통계입니다.|  
|[저장소 엔진 쿼리](#bkmk_StorageEngineQuery)|Microsoft  Analysis  Services  저장소 엔진 쿼리와 관련된 통계입니다.|  
|[스레드](#bkmk_Threads)|Microsoft  Analysis  Services  스레드와 관련된 통계입니다.|  
  
###  <a name="bkmk_Cache"></a> 캐시  
 Microsoft  Analysis  Services  집계 캐시와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Current  KB|집계 캐시에서 사용하는 현재 메모리(KB)입니다.|  
|KB  added/sec|캐시에 추가된 메모리 속도(KB/초)입니다.|  
|Current entries|현재 캐시 항목 수입니다.|  
|Inserts/sec|캐시에 대한 삽입 비율입니다.  이 비율은 파티션,  큐브,  데이터베이스별로 추적됩니다.|  
|Evictions/sec|캐시에 대한 제거 비율입니다.  파티션,  큐브,  데이터베이스별로 표시됩니다.  제거는 주로 백그라운드에서 수행되는 클리너 프로세스에 의해 발생합니다.|  
|Total  inserts|캐시에 대한 삽입 수입니다.  이 비율은 파티션,  큐브,  데이터베이스별로 추적됩니다.|  
|Total  evictions|캐시에 대한 제거 수입니다.  제거는 파티션,  큐브,  데이터베이스별로 추적됩니다.  제거는 주로 백그라운드에서 수행되는 클리너 프로세스에 의해 발생합니다.|  
|Direct hits/sec|캐시 직접 적중 비율입니다. 캐시 적중은 기존의 캐시 항목이 쿼리에 응답했음을 나타냅니다.|  
|Misses/sec|캐시 누락 비율입니다.|  
|Lookups/sec|캐시 조회 비율입니다.|  
|Total  direct  hits|직접 캐시 적중의 총 개수입니다.  직접 캐시 적중은 기존의 캐시 항목이 쿼리에 응답했음을 나타냅니다.|  
|Total  misses|총 캐시 누락 수입니다.|  
|Total  lookups|캐시에 대한 총 조회 수입니다.|  
|Direct  hit  ratio|카운터 값 간의 기간에 발생하는 캐시 조회에 대한 캐시 직접 적중 비율입니다.|  
|Total  filtered  iterator  cache  hits|필터링된 결과에서 인덱싱된 반복자를 반환하는 총 캐시 적중 수입니다.|  
|Total  filtered  iterator  cache  misses|필터링된 결과에서 인덱싱된 반복자를 작성할 수 없어서 필터링된 결과로 새 캐시를 작성해야 하는 총 캐시 적중 수입니다.|  
  
###  <a name="bkmk_Connection"></a> 연결  
 Microsoft  Analysis  Services  연결과 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Current  connections|현재 설정된 클라이언트 연결 수입니다.|  
|Requests/sec|도착한 연결 요청  수입니다.|  
|Total  requests|도착한 총 연결 요청  수입니다.|  
|Successes/sec|성공적으로 완료된 연결 비율입니다.|  
|Total  successes|성공한 총 연결 수입니다.|  
|Failures/sec|실패한 연결 비율입니다.|  
|Total  failures|실패한 총 연결 시도 수입니다.|  
|Current  user  sessions|현재 설정된 사용자 세션 수입니다.|  
  
###  <a name="bkmk_DataMiningModelProcessing"></a> 데이터 마이닝 모델 처리  
 Microsoft  Analysis  Services  데이터 마이닝 모델 처리와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Cases/sec|사례가 처리되는 속도입니다.|  
|Current  models  processing|현재 처리 중인 모델 수입니다.|  
  
###  <a name="bkmk_DataMiningPrediction"></a> 데이터 마이닝 예측  
 Microsoft  Analysis  Services  데이터 마이닝 예측과 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Concurrent  DM  queries|현재 수행 중인 데이터 마이닝 쿼리 수입니다.|  
|Predictions/sec|데이터 마이닝 쿼리에서 생성되는 예측 수입니다.|  
|Rows/sec|데이터 마이닝 예측 쿼리 중에 처리되는 행 수입니다.|  
|Queries/sec|처리된 데이터 마이닝 쿼리 수입니다.|  
|Total  Queries|서버에서 받는 총 데이터 마이닝 쿼리 수입니다.|  
|Total  Rows|데이터 마이닝 쿼리에서 반환되는 총 행 수입니다.|  
|Total  Predictions|서버에서 받는 총 데이터 마이닝 예측 쿼리 수입니다.|  
  
###  <a name="bkmk_Locks"></a> 잠금  
 Microsoft  Analysis  Services  내부 서버 잠금과 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Current  latch  waits|현재 래치를 대기하는 스레드 수입니다.  즉시 허가를 받을 수 없어 대기 상태에 놓인 래치 요청이 포함됩니다.|  
|Latch  waits/sec|즉시 허용될 수 없어 허용될 때까지 기다려야 하는 래치 요청 비율입니다.|  
|Current  locks|현재 잠겨 있는 개체 수입니다.|  
|Current  lock  waits|현재 잠금을 대기하는 클라이언트 수입니다.|  
|Lock requests/sec|초당 잠금 요청 수입니다.|  
|Lock  grants/sec|초당 잠금 허용 수입니다.|  
|Lock waits/sec|초당 잠금 대기 수입니다.  즉시 잠금 허가를 받을 수 없어 대기 상태에 놓인 잠금 요청이 포함됩니다.|  
|Lock  denials/sec|잠금 거부 비율입니다.|  
|Unlock requests/sec|초당 잠금 해제 요청 수입니다.|  
|Total  deadlocks  detected|발견된 교착 상태의 총 수입니다.|  
  
###  <a name="bkmk_MDX"></a> MDX  
 Microsoft  Analysis  Services  MDX  계산과 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Number  of  calculation  covers|활성 노드 및 캐시된 노드를 포함하여 MDX  실행 계획으로 작성된 총 계산 노드 수입니다.|  
|현재 계산 노드 수|활성 노드 및 캐시된 노드를 포함하여 MDX  실행 계획으로 작성된 현재 계산 노드 수(근사치)입니다.|  
|Number  of  Storage  Engine  evaluation  nodes|MDX 실행 계획으로 작성된 총 저장소 엔진 계산 노드 수입니다.|  
|Number  of  cell-by-cell  evaluation  nodes|MDX  실행 계획으로 작성된 총 셀별 계산 노드 수입니다.|  
|대량 모드 계산 노드 수|MDX  실행 계획으로 작성된 총 대량 모드 계산 노드 수입니다.|  
|한 셀에만 적용되는 계산 노드 수|한 셀에만 적용되는 MDX  실행 계획으로 작성된 총 계산 노드 수입니다.|  
|Number  of  evaluation  nodes  with  calculations  at  the  same  granularity|계산이 계산 노드와 동일한 세분성에 있는 MDX  실행 계획으로 작성된 총 계산 노드 수입니다.|  
|Current  number  of  cached  evaluation  nodes|MDX 실행 계획으로 작성된 현재 캐시된 계산 노드 수(근사치)입니다.|  
|Number  of  cached  Storage  Engine  evaluation  nodes|MDX 실행 계획으로 작성된 총 캐시된 저장소 엔진 계산 노드 수입니다.|  
|캐시된 대량 모드 계산 노드 수|MDX  실행 계획으로 작성된 총 캐시된 대량 모드 계산 노드 수입니다.|  
|Number  of  cached  'other'  evaluation  nodes|저장소 엔진 또는 대량 모드가 아닌 MDX 실행 계획으로 작성된 총 캐시된 계산 노드 수입니다.|  
|Number  of  evictions  of  evaluation  nodes|충돌로 인한 계산 노드의 총 캐시 제거 수입니다.|  
|Number  of  hash  index  hits  in  the  cache  of  evaluation  nodes|해시 인덱스에 의해 충족되는 계산 노드 캐시의 총 적중 수입니다.|  
|Number  of  cell-by-cell  hits  in  the  cache  of  evaluation  nodes|계산 노드 캐시의 총 셀별 적중 수입니다.|  
|계산 노드 캐시의 셀별 누락 수|계산 노드 캐시의 총 셀별 누락 수입니다.|  
|산 노드 캐시의 하위 큐브 적중 수|계산 노드 캐시의 총 하위 큐브 적중 수입니다.|  
|Number  of  subcube  misses  in  the  cache  of  evaluation  nodes|계산 노드 캐시의 총 하위 큐브 누락 수입니다.|  
|Total  Sonar  subcubes|쿼리 최적화 프로그램에서 생성한 총 하위 큐브 수입니다.|  
|Total  cells  calculated|계산된 총 셀 속성 수입니다.|  
|Total  recomputes|오류로 인해 다시 계산된 총 셀 수입니다.|  
|Total  flat  cache  inserts|플랫 계산 캐시로 삽입된 총 셀 값 수입니다.|  
|Total  calculation  cache  registered|등록된 총 계산 캐시 수입니다.|  
|Total  NON  EMPTY|NON  EMPTY  알고리즘이 사용된 총 횟수입니다.|  
|Total  NON  EMPTY  unoptimized|최적화되지 않은 NON  EMPTY  알고리즘이 사용된 총 횟수입니다.|  
|Total  NON  EMPTY  for  calculated  members|계산 멤버에 NON  EMPTY  알고리즘을 루핑한 총 횟수입니다.|  
|Total  Autoexist|AUTOEXIST를 수행한 총 횟수입니다.|  
|Total  EXISTING|EXISTING  집합 연산을 수행한 총 횟수입니다.|  
  
###  <a name="bkmk_Memory"></a> 메모리  
 Microsoft  Analysis  Services  내부 서버 메모리와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Page  Pool  64  Alloc  KB|시스템에서 빌려 온 메모리(KB)입니다.  이 메모리는 서버의 다른 부분에 제공됩니다.|  
|Page  Pool  64  Lookaside  KB|64KB  할당 준비 목록에 있는 현재 메모리(KB)입니다.  메모리 페이지를 사용할 준비가 되었습니다.|  
|Page  Pool  8  Alloc  KB|64KB  페이지 풀에서 빌려 온 메모리(KB)입니다.  이 메모리는 서버의 다른 부분에 제공됩니다.|  
|Page Pool 8 Lookaside KB|8KB 할당 준비 목록에 있는 현재 메모리(KB)입니다.  메모리 페이지를 사용할 준비가 되었습니다.|  
|Page Pool 1 Alloc KB|64KB  페이지 풀에서 빌려 온 메모리(KB)입니다.  이 메모리는 서버의 다른 부분에 제공됩니다.|  
|Page Pool 1 Lookaside KB|8KB 할당 준비 목록에 있는 현재 메모리(KB)입니다.  메모리 페이지를 사용할 준비가 되었습니다.|  
|Cleaner  Current  Price|1000  단위로 규정된 메모리의 현재 가격($/바이트/시간)입니다.|  
|Cleaner Balance/sec|밸런스 및 축소 작업의 비율입니다.|  
|Cleaner Memory shrunk KB/sec|축소 속도(KB/초)입니다.|  
|Cleaner Memory shrinkable KB|백그라운드에서 수행되는 클리너에 의한 제거에 영향을 받는 메모리 용량(KB)입니다.|  
|Cleaner  Memory  nonshrinkable  KB|백그라운드에서 수행되는 클리너에 의한 제거에 영향을 받지 않는 메모리 용량(KB)입니다.|  
|Cleaner  Memory  KB|백그라운드에서 수행되는 클리너에 인식된 메모리 용량(KB)입니다.  (클리너 메모리 축소 가능 +  클리너 메모리 축소 불가능.)|  
|Memory  Usage  KB|더욱 명확한 메모리 비용 계산에 사용되는 서버 프로세스의 메모리 사용량입니다.  Process\PrivateBytes  카운터와 메모리가 매핑된 데이터의 크기를 더한 값과 동일하며,  xVelocity  엔진 Memory  Limit를 초과하여 xVelocity  메모리 내 분석 엔진(VertiPaq)에 의해 매핑되었거나 할당된 메모리는 무시합니다.|  
|Memory  Limit  Low  KB|구성 파일의 하한 메모리 제한입니다.|  
|Memory  Limit  High  KB|구성 파일의 상한 메모리 제한입니다.|  
|AggCacheKB|집계 캐시에 할당된 현재 메모리(KB)입니다.|  
|Quota  KB|현재 메모리 할당량(KB)입니다.  메모리 할당량은 메모리 부여 또는 메모리 예약이라고도 합니다.|  
|Quota  Blocked|다른 메모리 할당량이 해제될 때까지 차단되는 현재 할당량 요청 수입니다.|  
|Filestore KB|파일 저장소(파일 캐시)에 할당된 현재 메모리(KB)입니다.|  
|Filestore  Page  Faults/sec|파일 저장소 페이지 폴트 비율입니다.|  
|Filestore  Reads/sec|초당 파일 저장소 페이지 읽기 수입니다.|  
|Filestore  KB  Reads/sec|초당 파일 저장소 KB 읽기 수입니다.|  
|Filestore  Writes/sec|초당 파일 저장소 페이지 쓰기 수입니다.  쓰기는 비동기 작업입니다.|  
|Filestore KB Write/sec|초당 파일 저장소 KB 쓰기 수입니다.  쓰기는 비동기 작업입니다.|  
|Filestore IO Errors/sec|파일 저장소 IO  오류 비율입니다.|  
|Filestore  IO  Errors|총 파일 저장소 IO 오류 수입니다.|  
|Filestore  Clock  Pages  Examined/sec|제거 고려 사항에 대한 백그라운드에서 수행되는 클리너 검사 페이지 비율입니다.|  
|Filestore  Clock  Pages  HaveRef/sec|백그라운드에서 수행되는 클리너 검사 페이지 비율에 사용하고 있는 현재 참조 수가 있습니다.|  
|Filestore Clock Pages Valid/sec|유효한 제거 후보 페이지를 백그라운드에서 수행되는 클리너가 검사하는 속도입니다.|  
|Filestore  Memory  Pinned  KB|현재 고정된 파일 저장소 메모리(KB)입니다.|  
|In-memory Dimension Property File KB|현재 메모리 내 차원 속성 파일의 크기(KB)입니다.|  
|In-memory Dimension Property File KB/sec|메모리 내 차원 속성 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential  In-memory  Dimension  Property  File  KB|현재 메모리 내 차원 속성 파일의 잠재적 크기(KB)입니다.|  
|Dimension Property Files|차원 속성 파일 수입니다.|  
|In-memory  Dimension  Index  (Hash)  File  KB|현재 메모리 내 차원 인덱스(해시) 파일의 크기(KB)입니다.|  
|In-memory Dimension Index (Hash) File KB/sec|메모리 내 차원 인덱스(해시)  파일에 대한 쓰기 비율(KB)입니다.|  
|Potential In-memory Dimension Index (Hash) File KB|메모리 내 차원 인덱스(해시)  파일의 잠재적 크기(KB)입니다.|  
|Dimension Index (Hash) Files|차원 인덱스(해시)  파일 수입니다.|  
|In-memory Dimension String File KB|현재 메모리 내 차원 문자열 파일의 크기(KB)입니다.|  
|In-memory  Dimension  String  File  KB/sec|메모리 내 차원 문자열 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential  In-memory  Dimension  String  File  KB|메모리 내 차원 문자열 파일의 잠재적 크기(KB)입니다.|  
|Dimension  String  Files|차원 문자열 파일 수입니다.|  
|In-memory Map File KB|현재 메모리 내 맵 파일의 크기(KB)입니다.|  
|In-memory Map File KB/sec|메모리 내 맵 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential  In-memory  Map  File  KB|메모리 내 맵 파일의 잠재적 크기(KB)입니다.|  
|Map  Files|맵 파일 수입니다.|  
|In-memory  Aggregation  Map  File  KB|현재 메모리 내 집계 맵 파일의 크기(KB)입니다.|  
|In-memory  Aggregation  Map  File  KB/sec|메모리 내 집계 맵 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential In-memory Aggregation Map File KB|메모리 내 집계 맵 파일의 잠재적 크기(KB)입니다.|  
|Aggregation  Map  Files|집계 맵 파일 수입니다.|  
|In-memory Fact Data File KB|현재 메모리 내 팩트 데이터 파일의 크기(KB)입니다.|  
|In-memory  Fact  Data  File  KB/sec|메모리 내 팩트 데이터 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential  In-memory  Fact  Data  File  KB|메모리 내 팩트 데이터 파일의 잠재적 크기(KB)입니다.|  
|Fact  Data  Files|팩트 데이터 파일 수입니다.|  
|In-memory  Fact  String  File  KB|현재 메모리 내 팩트 문자열 파일의 크기(KB)입니다.|  
|In-memory  Fact  String  File  KB/sec|메모리 내 팩트 문자열 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential  In-memory  Fact  String  File  KB|메모리 내 팩트 문자열 파일의 잠재적 크기(KB)입니다.|  
|Fact String Files|팩트 문자열 파일 수입니다.|  
|In-memory  Fact  Aggregation  File  KB|현재 메모리 내 팩트 집계 파일의 크기(KB)입니다.|  
|In-memory Fact Aggregation File KB/sec|메모리 내 팩트 집계 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential  In-memory  Fact  Aggregation  File  KB|메모리 내 팩트 집계 파일의 잠재적 크기(KB)입니다.|  
|Fact Aggregation Files|팩트 집계 파일 수입니다.|  
|In-memory  Other  File  KB|현재 메모리 내 기타 파일의 크기(KB)입니다.|  
|In-memory Other File KB/sec|메모리 내 기타 파일에 대한 쓰기 비율(KB)입니다.|  
|Potential In-memory Other File KB|메모리 내 기타 파일의 잠재적 크기(KB)입니다.|  
|Other Files|기타 파일 수입니다.|  
|VertiPaq Paged KB|메모리 내 데이터에 대해 사용 중인 페이징된 메모리(KB)입니다.|  
|VertiPaq Nonpaged KB|메모리 내 엔진에서 사용하기 위한 작업 집합에 잠긴 메모리(KB)입니다.|  
|VertiPaq Memory-Mapped KB|메모리 내 데이터에 대해 사용 중인 페이징 가능한 메모리(KB)입니다.|  
|Memory Limit Hard KB|구성 파일의 하드 메모리 제한입니다.|  
|Memory Limit VertiPaq KB|구성 파일의 메모리 내 제한입니다.|  
  
###  <a name="bkmk_ProactiveCaching"></a> 자동 관리 캐싱  
 Microsoft  Analysis  Services  자동 관리 캐싱과 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Notifications/sec|관계형 데이터베이스의 알림 비율입니다.|  
|Processing Cancellations/sec|알림에 의해 처리가 취소된 비율입니다.|  
|Proactive Caching Begin/sec|자동 관리 캐싱 시작 비율입니다.|  
|Proactive Caching Completion/sec|자동 관리 캐싱 완료 비율입니다.|  
  
###  <a name="bkmk_ProcAggregations"></a> 집계 처리  
 MOLAP  데이터 파일의 Microsoft  Analysis  Services  집계 처리와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Current  partitions|현재 처리 중인 파티션 수입니다.|  
|Total  partitions|성공 여부에 관계없이 처리된 파티션의 총 수입니다.|  
|Memory  size  rows|메모리에 있는 현재 집계의  예상 크기입니다.|  
|Memory  size  bytes|메모리에 있는 현재 집계의  예상 크기입니다.|  
|Rows  merged/sec|집계로 병합 또는 삽입된 행의 비율입니다.|  
|Rows created/sec|생성된 집계 행의 비율입니다.|  
|Temp  file  rows  written/sec|임시 파일에 쓰는 행의 비율입니다.  이 작업은 집계가 메모리 한계를 초과할 때 발생합니다.|  
|Temp  file  bytes  written/sec|임시 파일에 쓰는 바이트의 비율입니다.  이 작업은 집계가 메모리 한계를 초과할 때 발생합니다.|  
  
###  <a name="bkmk_ProcIndexes"></a> 인덱스 처리  
 MOLAP  데이터 파일의 Microsoft  Analysis  Services  인덱스 처리와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Current  partitions|현재 처리 중인 파티션 수입니다.|  
|Total  partitions|성공 여부에 관계없이 처리된 파티션의 총 수입니다.|  
|Rows/sec|인덱스를 만드는 데 사용한 MOLAP  파일의 행 비율입니다.|  
|Total  Rows|인덱스를 만드는 데 사용한 MOLAP  파일의 총 행 수입니다.|  
  
###  <a name="bkmk_Processing"></a> 처리  
 Microsoft  Analysis  Services  데이터 처리와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Rows read/sec|모든 관계형 데이터베이스에서 읽은 행의 비율입니다.|  
|Total  rows  read|모든 관계형 데이터베이스에서 읽은 행 수입니다.|  
|Rows  converted/sec|처리하는 동안 변환된 행의 비율입니다.|  
|Total  rows  converted|처리하는 동안 변환된 행 수입니다.|  
|Rows  written/sec|처리하는 동안 쓴 행의 비율입니다.|  
|Total  rows  written|처리하는 동안 쓴 행 수입니다.|  
  
###  <a name="bkmk_StorageEngineQuery"></a> 저장소 엔진 쿼리  
 Microsoft  Analysis  Services  저장소 엔진 쿼리와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Current  measure  group  queries|현재 수행 중인 측정값 그룹 쿼리 수입니다.|  
|Measure group queries/sec|측정값 그룹 쿼리의 비율입니다.|  
|Total  measure  group  queries|측정값 그룹에 대한 총 쿼리 수입니다.|  
|Current  dimension  queries|현재 수행 중인 차원 쿼리 수입니다.|  
|Dimension  queries/sec|차원 쿼리 비율입니다.|  
|Total  dimension  queries|총 차원 쿼리 수입니다.|  
|Queries answered/sec|응답한 쿼리의 비율입니다.|  
|Total  queries  answered|응답한 쿼리의 총 수입니다.|  
|Bytes sent/sec|서버가 쿼리에 대한 응답으로 클라이언트에 보낸 바이트 비율입니다.|  
|Total  bytes  sent|서버가 쿼리에 대한 응답으로 클라이언트에 보낸 총 바이트 수입니다.|  
|Rows  sent/sec|서버가 클라이언트로 보낸 행 비율입니다.|  
|Total  rows  sent|서버가 클라이언트로 보낸 총 행 수입니다.|  
|Queries  from  cache  direct/sec|캐시에서 직접 응답한 쿼리 비율입니다.|  
|Queries from cache filtered/sec|기존 캐시 항목을 필터링하여 응답한 쿼리 비율입니다.|  
|Queries from file/sec|파일에서 응답한 쿼리 비율입니다.|  
|Total  queries  from  cache  direct|캐시에서 직접 가져온 파티션별  총 쿼리 수입니다.|  
|Total  queries  from  cache  filtered|기존 캐시 항목을 필터링하여 응답한 총 쿼리 수입니다.|  
|Total  queries  from  file|파일에서 응답한 총 쿼리 수입니다.|  
|Map  reads/sec|맵 파일을 사용한 논리적 읽기 작업 수입니다.|  
|Map  bytes/sec|맵 파일에서 읽은 바이트 수입니다.|  
|Data  reads/sec|데이터 파일을 사용한 논리적 읽기 작업 수입니다.|  
|Data bytes/sec|데이터 파일에서 읽은 바이트 수입니다.|  
|Avg time/query|쿼리당 평균 시간(밀리초)입니다.  마지막으로 카운터를 측정한 후 처리된 쿼리를 기초로 계산한 응답 시간입니다.|  
|Network round trips/sec|네트워크 왕복 비율입니다.  여기에는 모든 클라이언트/서버 통신이 포함됩니다.|  
|Total network round trips|총 네트워크 왕복 수입니다.  여기에는 모든 클라이언트/서버 통신이 포함됩니다.|  
|Flat cache lookups/sec|플랫 캐시 조회 비율입니다.  여기에는 전역,  세션 및 쿼리 범위 플랫 캐시가 포함됩니다.|  
|Flat  cache  hits/sec|플랫 캐시 적중 비율입니다.  여기에는 전역,  세션 및 쿼리 범위 플랫 캐시가 포함됩니다.|  
|Calculation  cache  lookups/sec|계산 캐시 조회 비율입니다.  여기에는 전역,  세션 및 쿼리 범위 계산 캐시가 포함됩니다.|  
|Calculation  cache  hits/sec|계산 캐시 적중 비율입니다.  여기에는 전역,  세션 및 쿼리 범위 계산 캐시가 포함됩니다.|  
|Persisted cache lookups/sec|지속형 캐시 조회 비율입니다.  지속형 캐시는 MDX  스크립트 CACHE  문으로 만들어집니다.|  
|Persisted cache hits/sec|지속형 캐시 적중 비율입니다.  지속형 캐시는 MDX  스크립트 CACHE  문으로 만들어집니다.|  
|Dimension cache lookups/sec|차원 캐시 조회 비율입니다.|  
|Dimension cache hits/sec|차원 캐시 적중 비율입니다.|  
|Measure  group  cache  lookups/sec|측정값 그룹 캐시 조회 비율입니다.|  
|Measure group cache hits/sec|측정값 그룹 캐시 적중 비율입니다.|  
|Aggregation  lookups/sec|집계 조회 비율입니다.|  
|Aggregation  hits/sec|집계 적중 비율입니다.|  
  
###  <a name="bkmk_Threads"></a> 스레드  
 Microsoft  Analysis  Services  스레드와 관련된 통계입니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|Short  parsing  idle  threads|짧은 구문 분석 스레드 풀의 유휴 상태 스레드 수입니다.|  
|Short  parsing  busy  threads|짧은 구문 분석 스레드 풀의 사용 중인 스레드 수입니다.|  
|Short  parsing  job  queue  length|짧은 구문 분석 스레드 풀의 큐에 있는 작업 수입니다.|  
|Short  parsing  job  rate|짧은 구문 분석 스레드 풀을 통한 작업 비율입니다.|  
|Long  parsing  idle  threads|긴 구문 분석 스레드 풀의 유휴 상태 스레드 수입니다.|  
|Long  parsing  busy  threads|긴 구문 분석 스레드 풀의 사용 중인 스레드 수입니다.|  
|Long  parsing  job  queue  length|긴 구문 분석 스레드 풀의 큐에 있는 작업 수입니다.|  
|Long  parsing  job  rate|긴 구문 분석 스레드 풀을 통한 작업 비율입니다.|  
|Query  pool  idle  threads|쿼리 스레드 풀의 유휴 상태 스레드 수입니다.|  
|Query  pool  busy  threads|쿼리 스레드 풀의 사용 중인 스레드 수입니다.|  
|Query  pool  job  queue  length|쿼리 스레드 풀의 큐에 있는 작업 수입니다.|  
|Query  pool  job  rate|쿼리 스레드 풀을 통한 작업 비율입니다.|  
|Processing pool idle non-I/O threads|비-I/O  작업에만 사용되는 처리 스레드 풀의 유휴 상태 스레드 수입니다.|  
|Processing pool busy non-I/O threads|처리 스레드 풀에서 비-I/O  작업을 실행 중인 스레드 수입니다.|  
|Processing pool job queue length|처리 스레드 풀의 큐에 있는 비-I/O  작업 수입니다.|  
|Processing  pool  job  rate|처리 스레드 풀을 통한 비-I/O  작업 비율입니다.|  
|Processing  pool  idle  I/O  job  threads|처리 스레드 풀에서 I/O 작업에 사용되는 유휴 상태 스레드 수입니다.|  
|Processing  pool  busy  I/O  job  threads|처리 스레드 풀에서 I/O 작업을 실행 중인 스레드 수입니다.|  
|Processing  pool  I/O  job  queue  length|처리 스레드 풀의 큐에 있는 I/O  작업 수입니다.|  
|Processing  pool  I/O  job  completion  rate|처리 스레드 풀을 통한 I/O 작업 비율입니다.|  
  
  
