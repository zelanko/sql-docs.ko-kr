---
title: 클러스터형된 Columnstore 인덱스를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e65c3e277eb9a3e5e3703525b9c1ac06b423c96
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773743"
---
# <a name="using-clustered-columnstore-indexes"></a>클러스터형 columnstore 인덱스 사용
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 클러스터형 columnstore 인덱스를 사용하는 태스크입니다.  
  
 columnstore 인덱스에 대한 개요는 [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)를 참조하십시오.  
  
 클러스터형 columnstore 인덱스에 대한 자세한 내용은 [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)을 참조하십시오.  
  
## <a name="contents"></a>내용  
  
-   [클러스터형된 Columnstore 인덱스 만들기](#create)  
  
-   [클러스터형된 Columnstore 인덱스를 삭제 합니다.](#drop)  
  
-   [클러스터형 Columnstore 인덱스로 데이터 로드](#load)  
  
-   [클러스터형된 Columnstore 인덱스에 데이터를 변경 합니다.](#change)  
  
-   [클러스터형된 Columnstore 인덱스를 다시 작성](#rebuild)  
  
-   [클러스터형된 Columnstore 인덱스를 다시 구성](#reorganize)  
  
##  <a name="create"></a> 클러스터형된 Columnstore 인덱스 만들기  
 클러스터형된 columnstore 인덱스를 만들려면 먼저 rowstore 테이블을 힙 또는 클러스터형된 인덱스를 만들고 사용 하 여 합니다 [CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) 변환할 테이블을 클러스터형 문 columnstore 인덱스입니다. 클러스터형 columnstore 인덱스의 이름을 클러스터형 인덱스와 동일하게 지정하려면 DROP_EXISTING 옵션을 사용합니다.  
  
 이 예에서는 테이블을 힙으로 만들고 이를 cci_Simple라는 클러스터형 columnstore 인덱스로 변환합니다. 이렇게 하면 전체 테이블의 저장소가 rowstore에서 columnstore로 변경됩니다.  
  
```  
CREATE TABLE T1(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;  
GO  
```  
  
 추가 예제를 보려면 예 섹션을 참조 하세요 [CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)합니다.  
  
##  <a name="drop"></a> 클러스터형된 Columnstore 인덱스를 삭제 합니다.  
 사용 된 [DROP INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/drop-index-transact-sql) 문이 클러스터형된 columnstore 인덱스를 삭제 하려면. 이 연산은 인덱스를 삭제하고 columnstore 테이블을 rowstore 힙으로 변환합니다.  
  
##  <a name="load"></a> 클러스터형 Columnstore 인덱스로 데이터 로드  
 표준 로딩 방법 중 하나를 사용하여 기존 클러스터형 columnstore 인덱스에 데이터를 추가할 수 있습니다.  예를 들어, bcp 대량 로드 도구, Integration Services 및 INSERT... SELECT는 모두 클러스터형 columnstore 인덱스에 데이터를 로드할 수 있습니다.  
  
 클러스터형 columnstore 인덱스는 columnstore의 열 세그먼트 조각화를 방지하기 위해 deltastore를 활용합니다.  
  
### <a name="loading-into-a-partitioned-table"></a>분할된 테이블로 로드  
 분할된 데이터에 대해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 먼저 각 행을 파티션에 할당한 다음 파티션 내에서 데이터에 columnstore 작업을 수행합니다. 각 파티션에는 고유한 행 그룹 수와 적어도 하나의 deltastore가 있습니다.  
  
### <a name="deltastore-loading-scenarios"></a>Deltastore 로드 시나리오  
 행 수가 행 그룹에 허용된 최대 행 수에 도달할 때까지 행은 deltastore에 누적됩니다. Deltastore 행 그룹당 최대 수를 포함 하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] "CLOSED"로 표시 합니다. 백그라운드 프로세스가 "tuple-mover" 라는 닫힌된 행 그룹을 발견 하며 여기서 행 그룹이 열 세그먼트로 압축 되 고 열 세그먼트가 columnstore에 저장 된 columnstore로 이동 합니다.  
  
 클러스터형 columnstore 인덱스마다 여러 deltastore가 있을 수 있습니다.  
  
-   deltastore가 잠겨 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 다른 deltastore를 잠그려고 합니다. 사용 가능한 deltastore가 없으면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 새 deltastore를 만듭니다.  
  
-   분할된 테이블의 경우 각 파티션에 대해 하나 이상의 deltastore가 있을 수 있습니다.  
  
 다음 시나리오에서는 클러스터형 columnstore 인덱스에 대해서만 로드된 행이 언제 columnstore로 곧바로 이동하거나 deltastore로 이동하는지를 설명합니다.  
  
 예를 들어, 각 행 그룹에는 행 그룹당 102,400-1,048,576행이 있을 수 있습니다.  
  
|대량 로드할 행|Columnstore에 추가된 행|Deltastore에 추가된 행|  
|-----------------------|-----------------------------------|----------------------------------|  
|102,000|0|102,000|  
|145,000|145,000<br /><br /> 행 그룹 크기: 145,000|0|  
|1,048,577|1,048,576<br /><br /> 행 그룹 크기: 1,048,576.|1|  
|2,252,152|2,252,152<br /><br /> 행 그룹 크기: 1,048,576, 1,048,576, 155,000.|0|  
  
 다음 예제에서는 1,048,577행을 파티션으로 로드하는 결과를 보여 줍니다. 결과에는 columnstore에 COMPRESSED 행 그룹이 하나 있고(열 세그먼트로 압축됨) deltastore에 행이 1개 있습니다.  
  
```  
SELECT * FROM sys.column_store_row_groups  
```  
  
 ![일괄 처리 로드를 위한 행 그룹 및 deltastore](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "일괄 처리 로드를 위한 행 그룹 및 deltastore")  
  

  
##  <a name="change"></a> 클러스터형된 Columnstore 인덱스에 데이터를 변경 합니다.  
 클러스터형 columnstore 인덱스는 DML 삽입, 업데이트 및 삭제 작업을 지원합니다.  
  
 사용 하 여 [삽입 &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql) 행을 삽입 합니다. 그러면 행이 deltastore에 추가됩니다.  
  
 행을 삭제하려면 [DELETE&#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) 를 사용합니다.  
  
-   행이 columnstore에 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 행을 논리적으로 삭제된 것으로 표시하지만, 인덱스가 다시 작성될 때까지는 행에 대한 물리적 저장소를 회수하지 않습니다.  
  
-   행이 deltastore에 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 행을 논리적 및 물리적으로 삭제합니다.  
  
 행을 삭제하려면 [UPDATE&#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) 를 사용합니다.  
  
-   행이 columnstore에 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 행을 논리적으로 삭제됨으로 표시한 다음 업데이트된 행을 deltastore에 삽입합니다.  
  
-   행이 deltastore에 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 deltastore에 있는 행을 업데이트합니다.  
  
##  <a name="rebuild"></a> 클러스터형된 Columnstore 인덱스를 다시 작성  
 사용 하 여 [CREATE CLUSTERED COLUMNSTORE INDEX &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) 하거나 [ALTER INDEX &#40;Transact SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql) 기존 클러스터형된 columnstore 인덱스의 전체 다시 빌드를 수행 하 합니다. 또한 ALTER INDEX ... REBUILD를 사용하여 다시 작성할 수 있습니다.  
  
### <a name="rebuild-process"></a>프로세스 다시 작성  
 클러스터형 columnstore 인덱스를 다시 작성하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   다시 작성 작업이 발생한 동안 테이블 또는 파티션에서 배타적 잠금을 획득합니다.  다시 작성 중에 데이터는 “오프라인”이며 사용할 수 없습니다.  
  
-   테이블에서 논리적으로 삭제된 행을 물리적으로 삭제하여 columnstore를 조각 모음합니다. 삭제된 바이트는 물리적 미디어에서 회수됩니다.  
  
-   인덱스를 다시 작성하기 전에 deltastore의 rowstore 데이터를 columnstore의 데이터와 병합합니다. 다시 작성 작업을 마치면 모든 데이터가 columnstore 형식으로 저장되며 deltastore는 비워집니다.  
  
-   모든 데이터를 columnstore로 다시 압축합니다. 다시 작성 작업이 발생한 동안에는 columnstore 인덱스의 두 복사본이 존재합니다. 다시 작성 작업이 끝나면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 원래 columnstore 인덱스를 삭제합니다.  
  
### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>클러스터형 Columnstore 인덱스 다시 작성 관련 권장 사항  
 클러스터형 columnstore 인덱스 다시 작성은 조각화 제거 및 모든 행을 columnstore로 이동하는 데 유용합니다. 다음 권장 사항을 고려할 수 있습니다.  
  
-   전체 테이블 대신 파티션을 다시 작성합니다.  
  
    1.  인덱스가 큰 경우 전체 테이블을 다시 작성하려면 많은 시간이 소요되고 다시 작성 중에 인덱스의 추가 복사본을 저장할 수 있는 충분한 디스크 공간이 필요합니다. 일반적으로 가장 최근에 사용한 파티션만 다시 작성하면 됩니다.  
  
    2.  분할된 테이블의 경우 최근 수정된 파티션에서만 주로 조각화가 발생하므로 전체 columnstore 인덱스를 다시 작성할 필요는 없습니다. 팩트 테이블 및 대규모 차원 테이블은 일반적으로 테이블 청크에서 백업 및 관리 작업을 수행하기 위해 분할됩니다.  
  
-   리소스 사용량이 많은 DML 작업 후 파티션을 다시 작성합니다.  
  
     파티션을 다시 작성하면 파티션을 조각 모음하여 디스크 스토리지를 줄일 수 있습니다. 다시 작성 시 columnstore에서 삭제 표시된 모든 행이 삭제되고 deltastore의 모든 행이 columnstore로 이동됩니다.  
  
-   데이터를 로드한 후 파티션을 다시 작성합니다.  
  
     이렇게 하면 모든 데이터가 columnstore에 저장됩니다. 여러 로드를 동시에 수행하면 각 파티션에 여러 deltastore가 생길 수 있습니다. 다시 작성 시 deltastore의 모든 행이 columnstore로 이동됩니다.  
  
##  <a name="reorganize"></a> 클러스터형된 Columnstore 인덱스를 다시 구성  
 클러스터형 columnstore 인덱스를 다시 구성하면 모든 CLOSED 행 그룹이 columnstore로 이동됩니다. 재구성을 수행 하려면 사용 [ALTER INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)REORGANIZE 옵션을 사용 하 여 합니다.  
  
 CLOSED 행 그룹을 columnstore로 이동할 경우에는 다시 구성할 필요가 없습니다. tuple-mover 프로세스에서 모든 CLOSED 행 그룹을 찾아서 이동합니다. 하지만 tuple-mover는 단일 스레드이므로 작업에 맞게 충분히 빠르게 행 그룹을 이동하지 못할 수 있습니다.  
  
### <a name="recommendations-for-reorganizing"></a>재구성 관련 권장 사항  
 클러스터형 columnstore 인덱스를 다시 구성해야 하는 경우:  
  
-   하나 이상의 데이터 로드 후에는 최대한 빠르게 쿼리 성능 장점을 얻기 위해 클러스터형 columnstore 인덱스를 다시 구성합니다. 다시 구성하려면 처음에 데이터를 압축하기 위한 추가 CPU 리소스가 필요하므로 전체 시스템 성능이 느려질 수 있습니다. 하지만 데이터가 압축되는 즉시 쿼리 성능을 향상할 수 있습니다.  
  
  
