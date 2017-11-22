---
title: "인덱스 속성 F1 도움말 | Microsoft 문서"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.swb.indexproperties.filter.f1
- sql13.swb.indexproperties.partitions.f1
- sql13.swb.indexproperties.general.f1
- sql13.swb.indexproperties.storage.f1
- sql13.swb.indexproperties.columns.f1
- sql13.swb.indexproperties.options.f1
- sql13.swb.indexproperties.spatial.f1
ms.assetid: 45efd81a-3796-4b04-b0cc-f3deec94c733
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7bf66d7aa47b9f15428b08943638dac0cd905fde
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="index-properties-f1-help"></a>인덱스 속성 F1 도움말
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 항목의 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 이용할 수 있는 다양한 인덱스 속성을 참조합니다.  
  
 **항목 내용:**  
  
 [인덱스 속성 일반 페이지](#General)  
  
 [(인덱스) 열 선택 대화 상자](#Columns)  
  
 [인덱스 속성 저장소 페이지](#Storage)  
  
 [인덱스 속성 공간 페이지](#Spatial)  
  
 [인덱스 속성 필터 페이지](#Filter)  
  
##  <a name="General"></a> 인덱스 속성 일반 페이지  
 일반 페이지를 사용하여 선택한 테이블 또는 뷰의 인덱스 속성을 확인하거나 수정할 수 있습니다. 각 페이지의 옵션은 선택하는 인덱스의 유형에 따라 변경될 수 있습니다.  
  
 **테이블 이름**  
 인덱스가 생성된 테이블 또는 뷰의 이름을 표시합니다. 이 필드는 읽기 전용입니다. 다른 테이블을 선택하려면 인덱스 속성 페이지를 닫고 올바른 테이블을 선택한 다음 인덱스 속성 페이지를 다시 엽니다.  
  
 공간 인덱스는 인덱싱된 뷰에 지정할 수 없습니다. 공간 인덱스는 기본 키가 있는 테이블에 대해서만 정의할 수 있습니다. 테이블의 최대 기본 키 열 수는 15개입니다. 기본 키 열의 결합된 행별 크기는 최대 895바이트로 제한됩니다.  
  
 **인덱스 이름**  
 인덱스 이름을 표시합니다. 기존 인덱스의 경우 이 필드는 읽기 전용입니다. 새 인덱스를 만드는 중이면 인덱스 이름을 입력합니다.  
  
 **인덱스 유형**  
 인덱스의 유형을 나타냅니다. 새 인덱스의 경우 대화 상자를 열 때 선택한 인덱스의 유형을 나타냅니다. 인덱스는 **클러스터형**, **비클러스터형**, **기본 XML**, **보조 XML**, **공간**, **클러스터형 Columnstore**또는 **비클러스터형 Columnstore**일 수 있습니다.  
  
 **참고** 각 테이블에 대해 클러스터형 인덱스는 하나만 허용됩니다. 각 테이블에 대해 xVelocity 메모리 액세스에 최적화된 columnstore 인덱스는 하나만 허용됩니다.  
  
 **고유**  
 이 확인란을 선택하면 인덱스가 고유해집니다. 두 행의 인덱스 값이 같을 수 없습니다. 이 확인란은 기본적으로 선택되어 있지 않습니다. 기존 인덱스를 수정할 때 두 행의 값이 같으면 인덱스 만들기에 실패하게 됩니다. Null이 허용되는 열에서 고유한 인덱스는 하나의 Null 값을 허용합니다.  
  
 **인덱스 유형** 필드에서 **공간** 을 선택하면 **고유** 확인란이 흐리게 표시됩니다.  
  
 **인덱스 키 열**  
 **인덱스 키 열** 표에 원하는 열을 추가합니다. 여러 열을 추가할 때는 원하는 순서대로 열을 나열해야 합니다. 인덱스의 열 순서는 인덱스 성능에 큰 영향을 미칠 수 있습니다.  
  
 16개 이하의 열만 단일 복합 인덱스에 참여할 수 있습니다. 열이 17개 이상인 경우에는 이 항목의 마지막 부분에 있는 "포괄 열"을 참조하세요.  
  
 공간 인덱스는 공간 데이터 형식이 포함되어 있는 단일 열( *공간 열*)에 대해서만 정의할 수 있습니다.  
  
 **이름**  
 인덱스 키에 참여하는 열 이름을 표시합니다.  
  
 **정렬 순서**  
 선택한 인덱스 열의 정렬 방향( **오름차순** 또는 **내림차순**)을 지정합니다.  
  
> [!NOTE]  
>  인덱스 유형이 **기본 XML** 또는 **공간**인 경우에는 테이블에 이 열이 나타나지 않습니다.  
  
 **데이터 형식**  
 데이터 형식 정보를 표시합니다.  
  
> [!NOTE]  
>  테이블 열이 계산 열인 경우에는 **데이터 형식** 에 "계산 열"이 표시됩니다.  
  
 **크기**  
 열 데이터 형식을 저장하는 데 필요한 최대 바이트 수를 표시합니다. 공간 또는 XML 열의 경우에는 0이 표시됩니다.  
  
 **ID**  
 인덱스 키에 참여하는 열이 ID 열인지 여부를 나타냅니다.  
  
 **NULL 허용**  
 인덱스 키에 참여하는 열이 테이블 또는 뷰 열에 NULL 값을 저장하도록 허용할지 여부를 나타냅니다.  
  
 **추가**  
 인덱스 키에 열을 추가합니다. **추가**를 클릭하면 나타나는 *\<테이블 이름>***에서 열 선택** 대화 상자에서 테이블 열을 선택합니다. 공간 인덱스의 경우 열을 하나 선택하면 이 단추가 흐리게 표시됩니다.  
  
 **제거**  
 선택된 열을 인덱스 키에 참여하는 열에서 제거합니다.  
  
 **위로 이동**  
 인덱스 키 표에서 선택된 열을 위로 이동합니다.  
  
 **아래로 이동**  
 인덱스 키 표에서 선택된 열을 아래로 이동합니다.  
  
 **Columnstore 열**  
 **추가** 를 클릭하여 columnstore 인덱스의 열을 선택합니다. columnstore 인덱스에 대한 제한 사항은 [CREATE COLUMNSTORE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)를 참조하세요.  
  
 **포괄 열**  
 비클러스터형 인덱스에 키가 아닌 열을 포함합니다. 이 옵션을 사용하면 비클러스터형 인덱스의 리프 수준에 열을 추가할 때 키가 아닌 열로 추가하여 인덱스 키의 전체 크기 및 인덱스 키에 포함되는 최대 열 수에 대한 제한을 무시할 수 있습니다. 자세한 내용은 [포괄 열을 사용하여 인덱스 만들기](../../relational-databases/indexes/create-indexes-with-included-columns.md)를 참조하세요.  
  
##  <a name="Columns"></a> (인덱스) 열 선택 대화 상자  
 인덱스를 만들거나 수정할 때 이 페이지를 사용하여 **인덱스 속성 일반** 페이지에 열을 추가할 수 있습니다.  
  
 **확인란**  
 열을 추가하려면 선택합니다.  
  
 **이름**  
 열의 이름입니다.  
  
 **데이터 형식**  
 열의 데이터 형식입니다.  
  
 **바이트**  
 열의 크기를 바이트 단위로 표시한 것입니다.  
  
 **ID**  
 ID 열인 경우 **예** 를 표시하고 ID 열이 아닌 경우 **아니요** 를 표시합니다.  
  
 **Allow Nulls**  
 테이블 정의에 따라 열에 Null 값이 허용되는 경우 **예** 를 표시합니다. 테이블 정의에 따라 열에 Null 값이 허용되지 않는 경우 **아니요** 를 표시합니다.  
  
##  <a name="Storage"></a> 저장소 페이지 옵션  
 이 페이지를 사용하여 선택한 인덱스의 파일 그룹 또는 파티션 구성표 속성을 확인하거나 수정할 수 있습니다. 인덱스 유형과 관련된 옵션만 표시됩니다.  
  
 **파일 그룹**  
 지정한 파일 그룹에 인덱스를 저장합니다. 목록에는 표준(행) 파일 그룹만 표시됩니다. 목록에서는 기본적으로 데이터베이스의 PRIMARY 파일 그룹이 선택됩니다. 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하세요.  
  
 **Filestream 파일 그룹**  
 FILESTREAM 데이터의 파일 그룹을 지정합니다. 이 목록에는 FILESTREAM 파일 그룹만 표시됩니다. 목록에서는 기본적으로 PRIMARY FILESTREAM 파일 그룹이 선택됩니다. 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
 **파티션 구성표**  
 파티션 구성표에 인덱스를 저장합니다. **파티션 구성표** 를 클릭하면 아래의 표가 활성화됩니다. 목록에서는 기본적으로 테이블 데이터를 저장하는 데 사용되는 파티션 구성표가 선택됩니다. 목록에서 다른 파티션 구성표를 선택하면 표의 정보가 업데이트됩니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.  
  
 데이터베이스에 파티션 구성표가 없으면 파티션 구성표 옵션을 사용할 수 없습니다.  
  
 **Filestream 파티션 구성표**  
 FILESTREAM 데이터의 파티션 구성표를 지정합니다. 이 파티션 구성표는 **파티션 구성표** 옵션에서 지정한 구성표와 대칭이어야 합니다.  
  
 테이블이 분할되지 않은 경우 이 필드가 비어 있습니다.  
  
 **파티션 구성표 매개 변수**  
 파티션 구성표에 포함되는 열의 이름을 표시합니다.  
  
 **테이블 열**  
 파티션 구성표에 매핑할 테이블 또는 뷰를 선택합니다.  
  
 **열 데이터 형식**  
 열의 데이터 형식을 표시합니다.  
  
> [!NOTE]  
>  테이블 열이 계산 열이면 **열 데이터 형식** 에 "계산 열"이 표시됩니다.  
  
 **인덱스를 이동하는 동안 DML 문의 온라인 처리 허용**  
 이 옵션을 사용하면 사용자는 인덱스 작업 중에 기본 테이블이나 클러스터형 인덱스 데이터 및 연관된 모든 비클러스터형 인덱스에 액세스할 수 있습니다. 자세한 내용은 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.  
  
> [!NOTE]  
>  이 옵션은 XML 인덱스에 대해서는 사용할 수 없으며 인덱스가 비활성화된 클러스터형 인덱스인 경우에도 사용할 수 없습니다.  
  
 **최대 병렬 처리 수준 설정**  
 병렬 계획 실행 중 사용할 프로세서 수를 제한합니다. 기본값인 0으로 설정하면 사용 가능한 실제 CPU 수를 사용합니다. 값을 1로 설정하면 병렬 계획이 생성되지 않습니다. 값을 1보다 큰 값으로 설정하면 단일 쿼리 실행에서 사용하는 최대 프로세서 수가 제한됩니다. 이 옵션은 대화 상자가 **다시 작성** 또는 **다시 만들기** 상태에 있을 때만 사용할 수 있습니다. 자세한 내용은 [Set the Max Degree of Parallelism Option for Optimal Performance](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)을 참조하세요.  
  
> [!NOTE]  
>  사용 가능한 CPU 수보다 더 큰 수를 지정하면 사용 가능한 실제 CPU 수가 사용됩니다.  
  
##  <a name="Spatial"></a> 공간 페이지 인덱스 옵션  
 **공간** 페이지를 사용하여 공간 속성의 값을 확인하거나 지정할 수 있습니다. 자세한 내용은 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)을 참조하세요.  
  
### <a name="bounding-box"></a>경계 상자  
 *경계 상자* 는 기하 평면에서 최상위 표의 경계입니다. 경계 상자 매개 변수는 기하 도형 표 공간 분할에서만 존재합니다. 이러한 매개 변수는 **공간 분할(tessellation) 구성표** 가 **지리 표**인 경우 사용할 수 없습니다.  
  
 패널에는 경계 상자의 **(***X-min***,***Y-min***)** 및 **(***X-max***,***Y-max***)** 좌표가 표시됩니다. 기본 좌표 값은 없습니다. 따라서 **geometry** 유형 열에 새 공간 인덱스를 만드는 경우 좌표 값을 지정해야 합니다.  
  
 **X-min**  
 경계 상자의 왼쪽 아래 모퉁이의 X 좌표입니다.  
  
 **Y-min**  
 경계 상자의 왼쪽 아래 모퉁이의 Y 좌표입니다.  
  
 **X-max**  
 경계 상자의 오른쪽 위 모퉁이의 X 좌표입니다.  
  
 **Y-max**  
 경계 상자의 오른쪽 위 모퉁이의 Y 좌표입니다.  
  
### <a name="general"></a>일반  
 **공간 분할(tessellation) 구성표**  
 인덱스의 공간 분할(tessellation) 구성표를 나타냅니다. 지원되는 공간 분할(tessellation) 구성표는 다음과 같습니다.  
  
 **기하 도형 표**  
 **geometry** 데이터 형식의 열에 적용되는 기하 도형 표 공간 분할(tessellation) 구성표를 지정합니다.  
  
 **기하 도형 자동 표**  
 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 호환성 수준이 110 이상으로 설정된 경우에 사용할 수 있습니다.  
  
 **지리 표**  
 **geography** 데이터 형식의 열에 적용되는 지리 표 공간 분할(tessellation) 구성표를 지정합니다.  
  
 **지리 자동 표**  
 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 호환성 수준이 110 이상으로 설정된 경우에 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 공간 분할을 구현하는 방법은 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)를 참조하세요.  
  
 **개체당 셀 수**  
 인덱스의 단일 공간 개체에 사용할 수 있는 개체당 공간 분할(tessellation) 셀 수를 나타냅니다. 이 수는 1과 8192(포함) 사이의 정수일 수 있습니다. 기본값은 16이며, 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 호환성 수준이 110 이상으로 설정된 경우에는 8입니다.  
  
 최상위 수준에서, 개체가 *n*으로 지정된 셀보다 많은 셀을 포함하는 경우 인덱싱 시 전체 최상위 수준 공간 분할을 제공하는 데 필요한 만큼의 셀 수를 사용합니다. 이 경우 개체는 지정된 셀 수보다 많은 수의 셀을 받을 수 있습니다. 여기서 최대 수는 최상위 표에 의해 생성된 셀의 개수로, **수준 1** 밀도에 따라 달라집니다.  
  
### <a name="grids"></a>표  
 이 패널에는 각 공간 분할(tessellation) 구성표 수준에서 표의 밀도가 표시됩니다. 밀도는 **낮음**, **보통**또는 **높음**으로 지정됩니다. 기본값은 **보통**입니다. **낮음** 은 4x4 표(16개의 셀), **보통** 은 8x8 표(64개의 셀), **높음** 은 16x16 표(256개의 셀)를 나타냅니다. **기하 도형 자동 표** 또는 **지리 자동 표** 공간 분할 옵션을 선택한 경우에는 이러한 옵션을 사용할 수 없습니다.  
  
 **수준 1**  
 첫째 수준(최상위) 표의 밀도입니다.  
  
 **수준 2**  
 둘째 수준 표의 밀도입니다.  
  
 **수준 3**  
 셋째 수준 표의 밀도입니다.  
  
 **수준 4**  
 넷째 수준 표의 밀도입니다.  
  
##  <a name="Filter"></a> 필터 페이지  
 이 페이지를 사용하여 필터링된 인덱스에 대한 필터 조건자를 입력할 수 있습니다. 자세한 내용은 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)을(를) 참조하세요.  
  
 **필터 식**  
 필터링된 인덱스에 포함할 데이터 행을 정의합니다. 예를 들면 다음과 같습니다. `StartDate > '20000101' AND EndDate IS NOT NULL'.`  
  
## <a name="see-also"></a>참고 항목  
 [인덱스 옵션 설정](../../relational-databases/indexes/set-index-options.md)   
 [INDEXPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
