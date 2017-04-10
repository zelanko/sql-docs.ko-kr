---
title: "Columnstore 인덱스 데이터 로드 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b29850b5-5530-498d-8298-c4d4a741cdaf
caps.latest.revision: 31
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 28
---
# Columnstore 인덱스 데이터 로드
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  표준 SQL 대량 로드와 trickle insert 메서드를 사용하여 columnstore 인덱스로 데이터를 로드합니다. 이러한 메서드에는 bcp, Integration Services, Transact-SQL merge 또는 insert 문이 있습니다.  
  
 columnstore 인덱스를 처음 사용하십니까? 용어와 개념은 [Columnstore 인덱스 가이드](../Topic/Columnstore%20Indexes%20Guide.md)를 참조하세요.  
  
 심층적인 논의가 필요하십니까? 이 [블로그 게시물](http://blogs.msdn.com/b/sqlcat/archive/2015/03/11/data-loading-performance-considerations-on-tables-with-clustered-columnstore-index.aspx)을 참조하세요.  
  
##  <a name="dataload_cci"></a> 클러스터형 columnstore 인덱스로 대량 로드  
 클러스터형 columnstore 인덱스로 행을 대량 로드하려면 bcp 명령줄 도구, Integration Services를 사용하거나 준비 테이블에서 행을 선택할 수 있습니다.  
  
 ![클러스터형 columnstore 인덱스로 로드](../../relational-databases/indexes/media/sql-server-pdw-columnstore-loadprocess.gif "클러스터형 columnstore 인덱스로 로드")  
  
 다이어그램에서 알 수 있듯이 대량 로드::  
  
1.  데이터를 미리 정렬하지 않습니다. 수신하는 순서대로 데이터가 행 그룹으로 삽입됩니다.  
  
2.  일괄 처리 크기가 102400 이상인 경우 행은 압축된 행 그룹으로 바로 삽입됩니다. 백그라운드 스레드, 튜플 이동기(TM)에 의해 행이 결과적으로 압축된 행 그룹으로 이동되기 전에 데이터 행을 델타 행 그룹으로 이동하는 것을 방지할 수 있으므로 효율적인 대량 가져오기를 위해 102400 이상의 일괄 처리 크기를 선택하는 것이 좋습니다.  
  
3.  일괄 처리 크기가 102400 미만이거나 남은 행이 102400인 경우 행은 델타 행 그룹으로 로드됩니다.  
  
 클러스터형 columnstore 인덱스로 대량 로드 시 사용 가능한 최적화는 다음과 같습니다.  
  
-   병렬 로드: 별도의 데이터 파일을 로드할 때마다 여러 동시 대량 가져오기(bcp 또는 대량 삽입)를 동시에 수행할 수 있습니다. rowstore와는 달리, 각 대량 가져오기 스레드가 배타적 잠금 상태의 별도 행 그룹(압축 또는 델타 행 그룹)으로 배타적으로 로드되므로 TABLOCK을 지정할 필요가 없습니다.   TABLOCK을 사용하면 테이블에 대한 배타적 잠금이 강제 적용되어 데이터를 병렬로 가져올 수 없게 됩니다.  
  
-   로그 최적화: 데이터가 압축된 행 그룹으로 로드될 때 대량 로드가 둘 다 최소로 기록됩니다. 데이터가 일괄 처리 크기 102400인 델타 행 그룹으로 로드되는 경우 최소 로깅은 없습니다.  
  
-   잠금 최적화: 압축된 행 그룹으로 로드 시 행 그룹에 대한 X 잠금이 획득됩니다. 그러나 델타 행 그룹으로 대량 로드 시 행 그룹에서 X 잠금이 획득되지만 SQL Server는 X 행 그룹 잠금이 잠금 계층 구조의 일부가 아니므로, 잠금 PAGE/EXTENT를 그대로 잠급니다.  
  
 하나 이상의 비클러스터형 인덱스가 있는 경우 인덱스 자체에 대한 잠금 또는 로깅 최적화는 없지만 위의 설명대로 클러스터형 columnstore 인덱스에 대한 최적화는 여전히 남아 있습니다.  
  
## deltastore 작동 방식  
 클러스터형 columnstore 인덱스는 압축 행 그룹으로 압축하기 전에 deltastore에 최대 1,048,576개의 행을 수집합니다. 이를 통해 columnstore 인덱스의 압축이 개선됩니다. deltastore 행 그룹에 1,048,576개의 행이 포함되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 해당 행 그룹을 closed(닫힘)로 표시합니다. *tuple-mover*라는 백그라운드 프로세스가 각 닫힌 행 그룹을 발견하고 columnstore로 압축합니다.  
  
 클러스터형 columnstore 인덱스마다 여러 deltastore가 있을 수 있습니다.  
  
-   deltastore가 잠겨 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다른 deltastore를 잠그려고 합니다. 사용 가능한 deltastore가 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 새 deltastore를 만듭니다.  
  
-   분할된 테이블의 경우 각 파티션에 대해 여러 deltastore가 있을 수 있습니다.  
  
 다음 시나리오에서는 로드된 행이 언제 columnstore로 곧바로 이동하거나 deltastore로 이동하는지를 설명합니다.  
  
 예를 들어, 각 행 그룹에는 행 그룹당 102,400-1,048,576행이 있을 수 있습니다. 실제로 행 그룹의 최대 크기는 메모리 압박이 있는 경우 1,048,576개 행보다 적을 수 있습니다.  
  
|대량 로드할 행|압축된 행 그룹에 추가된 행|델타 행 그룹에 추가된 행|  
|-----------------------|-------------------------------------------|--------------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> 행 그룹 크기: 145,000|0|  
|1,048,577|1,048,576<br /><br /> 행 그룹 크기: 1,048,576|1|  
|2,252,152|2,252,152<br /><br /> 행 그룹 크기: 1,048,576, 1,048,576, 155,000|0|  
  
 다음 예제에서는 1,048,577개 행을 테이블로 로드하는 결과를 보여 줍니다. 결과에는 columnstore에 COMPRESSED 행 그룹이 하나 있고(열 세그먼트로 압축됨) deltastore에 행이 1개 있습니다.  
  
```  
SELECT object_id, index_id, partition_number, row_group_id, delta_store_hobt_id, state state_desc, total_rows, deleted_rows, size_in_bytes   
FROM sys.dm_db_column_store_row_group_physical_stats  
```  
  
 ![Rowgroup and deltastore for a batch load](../../relational-databases/indexes/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup and deltastore for a batch load")  
  
## 준비 테이블에서 로드  
 데이터 로드에 대한 일반적인 패턴은 데이터를 준비 테이블로 로드하고 일부 변형을 수행한 후 다음 명령을 사용하여 대상 테이블로 로드하는 것입니다.  
  
```  
INSERT INTO <columnstore index>  SELECT <list of columns> FROM <Staging Table>  
  
```  
  
 이 명령은 BCP 또는 Bulk Insert와 유사한 방식이지만, 단일 일괄 처리로 columnstore 인덱스에 데이터를 로드합니다. 준비 테이블의 행 수가 102400 미만인 경우 행은 델타 행 그룹으로 로드됩니다. 그렇지 않으면, 행은 압축된 행 그룹으로 바로 로드됩니다.  한 가지 주요 제한 사항은 이 INSERT 작업이 단일 스레드라는 것입니다. 병렬로 데이터를 로드하려면 여러 준비 테이블을 만들거나 준비 테이블에서 행의 범위가 겹치지 않는 INSERT/SELECT를 실행할 수 있습니다.  이 제한 사항은 SQL Server 2016에서 사라집니다. 아래 명령은 준비 테이블에서 데이터를 병렬로 로드하지만 TABLOCK을 지정해야 합니다.  
  
```  
INSERT INTO <columnstore index>  WITH (TABLOCK)  SELECT <list of columns> FROM <Staging Table>  
```  
  
 준비 테이블에서 클러스터형 columnstore 인덱스로 대량 로드 시 사용 가능한 최적화는 다음과 같습니다.  
  
-   로그 최적화: 데이터가 압축된 행 그룹으로 로드될 때 둘 다 최소로 기록됩니다. 데이터가 델타 행 그룹으로 로드되는 경우 최소 로깅은 없습니다.  
  
-   잠금 최적화: 압축된 행 그룹으로 로드 시 행 그룹에 대한 X 잠금이 획득됩니다. 그러나 델타 행 그룹을 통해 X 잠금이 행 그룹에서 획득되지만 SQL Server는 X 행 그룹 잠금이 잠금 계층 구조의 일부가 아니므로, 잠금 PAGE/EXTENT를 그대로 잠급니다.  
  
 하나 이상의 비클러스터형 인덱스가 있는 경우 인덱스 자체에 대한 잠금 또는 로깅 최적화는 없지만 위의 설명대로 클러스터형 columnstore 인덱스에 대한 최적화는 여전히 남아 있습니다.  
  
## Trickle insert를 사용하여 로드  
 *Trickle insert* 는 INSERT INTO를 사용하여 행이 columnstore로 로드되는 방식을 나타냅니다. 각 행은 델타 행 그룹에 추가됩니다. trickle되는 행은 1,048,576개 행에 도달한 후 행 그룹이 닫히거나 columnstore 인덱스가 다시 작성될 때까지 이들이 축적되는 deltastore 행 그룹으로 바로 이동됩니다.  
  
```  
INSERT INTO <table-name> VALUES (<set of values>)  
```  
  
 단, 클러스터형 columnstore 인덱스로 값을 삽입하기 위해 INSERT INTO를 사용하는 동시 스레드는 행을 동일한 deltastore 행 그룹에 삽입할 수 있습니다.  
  
 행 그룹에 1,048,576개 행이 포함되면 델타 행 그룹은 closed(닫힘)로 표시해도 쿼리와 업데이트/삭제 작업은 할 수 있지만 새로 삽입된 행은 기존 또는 새롭게 만든 deltastore 행 그룹으로 이동됩니다. 닫힌 델타 행 그룹을 5분 간격으로 압축하는 백그라운드 스레드 *TM(튜플 이동기)*가 있습니다. 닫힌 델타 행 그룹을 압축하기 위해 다음 명령을 명시적으로 호출할 수 있습니다.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE  
```  
  
 델타 행 그룹에 닫힘 및 압축을 강제 적용하려는 경우 다음 명령을 실행할 수 있습니다. 행 로드를 완료하고 새로운 행을 원하지 않을 경우 이 명령을 실행할 수 있습니다. 델타 행 그룹을 명시적으로 닫고 압축하면 저장 공간을 추가로 절약하고 분석 쿼리 성능을 개선할 수 있습니다. 새 행의 삽입을 원하지 않는 경우 이 명령을 호출하는 것이 가장 좋은 방법입니다.  
  
```  
ALTER INDEX <index-name> on <table-name> REORGANIZE with (COMPRESS_ALL_ROW_GROUPS = ON)  
```  
  
## 분할된 테이블에 로드  
 분할된 데이터에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 먼저 각 행을 파티션에 할당한 다음 파티션 내에서 데이터에 columnstore 작업을 수행합니다. 각 파티션에는 고유한 행 그룹 수와 적어도 하나의 deltastore가 있습니다.  
  
## 비클러스터형 columnstore 인덱스에 로드  
 비클러스터형 columnstore 인덱스 데이터가 있는 rowstore 테이블에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 항상 데이터를 기본 테이블에 삽입합니다. 데이터는 columnstore 인덱스에 직접 삽입되지 않습니다.  
  
## 참고 항목  
 [Columnstore 인덱스 가이드](../Topic/Columnstore%20Indexes%20Guide.md)   
 [Columnstore 인덱스 버전형 기능 요약](../Topic/Columnstore%20Indexes%20Versioned%20Feature%20Summary.md)   
 [Columnstore 인덱스 쿼리 성능](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [Get started with Columnstore for real time operational analytics(실시간 운영 분석을 위한 Columnstore 시작)](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [데이터 웨어하우스용 Columnstore 인덱스](../Topic/Columnstore%20Indexes%20for%20Data%20Warehousing.md)   
 [Columnstore 인덱스 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  