---
title: hierarchyid (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44299e7ddb90bdd52e2638dd859993513bd6f966
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyid-data-type-method-reference"></a>hierarchyid 데이터 형식 메서드 참조
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**hierarchyid** 데이터 형식은 가변 길이의 시스템 데이터 형식입니다. 사용 하 여 **hierarchyid** 계층의 위치를 나타내는입니다. **hierarchyid** 형식의 열은 자동으로 트리를 나타내지 않습니다. 응용 프로그램에 따라 원하는 행 간 관계가 값에 반영되도록 **hierarchyid** 값이 생성되어 할당됩니다.
  
**hierarchyid** 데이터 형식의 값은 트리 계층에서의 위치를 나타냅니다. **hierarchyid** 값의 속성은 다음과 같습니다.
  
-   높은 압축성  
     포함 된 트리에서 노드를 나타내는 데 필요한 비트 수 평균  *n*  노드는 평균 fanout (노드의 자식 항목의 평균 수)에 따라 달라 집니다. 작은 fanout (0-7)의 크기는 약 6\*logA *n*  비트, 여기서 A는 평균 fanout입니다. 평균 fanout 수준이 6인 100,000명으로 구성된 조직 계층의 노드는 약 38비트를 사용합니다. 이는 저장을 위해 40비트나 5바이트로 반올림됩니다.  
-   깊이 우선 순서로 비교  
     두 개의 **hierarchyid** 값이 **a**와 **b**인 경우 **a<b**는 깊이 우선 트리 탐색에서 a가 b 앞에 온다는 의미입니다. **hierarchyid** 데이터 형식의 인덱스에는 깊이 우선 순서가 사용되며 깊이 우선 탐색에서 서로 가까이 있는 노드는 서로 가깝게 저장됩니다. 예를 들어 레코드의 자식은 해당 레코드에 인접하게 저장됩니다. 자세한 내용은 참조 [계층적 데이터 &#40; SQL Server &#41; ](../../relational-databases/hierarchical-data-sql-server.md).  
-   임의 삽입 및 삭제 지원  
     [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) 메서드를 사용하면 지정한 노드의 오른쪽, 지정한 노드의 왼쪽 또는 두 형제 사이에 형제를 생성할 수 있습니다. 임의 개수의 노드를 계층에서 삽입하거나 삭제할 때 비교 속성이 유지됩니다. 대부분의 삽입 및 삭제 시 압축성 속성이 유지됩니다. 그러나 두 노드 간 삽입 시에는 약간 덜 압축된 표현으로 hierarchyid 값이 생성됩니다.  
-   사용 되는 인코딩을 **hierarchyid** 형식 892 바이트로 제한 됩니다. 결과적으로 표현 892 바이트에 들어가지에 수준이 너무 많아 노드를 표현할 수 없는 **hierarchyid** 유형입니다.  
  
**hierarchyid** 형식은 CLR 클라이언트는 사용할 수는 **SqlHierarchyId** 데이터 형식입니다.
  
## <a name="remarks"></a>주의  
**hierarchyid** 형식 트리의 루트에서 노드까지의 경로 인코딩하여 계층 트리의 단일 노드에 대 한 정보를 논리적으로 인코딩합니다. 이러한 경로는 루트 이후 거친 모든 자식의 노드 레이블 시퀀스로 논리적으로 표현됩니다. 표현은 슬래시로 시작하며 루트만 거친 경로는 단일 슬래시로 표시됩니다. 루트 아래 수준의 경우 각 레이블은 마침표로 분리된 정수 시퀀스로 인코딩됩니다. 자식 간의 비교는 마침표로 분리된 정수 시퀀스를 사전 순서로 비교하여 수행됩니다. 각 수준 다음에는 슬래시가 사용됩니다. 즉, 슬래시가 부모와 자식을 분리합니다. 예를 들어 다음은 유효한 **hierarchyid** 길이 1, 2, 2, 3 및 3에 대 한 경로 각각 수준:
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
노드는 어느 위치에나 삽입할 수 있습니다. 노드 뒤에 삽입 **/1/2/** 하기 전에 **/1/3/** 으로 나타낼 수 **/1/2.5/**합니다. 0 앞에 삽입된 노드의 논리 표현은 음수입니다. 예를 들어 앞에 있는 노드 **/1/1/** 으로 나타낼 수 **/1/1 /**합니다. 노드에는 앞에 오는 0이 포함될 수 없습니다. 예를 들어 **/1/1.1/** 유효 하지만 **/1/1.01/** 올바르지 않습니다. 오류를 방지 하려면 노드를 사용 하 여 삽입 된 [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) 메서드.
  
## <a name="data-type-conversion"></a>데이터 형식 변환
**hierarchyid** 다음과 같이 데이터 형식은 다른 데이터 형식으로 변환 수 있습니다.
-   사용 하 여는 [tostring ()](../../t-sql/data-types/tostring-database-engine.md) 변환 하는 메서드는 **hierarchyid** 값을 논리적 표현으로는 **nvarchar (4000)** 데이터 형식입니다.  
-   사용 하 여 [()를 읽을](../../t-sql/data-types/read-database-engine.md) 및 [Write ()](../../t-sql/data-types/write-database-engine.md) 변환할 **hierarchyid** 를 **varbinary**합니다.  
-   전송할 **hierarchyid** SOAP 통해 매개 변수 먼저 문자열로 캐스팅 합니다.  
  
## <a name="upgrading-databases"></a>데이터베이스 업그레이드
데이터베이스를 업그레이드할 때 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 새 어셈블리 및 **hierarchyid** 데이터 형식을 자동으로 설치 됩니다. 업그레이드 관리자 규칙에서는 이름이 충돌하는 사용자 형식이나 어셈블리를 검색합니다. 업그레이드 관리자는 충돌하는 어셈블리의 이름을 변경할 것을 알려 주며, 충돌하는 형식의 이름을 변경하거나 코드에서 기존 사용자 형식을 참조할 수 있도록 두 부분으로 된 이름을 사용할 것을 알려 줍니다.
  
데이터베이스 업그레이드에서 이름이 충돌하는 사용자 어셈블리가 발견되면 해당 어셈블리의 이름이 자동으로 변경되고 데이터베이스가 주의 대상 모드로 설정됩니다.
  
업그레이드 중에 이름이 충돌하는 사용자 형식이 발견된 경우에는 특별한 조치가 취해지지 않습니다. 업그레이드 후에는 기존 사용자 형식과 새 시스템 형식이 모두 존재하게 됩니다. 사용자 형식은 두 부분으로 된 이름을 통해서만 사용할 수 있습니다.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>복제 된 테이블에서 hierarchyid 열 사용
형식의 열 **hierarchyid** 복제 된 모든 테이블에서 사용할 수 있습니다. 응용 프로그램의 요구 사항은 복제가 단방향인지 양방향인지, 사용된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전이 무엇인지에 따라 달라집니다.
  
### <a name="one-directional-replication"></a>단방향 복제
단방향 복제에는 변경 내용이 구독자에 적용되지 않는 병합 복제 및 스냅숏 복제, 트랜잭션 복제가 포함됩니다. 어떻게 **된 hierachyid** 열 하나를 사용 단방향 복제의 버전에 따라 달라 집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에서 실행 되 고 있습니다.
-   A [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 게시자를 복제 하려면 **된 hierachyid** 열을 한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 특별 한 고려 없이 구독자입니다.  
-   A [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 게시자로 변환 해야 **hierarchyid** 열을 실행 하는 구독자에 복제 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 또는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssEW](../../includes/ssew-md.md)]및 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 하지 않는 **hierarchyid** 열입니다. 이러한 버전 중 하나를 사용 중인 경우에도 데이터를 구독자로 복제할 수 있습니다. 이렇게 하려면 열을 호환되는 데이터 형식으로 변환할 수 있도록 스키마 옵션이나 게시 호환성 수준(병합 복제의 경우)을 설정해야 합니다.  
  
열 필터링은 이러한 두 가지 시나리오에서 모두 지원됩니다. 여기에 필터링 **hierarchyid** 열입니다. 행 필터링이 지원는 포함 되지 않는 상태로 **hierarchyid** 열입니다.
  
### <a name="bi-directional-replication"></a>양방향 복제
양방향 복제에는 변경 내용이 구독자에 적용되는 병합 복제와 구독이 업데이트되는 트랜잭션 복제, 피어 투 피어 트랜잭션 복제가 포함됩니다. 포함 된 테이블을 구성할 수 있습니다 **hierarchyid** 양방향 복제에 대 한 열입니다. 다음 요구 사항 및 고려 사항을 유의하세요.
-   게시자와 모든 구독자는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 실행해야 합니다.  
-   복제 기능은 데이터를 바이트로 복제하며 계층의 무결성을 보장하기 위한 유효성 검사는 수행하지 않습니다.  
-   원본(구독자 또는 게시자)에 수행된 변경의 계층은 대상에 복제될 때 유지되지 않습니다.  
-   에 대 한 해시 값 **hierarchyid** 열은 생성 된 데이터베이스에만 합니다. 따라서 게시자와 구독자에 동일한 값이 생성되더라도 서로 다른 행에 적용될 수 있습니다. 이 조건에 대 한 복제를 확인 하지 않습니다 되며 파티션 수 있는 기본 방법이 **hierarchyid** 열 값을 ID 열에 없기 때문입니다. 응용 프로그램에서는 제약 조건 또는 기타 메커니즘을 사용하여 이러한 감지되지 않는 충돌을 피해야 합니다.  
-   구독자에 삽입한 행이 분리되는 경우가 발생할 수 있습니다. 이는 삽입된 행의 부모가 게시자에서 삭제되었기 때문일 수 있습니다. 이렇게 되면 구독자의 행이 게시자에 삽입될 때 감지되지 않은 충돌이 발생합니다.  
-   열 필터 필터링 할 수 없습니다 nullable이 아닌 **hierarchyid** 열:에 대 한 기본값이 있기 때문에 구독자에서의 삽입은 실패는 **hierarchyid** 게시자에서 열.  
-   행 필터링이 지원는 포함 되지 않는 상태로 **hierarchyid** 열입니다.  
  
## <a name="see-also"></a>참고 항목
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

