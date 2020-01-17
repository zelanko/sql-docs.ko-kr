---
title: 페이지 및 익스텐트 아키텍처 가이드 | Microsoft 문서
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- page and extent architecture guide
- guide, page and extent architecture
ms.assetid: 83a4aa90-1c10-4de6-956b-7c3cd464c2d2
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 971848a9feddd9cff64bafb5cadf36ab8bdc01e3
ms.sourcegitcommit: a92fa97e7d3132ea201e4d86c76ac39cd564cd3c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2019
ms.locfileid: "75325495"
---
# <a name="pages-and-extents-architecture-guide"></a>페이지 및 익스텐트 아키텍처 가이드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

페이지는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기본 데이터 스토리지 단위입니다. 익스텐트는 물리적인 연속 페이지 8개의 모음입니다. 익스텐트는 효과적인 페이지 관리에 도움이 됩니다. 이 가이드에서는 모든 SQL Server 버전에서 페이지 및 익스텐트를 관리하는 데 사용되는 데이터 구조에 대해 설명합니다. 페이지 및 익스텐트의 아키텍처에 대한 이해는 효율적으로 동작하는 데이터베이스를 디자인하고 개발하는 데 있어 중요합니다.

## <a name="pages-and-extents"></a>페이지 및 익스텐트

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 기본 데이터 스토리지 단위는 페이지입니다. 데이터베이스에서 데이터 파일(.mdf 또는 .ndf)에 할당되는 디스크 공간은 논리적인 페이지로 나뉘어지며 0에서 n 사이의 숫자가 연속으로 페이지에 매겨집니다. 디스크 I/O 작업은 페이지 수준에서 수행됩니다. 즉, SQL Server가 전체 데이터 페이지를 읽거나 씁니다.

익스텐트는 실제로 연속하는 8페이지를 모은 것으로 페이지를 효율적으로 관리하는 데 사용됩니다. 모든 페이지는 익스텐트가 구성됩니다.

### <a name="pages"></a>페이지

일반 책 사용: 모든 콘텐츠가 페이지에 기록됩니다. 책과 마찬가지로 SQL Server에서도 모든 데이터 행이 페이지에 기록됩니다. 책에서 모든 페이지의 실제 크기는 동일합니다. 마찬가지로 SQL Server에서도 모든 데이터 페이지의 크기는 8kb로 동일합니다. 책에서 대부분의 페이지에는 책의 주요 내용이 포함되어 있으며 일부 페이지에는 내용에 대한 메타데이터가 포함되어 있습니다. 예를 들어 목차와 인덱스 테이블 등입니다. 역시 SQL Server도 다르지 않습니다. 대부분의 페이지에는 사용자가 저장한 실제 데이터 행이 포함되어 있습니다. 이를 데이터 페이지 및 텍스트/이미지 페이지(특수한 경우)라고 합니다. 인덱스 페이지에는 데이터가 있는 위치에 대한 인덱스 참조가 포함되고, 마지막으로 데이터의 구성에 대한 다양한 메타데이터를 저장하는 시스템 페이지(PFS, GAM, SGAM, IAM, DCM, BCM 페이지)가 있습니다. 페이지 유형 및 설명은 아래 표를 참조하세요.

앞에서 설명한 대로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 페이지 크기는 8KB입니다. 이 사실은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 메가바이트당 128페이지가 있음을 의미합니다. 각 페이지는 96바이트 머리글로 시작하는데 이 머리글은 페이지에 대한 시스템 정보를 저장하는 데 사용됩니다. 페이지 번호, 페이지 유형, 해당 페이지의 사용 가능한 공간 크기 그리고 해당 페이지를 소유하고 있는 개체의 할당 단위 ID와 같은 정보를 저장합니다.

다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 데이터 파일에서 사용되는 페이지 유형을 보여 줍니다.

|페이지 유형 | 콘텐츠 |
|-------|-------|
|data |text in row를 ON으로 설정한 경우 온갖 데이터를 포함한 데이터 행. 단, 텍스트, ntext, 이미지, nvarchar(max), varchar(max), varbinary(max), xml 데이터 제외. |
|인덱스 |인덱스 항목 |
|텍스트/이미지 |LOB(Large Object) 데이터 유형: (텍스트, ntext, 이미지, nvarchar(max), varchar(max), varbinary(max), xml 데이터) <br> 데이터 행이 8KB를 초과하는 경우 가변 길이 열: (varchar, nvarchar, varbinary, and sql_variant) |
|전역 할당 맵, 공유 전역 할당 맵 |익스텐트가 할당되었는지 여부에 대한 정보 |
|페이지의 사용 가능한 공간(PFS) |페이지 할당 및 페이지의 사용 가능한 공간에 대한 정보 |
|IAM(Index Allocation Map) |테이블 또는 인덱스에서 할당 단위당 사용하는 익스텐트에 대한 정보 |
|대량 변경 맵 |마지막 BACKUP LOG 문 이후에 할당 단위당 대량 작업에 의해 수정된 익스텐트에 대한 정보 |
|차등 변경 맵 |마지막 BACKUP DATABASE 문 이후에 할당 단위당 변경된 익스텐트에 대한 정보 |

> [!NOTE]
> 로그 파일은 페이지는 포함하지 않으며 일련의 로그 레코드를 포함합니다.

데이터 행은 머리글 바로 다음부터 시작하여 페이지에 차례로 나옵니다. 행 오프셋 테이블은 페이지 끝에서 시작하는데 각 행 오프셋 테이블에는 해당 페이지에 있는 각 행에 대한 항목이 하나씩 있습니다. 각 행 오프셋 항목은 행의 첫 번째 바이트가 페이지 시작 지점에서 얼마나 떨어져 있는지를 기록합니다. 따라서 행 오프셋 테이블 함수는 SQL Server가 페이지에서 행을 빠르게 찾는 데 도움이 됩니다. 행 오프셋 테이블의 항목 순서는 페이지의 행 순서의 역순입니다.

![page_architecture](../relational-databases/media/page-architecture.gif)

#### <a name="large-row-support"></a>대용량 행 지원  

행들이 여러 페이지에 걸쳐 있을 수 없지만 그러한 행 부분들이 해당 행의 페이지를 벗어나서 해당 행이 실제로는 아주 커질 수 있습니다. 한 페이지의 단일 행에 데이터와 오버헤드가 최대 8,060바이트(8KB)까지 저장됩니다. 그러나 텍스트/이미지 페이지 유형에 저장되는 데이터는 여기에 포함되지 않습니다. 

이 제한은 varchar, nvarchar, varbinary 또는 sql_variant 열이 있는 테이블에는 제한적으로 적용됩니다. 테이블에 있는 모든 고정 및 변수 열의 전체 행 크기가 8,060바이트 한계를 초과하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 하나 이상의 가변 길이 열을 가장 너비가 넓은 열부터 시작하여 ROW_OVERFLOW_DATA 할당 단위에 있는 페이지로 동적으로 옮깁니다. 

삽입 또는 업데이트 작업으로 행의 전체 크기가 8,060바이트 한계를 초과하면 이러한 작업이 수행됩니다. 열이 ROW_OVERFLOW_DATA 할당 단위의 페이지로 이동하면 IN_ROW_DATA 할당 단위에 있는 원래 페이지의 24바이트 포인터가 그대로 유지됩니다. 후속 작업으로 행 크기가 줄면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]가 동적으로 열을 다시 원래 데이터 페이지로 이동합니다. 

##### <a name="row-overflow-considerations"></a>행 오버플로 고려 사항 

앞서 설명한 것처럼 행은 여러 페이지에 상주할 수 없으며, 가변 길이 데이터 형식 필드의 결합된 크기가 8,060바이트 한도를 초과할 경우 오버플로가 발생할 수 있습니다. 이 내용을 설명하기 위해 각각 varchar(7000)와 varchar(2000)인 두 열을 사용하여 테이블을 만들 수 있습니다. 개별적으로 두 열은 모두 8,060바이트를 초과하지 않지만, 각 열의 전체 너비를 채울 경우 합계가 8,060바이트를 초과합니다. SQL Server는 varchar(7000) 가변 길이 열을 ROW_OVERFLOW_DATA 할당 단위의 페이지로 동적으로 이동할 수 있습니다. 행당 8,060바이트를 초과하는 varchar, nvarchar, varbinary, sql_variant 또는 CLR 사용자 정의 형식 열을 결합할 때는 다음 사항을 고려하세요.
-  업데이트 작업에 따라 레코드가 길어지는 경우 큰 레코드는 동적으로 다른 페이지로 이동합니다. 업데이트 작업에 따라 레코드가 짧아지는 경우 해당 레코드는 IN_ROW_DATA 할당 단위에 있는 원래 페이지로 다시 이동할 수도 있습니다. 행 오버플로 데이터가 포함된 큰 레코드에 대한 정렬이나 조인 같은 다른 SELECT 작업을 쿼리 및 수행하면 해당 레코드가 비동기적으로 처리되지 않고 동기적으로 처리되기 때문에 처리 시간이 느려집니다.   
   따라서 여러 varchar, nvarchar, varbinary, sql_variant 또는 CLR 사용자 정의 형식 열이 있는 테이블을 디자인할 때는 오버플로될 가능성이 있는 행의 비율과 이 오버플로 데이터가 자주 쿼리될 가능성이 있는지 고려하십시오. 행 오버플로 데이터가 있는 다수의 행에서 쿼리가 자주 수행될 가능성이 높은 경우에는 일부 열이 다른 테이블로 이동하도록 테이블을 정규화하십시오. 그런 다음 비동기 JOIN 작업에서 이 테이블을 쿼리할 수 있습니다. 
-  varchar, nvarchar, varbinary, sql_variant 및 CLR 사용자 정의 형식 열의 개별 열 길이에는 여전히 8,000바이트의 제한이 적용되어야 합니다. 이 열이 결합되는 경우에만 테이블의 8,060바이트의 행 제한을 초과할 수 있습니다.
-  char 및 nchar 데이터를 비롯하여 다른 데이터 형식 열의 합계에는 8,060바이트의 행 제한이 적용되어야 합니다. 큰 개체 데이터도 8,060바이트의 행 제한에서 제외됩니다. 
-  클러스터형 인덱스의 인덱스 키는 ROW_OVERFLOW_DATA 할당 단위에 기존 데이터가 있는 varchar 열을 포함할 수 없습니다. varchar 열에 대한 클러스터형 인덱스를 만들고 기존 데이터가 IN_ROW_DATA 할당 단위에 있는 경우에는 데이터를 행 외부로 밀어넣는 열에 대한 후속 삽입 또는 업데이트 동작이 실패합니다. 할당 단위에 대한 자세한 내용은 Table and Index Organization(테이블 및 인덱스 구성)을 참조하세요.
-  행 오버플로 데이터가 있는 열을 비클러스터형 인덱스의 키 열이나 키가 아닌 열로 포함할 수 있습니다.
-  스파스 열을 사용하는 테이블의 레코드 크기 제한은 8,018바이트입니다. 변환된 데이터와 기존 레코드를 합한 크기가 8,018바이트를 초과하면 [MSSQLSERVER ERROR 576](../relational-databases/errors-events/database-engine-events-and-errors.md)이 반환됩니다. 열이 스파스에서 스파스가 아닌 유형으로 변환되면 데이터베이스 엔진에서 현재 레코드 데이터의 복사본을 보관합니다. 따라서 레코드에 필요한 스토리지 크기가 일시적으로 두 배가 됩니다.
-  행 오버플로 데이터가 포함될 수 있는 테이블이나 인덱스에 대한 정보를 얻으려면 [sys.dm_db_index_physical_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 동적 관리 함수를 사용합니다.

### <a name="extents"></a>Extents 

익스텐트는 공간 관리의 기본 단위입니다. 하나의 익스텐트는 실제로 연속하는 8페이지 또는 64KB입니다. 즉, SQL Server 데이터베이스는 메가바이트당 익스텐트 16개를 저장합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 다음과 같이 두 가지 유형의 익스텐트가 있습니다. 

* **균일** 익스텐트는 단일 개체가 소유합니다. 또한 익스텐트의 전체 8페이지는 소유하는 개체만 사용할 수 있습니다.
* **혼합** 익스텐트는 최대 8개의 개체가 공유할 수 있습니다. 익스텐트의 8페이지를 각각 다른 개체가 소유할 수 있습니다.

최대 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]까지, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 효율적인 공간 할당을 위해 적은 양의 데이터를 포함하는 테이블에 전체 익스텐트를 할당하지 않습니다. 일반적으로 새 테이블이나 인덱스에는 혼합 익스텐트의 페이지를 할당합니다. 테이블이나 인덱스의 페이지가 8페이지로 증가하면 후속 할당을 위해 균일 익스텐트를 사용하도록 전환됩니다. 인덱스에 8개의 페이지를 생성하는 데 충분한 행을 가진 기존 테이블에서 인덱스를 만드는 경우 인덱스에 대한 모든 할당 항목은 균일 익스텐트에 있습니다. 그러나 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]부터 데이터베이스에 있는 모든 할당의 기본값은 균일 익스텐트입니다.

![Extents](../relational-databases/media/extents.gif)

> [!NOTE]
> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]까지, 추적 플래그 1118을 사용하여 항상 균일 익스텐트를 사용하도록 기본 할당을 변경할 수 있습니다. 이 추적 플래그에 대한 자세한 내용은 [DBCC TRACEON - 추적 플래그](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.   
>   
> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]부터 TF 1118에서 제공하는 기능이 TempDB에서 자동으로 사용됩니다. 사용자 데이터베이스의 경우 이 동작은 기본값이 OFF로 설정된 `ALTER DATABASE`의 `SET MIXED_PAGE_ALLOCATION` 옵션에 의해 제어되며, 추적 플래그 1118은 영향을 미치지 않습니다. 자세한 내용은 [ALTER DATABASE SET 옵션(Transact-SQL)](../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.

## <a name="managing-extent-allocations-and-free-space"></a>익스텐트 할당 및 빈 공간 관리 

익스텐트 할당을 관리하고 빈 공간을 추적하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터 구조는 비교적 단순합니다. 다음과 같은 이점이 있습니다. 

* 빈 공간 정보는 빽빽하게 묶여 있으므로 이 정보를 포함하는 페이지의 수는 비교적 적습니다.   
  따라서 할당 정보 검색에 필요한 디스크 읽기 횟수가 줄어들어 속도가 빨라집니다. 더 이상의 읽기가 필요하지 않으므로 할당 페이지가 메모리에 남아 있게 될 확률도 높아집니다. 

* 대부분의 할당 정보는 서로 연결되어 있지 않으므로 유지 관리가 간편합니다.    
  각 페이지 할당 또는 할당 취소 작업을 신속하게 수행할 수 있으므로 페이지를 할당 또는 할당 취소해야 하는 동시 태스크 간의 경합이 줄어듭니다. 

### <a name="managing-extent-allocations"></a>익스텐트 할당 관리

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 다음의 두 가지 형식의 할당 맵을 사용하여 익스텐트의 할당을 기록합니다. 

- **전역 할당 맵(GAM)**    
  GAM 페이지는 어떤 익스텐트가 할당되었는지 기록합니다. 각 GAM은 64,000개의 익스텐트 또는 거의 4GB(기가비트)의 데이터를 처리합니다. GAM은 처리 간격으로 각 익스텐트에 대해 1비트를 갖습니다. 이 비트가 1인 경우 익스텐트는 비어 있고 이 비트가 0인 경우 익스텐트는 할당된 상태입니다. 

- **공유 전역 할당 맵(SGAM)**    
  SGAM 페이지는 어떤 익스텐트가 현재 혼합 익스텐트로 사용되고 있는지와 적어도 하나 이상의 사용되지 않은 페이지를 가지는지 기록합니다. 각 SGAM은 64,000개의 익스텐트 또는 거의 4GB의 데이터를 처리합니다. SGAM은 처리 간격으로 각 익스텐트에 대해 1비트를 갖습니다. 이 비트가 1인 경우 익스텐트가 혼합 익스텐트로 사용되고 있고 빈 페이지를 가지고 있는 상태입니다. 이 비트가 0인 경우 익스텐트가 혼합 익스텐트로 사용되지 않거나, 혼합 익스텐트이고 모든 페이지가 사용되는 상태입니다. 

각 익스텐트는 현재 사용 상태에 기반하여 GAM 및 SGAM에 설정된 다음의 비트 패턴을 갖습니다. 

|현재 익스텐트의 사용 | GAM 비트 설정 | SGAM 비트 설정 |
|---------|----------|------| 
|비어 있음, 사용 중이지 않음 |1 |0 |
|단일 익스텐트 또는 완전 혼합 익스텐트 |0 |0 |
|빈 페이지가 있는 혼합 익스텐트 |0 |1 |
 
이러한 복잡함 때문에 단순한 익스텐트 관리 알고리즘의 필요성이 부각되었습니다. 
-   [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 단일 익스텐트를 할당하기 위해 1비트에 해당하는 GAM을 검색하고 이를 0으로 설정합니다. 
-   또한 빈 페이지가 있는 혼합 익스텐트를 찾기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 1비트에 해당하는 SGAM을 검색합니다. 
-   [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 혼합 익스텐트를 할당하기 위해 1비트에 해당하는 GAM을 검색하고 이를 0으로 설정한 다음 SGAM의 해당 비트를 1로 설정합니다. 
-   또한 익스텐트 할당을 취소하기 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 GAM 비트를 1로 설정하고 SGAM 비트를 0으로 설정합니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 데이터베이스 내에서 균일하게 데이터를 분산시키므로 실제로 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 내부에서 사용하는 알고리즘은 이 문서에서 설명하는 알고리즘보다 더 복잡합니다. 그러나 실제 알고리즘의 경우 익스텐트 할당 정보 체인을 관리하지 않아도 되므로 이보다 더 단순합니다.

### <a name="tracking-free-space"></a>빈 공간 추적

**PFS(Page Free Space)** 페이지는 개별 페이지의 할당 여부 및 각 페이지에 있는 빈 공간의 양과 같은 페이지의 할당 상태를 기록합니다. PFS는 각 페이지에 1바이트를 사용하여 페이지의 할당 여부를 기록하고 할당된 경우 페이지의 상태를 비어 있음, 1~50% 채워짐, 51~80% 채워짐, 81~95% 채워짐 또는 96~100% 채워짐으로 기록합니다.

개체에 익스텐트가 할당된 후에는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 PFS 페이지를 사용하여 익스텐트의 할당된 페이지 또는 빈 페이지를 기록합니다. 이 정보는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 새 페이지를 할당해야 할 때 사용됩니다. 힙 및 텍스트/이미지 페이지에 대해서만 페이지 내의 빈 공간의 양이 관리됩니다. PFS 페이지는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 새로 삽입된 행을 보관할 수 있는 빈 공간이 있는 페이지를 찾아야 할 때 사용됩니다. 인덱스의 경우 새 행을 삽입할 지점이 인덱스 키 값에 의해 설정되므로 페이지의 빈 공간을 추적할 필요가 없습니다.

추적되는 각 추가 범위에 대한 새 PFS, GAM 또는 SGAM 페이지가 데이터 파일에 추가됩니다. 따라서 첫 번째 PFS 페이지 뒤에 8,088페이지의 새 PFS 페이지가 있고, 그다음에는 8,088페이지 간격으로 추가 PFS 페이지가 나옵니다. 즉, 페이지 ID 1이 PFS 페이지이고, 페이지 ID 8088이 PFS 페이지이며, 페이지 ID 16176이 PFS 페이지입니다. 첫 번째 GAM 페이지 뒤에 64,000개 익스텐트의 새 GAM 페이지가 있고, 그다음에 나오는 64,000개 익스텐트를 추적합니다. 64,000개 익스텐트 간격으로 시퀀스가 계속됩니다. 마찬가지로, 첫 번째 SGAM 페이지 뒤에 64,000개 익스텐트의 새 SGAM 페이지가 있고, 그다음에는 64,000개 익스텐트 간격으로 추가 SGAM 페이지가 나옵니다. 다음 그림은 익스텐트 할당 및 관리를 위해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 사용하는 페이지 순서를 보여 줍니다.

![manage_extents](../relational-databases/media/manage-extents.gif)

## <a name="managing-space-used-by-objects"></a>개체에서 사용하는 공간 관리 

**IAM(Index Allocation Map)** 페이지는 할당 단위에 사용되는 데이터베이스 파일의 4GB 부분에 익스텐트를 매핑합니다. 할당 단위의 유형은 다음 3가지가 있습니다.

- IN_ROW_DATA   
    힙 또는 인덱스의 파티션을 포함합니다.

- LOB_DATA   
   xml, varbinary(max), varchar(max) 같은 LOB(Large Object) 데이터 유형에 적용됩니다.

- ROW_OVERFLOW_DATA   
   varchar, nvarchar, varbinary 또는 sql_variant 열에 저장된 가변 길이 데이터 중 행 크기 제한인 8,060바이트를 초과하는 가변 길이 데이터에 적용됩니다. 

힙 또는 인덱스의 각 파티션에는 적어도 하나의 IN_ROW_DATA 할당 단위가 있습니다. 또한 힙 또는 인덱스 스키마에 따라 LOB_DATA 또는 ROW_OVERFLOW_DATA 할당 단위도 포함될 수 있습니다.

IAM 페이지는 파일에서 4GB 범위를 처리하며 이는 GAM 또는 SGAM 페이지와 동일합니다. 할당 단위에 하나 이상의 파일에서 매핑된 익스텐트가 포함되어 있거나 4GB를 넘는 파일 범위가 포함되어 있으면 하나의 IAM 체인에 여러 IAM 페이지가 연결됩니다. 따라서 각 할당 단위에는 익스텐트가 매핑된 각 파일에 대해 하나 이상의 IAM 페이지가 포함됩니다. 또한 할당 단위에 할당된 파일의 익스텐트 범위가 단일 IAM 페이지가 기록할 수 있는 범위를 초과하는 경우 파일에 IAM 페이지가 두 개 이상 있을 수 있습니다. 

![iam_pages](../relational-databases/media/iam-pages.gif)

IAM 페이지는 필요에 따라 각 할당 단위에 대해 할당되고 파일에서 임의의 위치에 배치됩니다. 시스템 뷰(sys.system_internals_allocation_units)는 할당 단위에 대한 첫 번째 IAM 페이지를 가리킵니다. 해당 할당 단위에 대한 모든 IAM 페이지는 체인으로 연결됩니다.

> [!IMPORTANT]
> `sys.system_internals_allocation_units` 시스템 뷰는 내부 전용이며 변경될 수 있습니다. 호환성은 보장되지 않습니다.

![iam_chain](../relational-databases/media/iam-chain.gif)
 
할당 단위별로 한 체인에 연결된 IAM 페이지 IAM 페이지에는 IAM 페이지에서 매핑하는 익스텐트 범위 중 시작 익스텐트를 표시하는 헤더가 있습니다. 또한 IAM 페이지는 각 비트가 하나의 익스텐트를 나타내는 대형 비트맵을 갖습니다. 맵의 첫째 비트는 범위의 첫째 익스텐트를 나타내고 둘째 비트는 둘째 익스텐트를 나타냅니다. 비트가 0인 경우 해당 익스텐트는 IAM을 소유하는 할당 단위에 할당되지 않은 것입니다. 비트가 1인 경우 해당 익스텐트는 IAM 페이지를 소유하는 할당 단위에 할당된 것입니다.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에서 새 행을 삽입해야 하는데 현재 페이지에 사용 가능한 공간이 없으면 IAM 및 PFS 페이지를 사용하여 할당할 페이지를 찾거나 힙 또는 텍스트/이미지 페이지의 경우 행을 보관하기에 충분한 공간이 있는 페이지를 찾습니다. [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 IAM 페이지를 사용하여 할당 단위에 할당된 익스텐트를 찾습니다. 각 익스텐트에 대해 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 PFS 페이지를 검색하여 사용할 수 있는 페이지가 있는지 확인합니다. 각 IAM 및 PFS 페이지는 많은 수의 데이터 페이지를 포함하므로 데이터베이스에는 IAM 및 PFS 페이지가 거의 없습니다. 이는 IAM 및 PFS 페이지가 대개 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버퍼 풀의 메모리에 있으므로 빠르게 검색할 수 있음을 의미합니다. 인덱스의 경우, 새 행의 삽입 지점은 인덱스 키로 설정되지만 새 페이지가 필요할 때 이전에 설명한 프로세스가 발생합니다.

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]은 삽입되는 행을 보관하기에 충분한 공간을 가진 기존 익스텐트에서 페이지를 빠르게 찾을 수 없을 때만 할당 단위에 새 익스텐트를 할당합니다. 

<a name="ProportionalFill"></a>[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]는 **비례 채우기 할당 알고리즘**을 사용하여 파일 그룹에서 사용할 수 있는 파일의 익스텐트를 할당합니다. 동일한 파일 그룹에 두 개의 파일이 있고 이 중 한 파일이 다른 파일에 비해 2배의 빈 공간을 가지는 경우 빈 공간이 더 많은 파일에서 두 페이지가 할당되고 빈 공간이 적은 다른 파일에서 한 페이지가 할당되는 방식으로 할당이 수행됩니다. 따라서 파일 그룹의 모든 파일이 유사한 공간 비율을 사용하게 됩니다. 

## <a name="tracking-modified-extents"></a>수정된 익스텐트 추적 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 두 개의 내부 데이터 구조를 사용하여 대량 복사 작업에 의해 수정된 익스텐트와 마지막 전체 백업 이후에 수정된 익스텐트를 추적할 수 있습니다. 이 두 데이터 구조를 사용하면 차등 백업의 속도가 크게 향상됩니다. 또한 데이터베이스가 대량 로그 복구 모델을 사용할 경우 대량 복사 작업의 로깅 속도도 향상됩니다. 이러한 구조들은 GAM(전역 할당 맵)과 SGAM(공유 전역 할당 맵) 페이지처럼 각 비트가 단일 익스텐트를 표시하는 비트맵에 해당합니다. 

- **DCM(차등 변경 맵)**    
   마지막 `BACKUP DATABASE` 문 이후에 변경된 익스텐트를 추적합니다. 익스텐트의 비트가 1인 경우 익스텐트는 마지막 `BACKUP DATABASE` 문 이후에 수정된 것입니다. 이 비트가 0인 경우 익스텐트는 수정되지 않은 것입니다. 차등 백업의 경우 DCM 페이지만 읽고도 어떤 익스텐트가 수정되었는지 알 수 있습니다. 이를 통해 차등 백업이 검색해야 하는 페이지의 수가 상당히 줄어듭니다. 차등 백업이 실행되는 시간의 길이는 데이터베이스의 전체 크기가 아니라 마지막 BACKUP DATABASE 문 이후에 수정된 익스텐트의 수에 비례합니다. 

- **BCM(대량 변경 맵)**    
   마지막 `BACKUP LOG` 문 이후에 대량 로그 작업에 의해 수정된 익스텐트를 추적합니다. 익스텐트의 비트가 1인 경우 익스텐트는 마지막 `BACKUP LOG` 문 이후에 대량 기록 작업에 의해 수정된 것입니다. 이 비트가 0인 경우 익스텐트는 대량 로그 작업에 의해 수정되지 않은 것입니다. BCM 페이지가 모든 데이터베이스에 표시되더라도 데이터베이스가 대량 로그 복구 모델을 사용할 때만 적절합니다. 이러한 복구 모델에서 `BACKUP LOG`가 수행되면 백업 프로세스는 수정된 익스텐트의 BCM을 검색하고 이런 익스텐트를 로그 백업에 포함시킵니다. 따라서 데이터베이스가 데이터베이스 백업과 일련의 트랜잭션 로그 백업에서 복원될 경우 대량 로그 작업이 복구될 수 있습니다. 단순 복구 모델을 사용 중인 데이터베이스에서는 대량 로그 작업이 기록되지 않으므로 BCM 페이지가 적절하지 않습니다. 이 복구 모델은 대량 로그 작업을 전체 로그 작업으로 취급하므로 전체 복구 모델을 사용하는 데이터베이스에서도 BCM 페이지는 적절하지 않습니다. 

DCM 페이지와 BCM 페이지 사이의 간격은 GAM 페이지와 SGAM 페이지의 간격인 64,000개의 익스텐트와 동일합니다. DCM 및 BCM 페이지는 물리적 파일에서 GAM 및 SGAM 페이지의 뒤에 있습니다.

![special_page_order](../relational-databases/media/special-page-order.gif)

## <a name="see-also"></a>참고 항목
[sys.allocation_units &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)     
[힙&#40;클러스터형 인덱스가 없는 테이블&#41;](../relational-databases/indexes/heaps-tables-without-clustered-indexes.md#heap-structures)       
[페이지 읽기](../relational-databases/reading-pages.md)   
[페이지 쓰기](../relational-databases/writing-pages.md)   
