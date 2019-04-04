---
title: 분할된 테이블 및 인덱스 | Microsoft 문서
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
- index partitions
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: add30d400db0a4ce73313ac5b7c4637bff8adfd9
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658297"
---
# <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 테이블 및 인덱스 분할을 지원합니다. 분할 테이블 및 인덱스의 데이터는 데이터베이스에서 두 개 이상의 파일 그룹으로 분할될 수 있는 단위로 나뉩니다. 행 그룹이 개별 파티션에 매핑되도록 데이터는 수평적으로 분할됩니다. 단일 인덱스나 테이블의 모든 파티션은 동일 데이터베이스에 상주해야 합니다. 데이터에서 쿼리나 업데이트가 수행되면 테이블이나 인덱스는 단일 논리적 엔터티로 처리됩니다. [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 전에는 분할된 테이블 및 인덱스를 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 기본적으로 최대 15,000개의 파티션을 지원합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전에서는 파티션 수가 기본적으로 1,000개로 제한되었습니다. x86 기반 시스템에서는 파티션 수가 1,000개를 초과하는 테이블 또는 인덱스를 만들 수 있지만 해당 테이블 또는 인덱스는 지원되지 않습니다.  
  
## <a name="benefits-of-partitioning"></a>분할의 이점  
 큰 테이블 또는 인덱스를 분할하면 관리 효율성과 성능 면에서 다음과 같은 이점이 있습니다.  
  
-   데이터 하위 집합을 빠르고 효율적으로 전송하거나 액세스할 수 있을 뿐만 아니라 데이터 컬렉션의 무결성을 유지할 수 있습니다. 예를 들어 데이터를 분할하지 않은 상태에서 몇 분 내지 몇 시간이 걸렸던 작업(예: OLTP에서 OLAP 시스템으로 데이터 로드)이 몇 초 안에 끝납니다.  
  
-   하나 이상의 파티션에서 유지 관리 작업을 더 빠르게 수행할 수 있습니다. 전체 테이블 대신 이 데이터 하위 집합만 대상으로 하기 때문에 작업이 더 효율적입니다. 예를 들어 하나 이상의 파티션에서 데이터를 압축하거나 인덱스의 파티션 중 하나 이상을 다시 작성할 수 있습니다.  
  
-   자주 실행하는 쿼리 유형과 사용 중인 하드웨어 구성에 따라 쿼리 성능이 향상될 수 있습니다. 예를 들어 쿼리 최적화 프로그램에서는 파티션 자체를 조인할 수 있으므로 테이블의 분할 열이 동일한 경우 두 개 이상의 분할된 테이블 간의 동등 조인 쿼리를 더 빠르게 처리할 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 I/O 작업을 위해 데이터를 정렬할 때 먼저 파티션을 기준으로 데이터가 정렬됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 한 번에 한 드라이브에 액세스하므로 성능이 저하될 수 있습니다. 데이터 저장 성능을 향상시키려면 RAID를 설정하여 두 개 이상의 디스크 간에 파티션의 데이터 파일을 스트라이프합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 여전히 파티션을 기준으로 데이터를 정렬하지만 동시에 각 파티션의 모든 드라이브에 액세스할 수 있습니다.  
  
또한 전체 테이블이 아니라 파티션 수준에서 잠금 에스컬레이션을 설정하여 성능을 향상시킬 수 있습니다. 따라서 테이블의 잠금 경합을 줄일 수 있습니다. 파티션에 잠금 에스컬레이션을 허용하여 잠금 경합을 줄이려면 `ALTER TABLE` 문의 `LOCK_ESCALATION` 옵션을 AUTO로 설정합니다. 
  
## <a name="components-and-concepts"></a>구성 요소 및 개념  
테이블 및 인덱스 분할에 적용되는 용어는 다음과 같습니다.  
  
### <a name="partition-function"></a>파티션 함수  
분할 열이라고 하는 특정 열의 값을 기반으로 파티션 집합에 테이블이나 인덱스의 행을 매핑하는 방식을 정의하는 데이터베이스 개체입니다. 즉, 파티션 함수는 테이블이 포함할 파티션 수를 정의하고 파티션 경계의 정의 방법을 정의합니다. 예를 들어 매출 주문 데이터가 포함된 테이블이 있다고 가정할 경우 매출 날짜와 같은 **datetime** 열을 기준으로 테이블을 12개(월별) 파티션으로 분할해야 할 수 있습니다.  
  
### <a name="partition-scheme"></a>파티션 구성표 
파티션 함수의 파티션을 파일 그룹 집합으로 매핑하는 데이터베이스 개체입니다. 별개의 파일 그룹에 파티션을 넣는 주된 이유는 파티션 백업 작업을 독립적으로 수행하기 위해서입니다. 이는 개별 파일 그룹에 대해 백업을 수행할 수 있기 때문입니다.  
  
### <a name="partitioning-column"></a>분할 열  
파티션 함수가 테이블이나 인덱스를 분할하는 데 사용하는 테이블 또는 인덱스의 열입니다. 파티션 함수에 참여하는 계산 열은 명시적으로 PERSISTED로 표시되어야 합니다. **timestamp**를 제외하고 인덱스 열로 사용할 수 있는 모든 데이터 형식을 분할 열로 사용할 수 있습니다. **ntext**, **text**, **image**, **xml**, **varchar(max)**, **nvarchar(max)** 또는 **varbinary(max)** 데이터 형식은 지정할 수 없습니다. 또한 Microsoft .NET Framework CLR(공용 언어 런타임) 사용자 정의 유형 및 별칭 데이터 형식 열은 지정할 수 없습니다.  
  
### <a name="aligned-index"></a>정렬된 인덱스  
해당 테이블과 동일한 파티션 구성표를 기반으로 작성되는 인덱스입니다. 테이블과 인덱스가 정렬되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 테이블과 인덱스의 파티션 구조를 유지하면서 신속하고 효율적으로 파티션을 전환할 수 있습니다. 인덱스가 기본 테이블에 맞게 정렬되기 위해 반드시 같은 이름의 파티션 함수를 사용할 필요는 없습니다. 그러나 인덱스 및 기본 테이블의 파티션 함수는 다음과 같은 측면에서 기본적으로 동일해야 합니다.
 1. 파티션 함수의 인수는 같은 데이터 형식입니다.
 2. 같은 수의 파티션을 정의합니다.
 3. 파티션에 대해 같은 경계 값을 정의합니다.  

#### <a name="partitioning-clustered-indexes"></a>클러스터형 인덱스 분할
클러스터형 인덱스를 분할하는 경우 클러스터링 키에 분할 열이 포함되어야 합니다. 고유하지 않은 클러스터형 인덱스를 분할하는 경우 분할 열이 클러스터링 키에 명시적으로 지정되어 있지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 분할 열이 클러스터형 인덱스 키 목록에 기본적으로 추가됩니다. 클러스터형 인덱스가 고유하면 클러스터형 인덱스 키에 분할 열이 포함되도록 명시적으로 지정해야 합니다.        

#### <a name="partitioning-nonclustered-indexes"></a>비클러스터형 인덱스 분할
고유한 비클러스터형 인덱스를 분할하는 경우 인덱스 키에 분할 열이 포함되어야 합니다. 고유하지 않은 비클러스터형 인덱스를 분할하는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기본적으로 분할 열이 키가 아닌(포함된) 인덱스 열로 추가되어 인덱스가 기본 테이블에 맞게 정렬됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이미 인덱스에 분할 열이 있으면 분할 열이 인덱스에 추가되지 않습니다. 

### <a name="non-aligned-index"></a>정렬되지 않은 인덱스  
해당 테이블과 독립적으로 분할된 인덱스입니다. 즉, 인덱스의 파티션 구성표가 다르거나 인덱스가 기본 테이블과 다른 파일 그룹에 생성됩니다. 다음과 같은 경우에는 정렬되지 않은 분할된 인덱스를 디자인하는 것이 유용할 수 있습니다.  
-   기본 테이블이 분할되지 않은 경우  
-   인덱스 키가 고유하고 테이블의 분할 열을 포함하고 있지 않은 경우  
-   기본 테이블이 다른 조인 열을 사용하여 추가 테이블과의 배치된 조인에 참여하도록 하려는 경우  

### <a name="partition-elimination"></a>파티션 제거
쿼리 최적화 프로그램에서 관련 파티션만 액세스하여 쿼리의 필터 조건을 충족하기 위해 사용되는 프로세스입니다.  

## <a name="performance-guidelines"></a>성능 지침  
 파티션 수 제한이 15,000개로 늘어나서 메모리, 분할된 인덱스 작업, DBCC 명령 및 쿼리에 영향을 줍니다. 이 섹션에서는 파티션 수를 1,000개 이상으로 늘리는 경우의 성능 영향에 대해 설명하고 필요한 경우 해결 방법을 제시합니다. 최대 파티션 수 제한을 15,000개로 늘리면 데이터를 더 오래 동안 저장할 수 있습니다. 하지만 데이터를 필요한 기간 동안만 저장하고 성능과 파티션 수를 균형되게 조정해야 합니다.  
  
### <a name="processor-cores-and-number-of-partitions-guidelines"></a>프로세서 코어 및 파티션 수 지침  
 병렬 작업의 성능을 최대화하기 위해 프로세서 코어와 동일한 수의 파티션을 최대 64개([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 활용할 수 있는 병렬 프로세서의 최대 수) 사용하는 것이 좋습니다.  
  
### <a name="memory-usage-and-guidelines"></a>메모리 사용량 및 지침  
 많은 수의 파티션을 사용할 경우 16GB 이상의 RAM을 사용하는 것이 좋습니다. 시스템의 메모리가 부족할 경우 DML(데이터 정의 언어), DDL(데이터 조작 언어) 문 및 기타 작업이 실패할 수 있습니다. 메모리를 많이 사용하는 프로세스를 실행하는 16GB RAM이 장착된 시스템에서 많은 수의 파티션에서 실행되는 작업을 수행하면 메모리가 부족해질 수 있습니다. 따라서 메모리(16GB 이상)가 많을수록 성능 및 메모리 문제가 발생할 가능성이 더 낮아집니다.  
  
 메모리 제한 사항은 분할된 인덱스를 작성하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능 또는 기능에 영향을 줄 수 있습니다. 이러한 제한 사항은 이미 테이블에 정렬된 클러스터형 인덱스가 있고 인덱스가 기본 테이블 또는 클러스터형 인덱스에 맞게 정렬되지 않은 경우에 크게 영향을 줍니다. 이 경우 인덱스 생성 메모리 서버 구성 옵션을 늘리는 것이 유용할 수 있습니다. 자세한 내용은 [인덱스 생성 메모리 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)을 참조하세요. 
  
### <a name="partitioned-index-operations"></a>분할된 인덱스 작업  
파티션 수가 1,000개를 초과하는 테이블에서 정렬되지 않은 인덱스를 만들거나 다시 작성할 수 있지만 해당 인덱스는 지원되지 않습니다. 그러면 작업 중에 성능이 저하되거나 메모리가 과도하게 소비될 수 있습니다.  
  
파티션 수가 늘어날수록 정렬된 인덱스를 만들거나 다시 작성하는 데 더 많은 시간이 걸릴 수 있습니다. 인덱스 만들기 및 다시 작성 명령을 한 번에 여러 개씩 실행하지 않는 것이 좋습니다. 그러면 성능 및 메모리 문제가 발생할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 정렬을 수행하여 분할된 인덱스를 작성할 때는 먼저 파티션마다 하나씩 정렬 테이블을 만듭니다. 그런 다음 각 파티션에 있는 각각의 파일 그룹에 정렬 테이블을 만들거나 SORT_IN_TEMPDB 인덱스 옵션이 지정된 경우 **tempdb**에 정렬 테이블을 만듭니다. 각 정렬 테이블을 만드는 데는 최소 메모리 크기가 요구됩니다. 기본 테이블에 맞게 정렬된 분할된 인덱스를 작성할 때는 정렬 테이블이 한 번에 하나씩 만들어지므로 메모리가 적게 소모됩니다. 그러나 정렬되지 않은 분할된 인덱스를 작성할 때는 모든 정렬 테이블이 동시에 만들어집니다. 따라서 이러한 동시 정렬을 처리하기에 충분한 메모리 양이 필요하게 됩니다. 파티션의 수가 많을수록 필요한 메모리 양은 늘어납니다. 파티션별 각 정렬 테이블의 최소 크기는 40페이지이며 페이지당 8KB의 용량이 필요합니다. 예를 들어 정렬되지 않은 분할된 인덱스의 파티션 수가 100개이면 4,000(40*100)페이지를 동시에 연속적으로 정렬하기에 충분한 메모리 양이 필요합니다. 메모리가 충분하면 인덱스 작성 작업을 수행할 수 있지만 성능이 저하될 수 있습니다. 메모리가 충분하지 않으면 작성 작업을 수행할 수 없습니다. 반면 정렬된 분할된 인덱스의 경우 파티션 수가 100개라도 정렬 작업이 동시에 수행되지 않으므로 40페이지를 정렬하기에 충분한 메모리만 있으면 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 다중 프로세서 컴퓨터에서 작성 작업을 수행할 때 병렬 처리 수준을 적용하면 정렬된 인덱스와 정렬되지 않은 인덱스 모두 메모리 요구 사항이 더 커질 수 있습니다. 이는 병렬 처리 수준이 높을수록 메모리 요구 사항이 커지기 때문입니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 병렬 처리 수준을 4로 설정하면 파티션 수가 100개인 정렬되지 않은 분할된 인덱스의 경우 4개의 프로세서에서 4,000페이지(16,000페이지)를 동시에 정렬하는 데 충분한 메모리 크기가 필요하게 됩니다. 분할된 인덱스가 정렬되어 있는 경우에는 4개의 프로세서에서 40페이지, 즉 160페이지(4*40)를 정렬할 수 있는 메모리 크기만 있으면 됩니다. 병렬 처리 수준은 MAXDOP 인덱스 옵션을 사용하여 수동으로 낮출 수 있습니다.  

### <a name="dbcc-commands"></a>DBCC 명령  
파티션 수가 늘어날수록 DBCC 명령을 실행하는 데 더 많은 시간이 걸릴 수 있습니다.  
  
### <a name="queries"></a>쿼리  
파티션 제거를 사용하는 쿼리는 파티션 수가 많을 경우 향상된 성능을 나타낼 수 있습니다. 파티션 제거를 사용하지 않는 쿼리는 파티션 수가 늘어나면 실행하는 데 더 많은 시간이 걸릴 수 있습니다.  
  
예를 들어 테이블에 1억 개의 행과 `A`, `B`및 `C`열이 있다고 가정합니다. 
-  시나리오 1에서는 테이블의 `A`열이 1,000개의 파티션으로 분할됩니다. 
-  시나리오 2에서는 테이블의 `A`열이 10,000개의 파티션으로 분할됩니다. `A` 열에서 필터링하는 `WHERE` 절이 있는 테이블에 대한 쿼리는 파티션 제거를 수행하고 파티션 하나를 검사합니다. 시나리오 2에서는 파티션에 검사할 행이 더 적기 때문에 동일한 쿼리가 더 빠르게 실행될 수 있습니다. B 열에서 필터링하는 `WHERE` 절이 있는 쿼리는 모든 파티션을 검사합니다. 시나리오 1에서는 시나리오 2보다 검사할 파티션 수가 더 적기 때문에 쿼리가 더 빠르게 실행될 수 있습니다.  

분할 열이 아닌 열에서 TOP 또는 MAX/MIN과 같은 연산자를 사용하는 쿼리에서는 모든 파티션이 평가되어야 하므로 분할 성능이 저하될 수 있습니다.  

두 개 이상의 분할된 테이블 간의 동등 조인을 수반하는 쿼리를 자주 실행할 경우 해당 분할 열과 테이블이 조인되는 열이 같아야 합니다. 또한 테이블이나 해당 인덱스를 배치해야 합니다. 즉, 같은 이름의 파티션 함수를 사용하거나 다음과 같이 본질적으로 동일한 다른 함수를 사용합니다.
-  분할에 사용되는 매개 변수 수가 같고 해당 매개 변수의 데이터 형식이 같습니다.
-  같은 수의 파티션을 정의하는 경우
-  파티션에 대해 같은 경계 값을 정의하는 경우
이러한 방식을 통해 파티션 자체를 조인할 수 있기 때문에 쿼리 최적화 프로그램에서 조인을 보다 빠르게 처리할 수 있습니다. 쿼리가 조인하는 두 테이블이 배치되지 않았거나 조인 필드에서 분할되지 않았으면 파티션으로 인해 쿼리 처리가 빨라지는 대신 실제로 느려질 수 있습니다.

## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>분할된 인덱스 작업 중 통계 계산의 동작 변경 내용  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 분할된 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 작성하지 않습니다. 대신 쿼리 최적화 프로그램에서 기본 샘플링 알고리즘을 사용하여 통계를 생성합니다. 분할된 인덱스로 데이터베이스를 업그레이드한 후 인덱스에 대한 히스토그램 데이터가 달라집니다. 이 동작 변경이 쿼리 성능에는 영향을 주지 않을 수 있습니다. 테이블의 모든 행을 검사하여 분할된 인덱스에 대한 통계를 얻으려면 `FULLSCAN` 절에서 `CREATE STATISTICS` 또는 `UPDATE STATISTICS`를 사용합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**태스크**|**항목**|  
|파티션 함수와 파티션 구성표를 만든 다음 테이블 및 인덱스에 적용하는 방법에 대해 설명합니다.|[분할된 테이블 및 인덱스 만들기](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>관련 내용  
 분할된 테이블 및 인덱스 전략과 구현에 대한 자세한 내용은 다음 백서를 참조하십시오.  
-   [SQL Server 2008을 사용할 경우의 분할된 테이블 및 인덱스 전략](https://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)    
-   [자동 슬라이딩 윈도우를 구현하는 방법](https://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)    
-   [분할된 테이블로 대량 로드](https://msdn.microsoft.com/library/cc966380.aspx)    
-   [Project REAL: 데이터 수명 주기 -- 분할](https://technet.microsoft.com/library/cc966424.aspx)    
-   [분할된 테이블 및 인덱스에서의 향상된 쿼리 처리](https://msdn.microsoft.com/library/ms345599.aspx)    
-   _SQLCAT의 가이드: 관계형 엔진_의 [대규모 관계형 데이터 웨어하우스 빌드를 위한 상위 10가지 모범 사례](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/SQLCAT's%20Guide%20to%20Relational%20Engine.pdf)
  
  
