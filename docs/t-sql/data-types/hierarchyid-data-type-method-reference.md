---
title: hierarchyid(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 122630048b7e4ff9cef34c49bfde68177020630f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68077907"
---
# <a name="hierarchyid-data-type-method-reference"></a>hierarchyid 데이터 형식 메서드 참조
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**hierarchyid** 데이터 형식은 가변 길이의 시스템 데이터 형식입니다. **hierarchyid**는 계층에서의 위치를 나타내는 데 사용됩니다. **hierarchyid** 형식의 열은 자동으로 트리를 나타내지 않습니다. 애플리케이션에 따라 원하는 행 간 관계가 값에 반영되도록 **hierarchyid** 값이 생성되어 할당됩니다.
  
**hierarchyid** 데이터 형식의 값은 트리 계층에서의 위치를 나타냅니다. **hierarchyid** 값의 속성은 다음과 같습니다.
  
-   높은 압축성  
     *n* 개 노드가 포함된 트리에서 노드를 나타내는 데 필요한 평균 비트 수는 평균 fanout(노드의 평균 자식 수)에 따라 달라집니다. 작은 fanout(0-7)의 경우 크기는 약 6\*logA*n* 비트입니다. 여기서 A는 평균 fanout입니다. 평균 fanout 수준이 6인 100,000명으로 구성된 조직 계층의 노드는 약 38비트를 사용합니다. 이는 스토리지를 위해 40비트나 5바이트로 반올림됩니다.  
-   깊이 우선 순서로 비교  
     두 개의 **hierarchyid** 값이 **a**와 **b**인 경우 **a<b**는 깊이 우선 트리 탐색에서 a가 b 앞에 온다는 의미입니다. **hierarchyid** 데이터 형식의 인덱스에는 깊이 우선 순서가 사용되며 깊이 우선 탐색에서 서로 가까이 있는 노드는 서로 가깝게 저장됩니다. 예를 들어 레코드의 자식은 해당 레코드에 인접하게 저장됩니다. 자세한 내용은 [계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)를 참조하세요.  
-   임의 삽입 및 삭제 지원  
     [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) 메서드를 사용하면 지정한 노드의 오른쪽, 지정한 노드의 왼쪽 또는 두 형제 사이에 형제를 생성할 수 있습니다. 임의 개수의 노드를 계층에서 삽입하거나 삭제할 때 비교 속성이 유지됩니다. 대부분의 삽입 및 삭제 시 압축성 속성이 유지됩니다. 그러나 두 노드 간 삽입 시에는 약간 덜 압축된 표현으로 hierarchyid 값이 생성됩니다.  
-   **hierarchyid** 형식에 사용되는 인코딩은 892바이트로 제한됩니다. 따라서 표현에 수준이 너무 많아 892바이트에 들어가지 못하는 노드는 **hierarchyid** 형식으로 나타낼 수 없습니다.  
  
**hierarchyid** 형식은 CLR 클라이언트에서 **SqlHierarchyId** 데이터 형식으로 사용할 수 있습니다.
  
## <a name="remarks"></a>설명  
**hierarchyid** 형식은 트리의 루트에서 노드까지의 경로를 인코딩하는 방법으로 계층 트리의 단일 노드에 대한 정보를 논리적으로 인코딩합니다. 이러한 경로는 루트 이후 거친 모든 자식의 노드 레이블 시퀀스로 논리적으로 표현됩니다. 표현은 슬래시로 시작하며 루트만 거친 경로는 단일 슬래시로 표시됩니다. 루트 아래 수준의 경우 각 레이블은 마침표로 분리된 정수 시퀀스로 인코딩됩니다. 자식 간의 비교는 마침표로 분리된 정수 시퀀스를 사전 순서로 비교하여 수행됩니다. 각 수준 다음에는 슬래시가 사용됩니다. 즉, 슬래시가 부모와 자식을 분리합니다. 예를 들어 다음은 길이가 각각 1, 2, 2, 3 및 3 수준인 유효한 **hierarchyid** 경로입니다.
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
노드는 어느 위치에나 삽입할 수 있습니다. **/1/2/** 와 **/1/3/** 사이에 삽입한 노드는 **/1/2.5/** 로 나타낼 수 있습니다. 0 앞에 삽입된 노드의 논리 표현은 음수입니다. 예를 들어 **/1/1/** 앞에 오는 노드는 **/1/-1/** 로 나타낼 수 있습니다. 노드에는 앞에 오는 0이 포함될 수 없습니다. 예를 들어 **/1/1.1/** 은 유효하지만 **/1/1.01/** 은 유효하지 않습니다. 오류가 발생하지 않도록 하려면 [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) 메서드를 사용하여 노드를 삽입합니다.
  
## <a name="data-type-conversion"></a>데이터 형식 변환
**hierarchyid** 데이터 형식은 다음과 같이 다른 데이터 형식으로 변환할 수 있습니다.
-   [ToString()](../../t-sql/data-types/tostring-database-engine.md) 메서드를 사용하여 **hierarchyid** 값을 **nvarchar(4000)** 데이터 형식의 논리 표현으로 변환할 수 있습니다.  
-   **hierarchyid**를 **varbinary**로 변환하려면 [Read ()](../../t-sql/data-types/read-database-engine.md) 및 [Write ()](../../t-sql/data-types/write-database-engine.md)를 사용합니다.  
-   SOAP를 통해 **hierarchyid** 매개 변수를 전송하려면 먼저 문자열로 캐스팅해야 합니다.  
  
## <a name="upgrading-databases"></a>데이터베이스 업그레이드
데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하면 새로운 어셈블리와 **hierarchyid** 데이터 형식이 자동으로 설치됩니다. 업그레이드 관리자 규칙에서는 이름이 충돌하는 사용자 형식이나 어셈블리를 검색합니다. 업그레이드 관리자는 충돌하는 어셈블리의 이름을 변경할 것을 알려 주며, 충돌하는 형식의 이름을 변경하거나 코드에서 기존 사용자 형식을 참조할 수 있도록 두 부분으로 된 이름을 사용할 것을 알려 줍니다.
  
데이터베이스 업그레이드에서 이름이 충돌하는 사용자 어셈블리가 발견되면 해당 어셈블리의 이름이 자동으로 변경되고 데이터베이스가 주의 대상 모드로 설정됩니다.
  
업그레이드 중에 이름이 충돌하는 사용자 형식이 발견된 경우에는 특별한 조치가 취해지지 않습니다. 업그레이드 후에는 기존 사용자 형식과 새 시스템 형식이 모두 존재하게 됩니다. 사용자 형식은 두 부분으로 된 이름을 통해서만 사용할 수 있습니다.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>복제된 테이블에서 hierarchyid 열 사용
**hierarchyid** 형식의 열은 복제된 모든 테이블에서 사용할 수 있습니다. 애플리케이션의 요구 사항은 복제가 단방향인지 양방향인지, 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전이 무엇인지에 따라 달라집니다.
  
### <a name="one-directional-replication"></a>단방향 복제
단방향 복제에는 변경 내용이 구독자에 적용되지 않는 병합 복제 및 스냅샷 복제, 트랜잭션 복제가 포함됩니다. **hierarchyid** 열이 단방향 복제에서 어떻게 작동하는지는 구독자가 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 달라집니다.
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 게시자는 특별히 고려할 사항 없이 **hierarchyid** 열을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 구독자에 복제할 수 있습니다.  
-   [!INCLUDE[ssEW](../../includes/ssew-md.md)] 또는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 구독자에게 **hierarchyid** 열을 복제하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 게시자는 이러한 열을 변환해야 합니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)] 및 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **hierarchyid** 열이 지원되지 않습니다. 이러한 버전 중 하나를 사용 중인 경우에도 데이터를 구독자로 복제할 수 있습니다. 이렇게 하려면 열을 호환되는 데이터 형식으로 변환할 수 있도록 스키마 옵션이나 게시 호환성 수준(병합 복제의 경우)을 설정해야 합니다.  
  
열 필터링은 이러한 두 가지 시나리오에서 모두 지원됩니다. 여기에는 **hierarchyid** 열 필터링도 포함됩니다. 행 필터링은 필터에 **hierarchyid** 열이 포함되어 있지 않은 경우에 한해 지원됩니다.
  
### <a name="bi-directional-replication"></a>양방향 복제
양방향 복제에는 변경 내용이 구독자에 적용되는 병합 복제와 구독이 업데이트되는 트랜잭션 복제, 피어 투 피어 트랜잭션 복제가 포함됩니다. **hierarchyid** 열이 있는 테이블을 양방향 복제에 맞게 구성할 수 있습니다. 다음 요구 사항 및 고려 사항을 유의하세요.
-   게시자와 모든 구독자는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 실행해야 합니다.  
-   복제 기능은 데이터를 바이트로 복제하며 계층의 무결성을 보장하기 위한 유효성 검사는 수행하지 않습니다.  
-   원본(구독자 또는 게시자)에 수행된 변경의 계층은 대상에 복제될 때 유지되지 않습니다.  
-   **hierarchyid** 열의 해시 값은 해당 값이 생성된 데이터베이스에 한정됩니다. 따라서 게시자와 구독자에 동일한 값이 생성되더라도 서로 다른 행에 적용될 수 있습니다. 복제 기능은 이러한 상황을 확인하지 않으며 IDENTITY 열과 같이 **hierarchyid** 열을 분할하는 방법은 기본적으로 제공되지 않습니다. 애플리케이션에서는 제약 조건 또는 기타 메커니즘을 사용하여 이러한 감지되지 않는 충돌을 피해야 합니다.  
-   구독자에 삽입한 행이 분리되는 경우가 발생할 수 있습니다. 이는 삽입된 행의 부모가 게시자에서 삭제되었기 때문일 수 있습니다. 이렇게 되면 구독자의 행이 게시자에 삽입될 때 감지되지 않은 충돌이 발생합니다.  
-   열 필터는 Null을 허용하지 않는 **hierarchyid** 열을 필터링할 수 없습니다. 게시자의 **hierarchyid** 열에 대한 기본값이 없기 때문에 구독자에서의 삽입은 실패합니다.  
-   행 필터링은 필터에 **hierarchyid** 열이 포함되어 있지 않은 경우에 한해 지원됩니다.  
  
## <a name="see-also"></a>참고 항목
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid 데이터 형식 메서드 참조](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
