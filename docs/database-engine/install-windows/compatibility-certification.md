---
title: 호환성 인증 | Microsoft Docs
description: 호환성 인증은 애플리케이션 호환성의 위험을 해소하여 온-프레미스와 클라우드에서 SQL Server 데이터베이스를 업그레이드할 수 있도록 합니다.
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
- Databases [SQL Server], upgrading
- Database Engine [SQL Server], upgrading
- compatibility [SQL Server], certification
- compatibility level [SQL Server], upgrades
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433856
author: pmasl
ms.author: pelopes
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: b1505d27dfa186999d1730eece740b711d87ae0e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85659663"
---
# <a name="compatibility-certification"></a>호환성 인증

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

호환성 인증을 통해 기업은 클라우드 및 에지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 온-프레미스를 업그레이드하고 현대화하여 애플리케이션 호환성 위험을 제거할 수 있습니다. 

동일한 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)](Managed Instance)를 모두 구동합니다. 이 공유된 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]는 사용자 데이터베이스를 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 간에 원활하게 이동할 수 있고, [!INCLUDE[tsql](../../includes/tsql-md.md)]처럼 데이터베이스에서 실행되는 애플리케이션 코드가 원본 시스템에 있는 것처럼 계속 작동한다는 것을 의미합니다.

각 새로운 릴리스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 경우 기본 호환성 수준은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 버전으로 설정됩니다. 그러나 이전 버전의 호환성 수준은 기존 애플리케이션의 호환성을 위해 유지됩니다. 이 호환성 매트릭스는 [여기](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats)에서 볼 수 있습니다.
따라서 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 작동하도록 인증된 애플리케이션은 실제로 해당 버전의 기본 호환성 수준에서 작동하도록 인증되었습니다.

예를 들어 데이터베이스 호환성 수준 130은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 기본값이었습니다. 호환성 수준은 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능 및 쿼리 최적화 동작을 강제하기 때문에 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에 작동하도록 인증된 데이터베이스는 데이터베이스 호환성 수준 130에서 암시적으로 인증되었습니다. 데이터베이스 호환성 수준이 130으로 유지되는 한, 이 데이터베이스는 좀 더 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](예: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]에서 그대로 작동할 수 있습니다. 

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 연속 통합 작업 모델의 기본 원칙입니다. [!INCLUDE[ssde_md](../../includes/ssde_md.md)]은 Azure에서 지속적으로 개선되고 업그레이드되지만 기존 데이터베이스는 현재 호환성 수준을 유지하기 때문에 기본 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]으로 업그레이드한 후에도 설계된 대로 계속 작동합니다. 

## <a name="managing-upgrade-risk-with-compatibility-certification"></a>호환성 인증으로 업그레이드 위험 관리
호환성 인증을 사용하는 것은 데이터베이스 현대화의 중요한 접근 방식입니다. 호환성 수준을 기반으로 한 인증을 통해 개발자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]에서 지원되는 애플리케이션에 대한 기술 요구 사항을 설정하지만, 데이터베이스 플랫폼 수명 주기와 애플리케이션 수명 주기를 분리합니다. 이렇게 하면 회사는 수명 주기 정책에 따라 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 업그레이드된 상태를 유지할 뿐만 아니라 코드에 종속되지 않는 새로운 확장성 및 성능 향상 기능을 활용하고, 애플리케이션 연결은 업그레이드를 통해 **기능 상태를 유지합니다**.

기능 및 성능에 부정적인 영향을 미칠 가능성은 모든 업그레이드의 주요 위험 요소입니다. 호환성 인증은 이러한 업그레이드 위험을 관리하는 측면에서 안심할 수 있음을 나타냅니다.

-  [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작과 관련하여 변경 사항이 있을 경우 정확성을 위해 애플리케이션을 재인증해야 함을 의미합니다. 그러나, [데이터베이스 호환성 수준 설정](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)은 전체 서버가 아닌 지정된 데이터베이스에 대해서만 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과의 호환성을 제공합니다. 데이터베이스 호환성 수준을 그대로 유지하면 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 업그레이드 전후에 기존 애플리케이션 쿼리가 동일한 동작을 계속 표시하게 할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작 및 호환성 수준에 대한 자세한 내용은 [이전 버전과의 호환성을 위해 호환성 수준 사용](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#backwardCompat)을 참조하세요.

-  성능에 관련된 사항에서는 모든 버전에서 쿼리 최적화 프로그램의 향상된 기능을 도입하기 때문에 다른 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 버전 간에 쿼리 계획의 차이가 발생할 수 있습니다. 업그레이드 범위에서 쿼리 계획의 차이점은 일반적으로 특정 쿼리 또는 작업에 부정적인 변화가 있을 수 있는 경우 위험으로 변환됩니다. 결과적으로 업그레이드를 지연하고 수명 주기 및 지원 문제를 일으킬 수 있는 이 위험 때문에 재인증을 해야 합니다. 
   업그레이드 위험을 완화하기 위해서 쿼리 최적화 프로그램의 향상된 기능이 새 릴리스의 기본 호환성 수준으로 제어되는 것입니다(즉, 새 버전에 대해 가장 높은 호환성 수준 사용 가능). 호환성 인증에는 **쿼리 계획 셰이프 보호**가 포함되어 있습니다. 이것은 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 업그레이드 직후에 데이터베이스 호환성 수준을 그대로 유지하면 업그레이드 이전처럼 새 버전에서 동일한 쿼리 최적화 모델이 사용되고 쿼리 계획 셰이프가 변경되지 않는다는 개념입니다. 
   자세한 내용은 이 문서의 [쿼리 계획 셰이프를 사용하는 이유](#queryplan_shape) 섹션을 참조하세요.
   
호환성 수준에 대한 자세한 내용은 [이전 버전과의 호환성을 위해 호환성 수준 사용](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#backwardCompat)을 참조하세요.
   
애플리케이션이 상위 데이터베이스 호환성 수준에서만 사용 가능한 향상 기능을 사용할 필요가 없는 한, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]를 업그레이드하고 이전 데이터베이스 호환성 수준을 유지하는 것이 유효한 접근법이며, 애플리케이션을 다시 인증할 필요가 없습니다. 자세한 내용은 이 문서의 뒷부분에 나오는 [호환성 수준 및 데이터베이스 엔진 업그레이드](#compatibility-levels-and-database-engine-upgrades)를 참조하세요.

새로운 개발 작업을 수행하는 경우 또는 기존 애플리케이션에 [지능형 쿼리 처리](../../relational-databases/performance/intelligent-query-processing.md) 및 새로운 [!INCLUDE[tsql](../../includes/tsql-md.md)]와 같은 새 기능을 사용해야 하는 경우 데이터베이스 호환성 수준을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용 가능한 최신 수준으로 업그레이드하고, 애플리케이션이 해당 호환성 수준과 함께 작동함을 인증하세요. 데이터베이스 호환성 수준을 업그레이드하는 방법에 대한 자세한 내용은 [데이터베이스 호환성 수준 업그레이드에 대한 모범 사례](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)를 참조하세요.
   
### <a name="why-query-plan-shape"></a><a name="queryplan_shape"></a> 쿼리 계획 셰이프를 사용하는 이유      
쿼리 계획 셰이프는 쿼리 계획을 구성하는 다양한 연산자의 시각적 표시를 나타냅니다. 여기에는 검색, 검사, 조인, 정렬 등의 연산자와 데이터 흐름을 나타내는 연산자 간 연결, 의도한 결과 세트를 생성하기 위해 실행해야 하는 연산 순서가 포함됩니다. 쿼리 계획 셰이프는 쿼리 최적화 프로그램에서 결정됩니다.

업그레이드하는 동안 쿼리 성능을 예측 가능하게 유지하려면 기본적으로 동일한 쿼리 계획 셰이프를 사용해야 합니다. 이를 위해서는 기본 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]의 버전이 다르더라도 업그레이드 직후에 데이터베이스 호환성 수준을 변경하지 않아야 합니다. 사용 가능한 리소스 또는 기본 데이터의 데이터 분산 방식을 획기적으로 변경하는 경우처럼 쿼리 실행 에코시스템을 변경하지 않았다면 쿼리 성능이 변경되지 않은 상태로 유지됩니다. 

그러나 쿼리 계획 셰이프를 유지하는 것이 업그레이드 후 성능에 영향을 미치는 유일한 요인은 아닙니다. 데이터베이스를 최신 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]로 이동하고 환경적 측면을 변경할 경우 쿼리 계획이 버전 간에 동일한 셰이프를 유지하더라도 쿼리 성능에 즉각적으로 영향을 미칠 수 있습니다. 이러한 환경적 변화에는 어느 정도의 사용 가능한 메모리 및 CPU 리소스를 제공하는 새로운 [!INCLUDE[ssde_md](../../includes/ssde_md.md)], 서버 또는 데이터베이스 구성 옵션의 변경, 쿼리 계획을 만드는 방법에 영향을 주는 데이터 분산 방식의 변경 등이 포함될 수 있습니다. 이때문에 데이터베이스 호환성 수준을 유지할 경우 쿼리 계획 **셰이프**의 변경을 방지할 수 있지만, 쿼리 성능에 영향을 주는 사용자가 시작한 변경을 비롯한 기타 다른 환경적 측면에서는 보호를 제공할 수 없다는 사실을 이해하는 것이 중요합니다.

자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements)를 참조하세요.
   
## <a name="compatibility-certification-benefits"></a>호환성 인증 이점
명명된 버전 접근 방식이 아닌 호환성 기반 방법 방식의 데이터베이스 인증에는 다음과 같은 여러 가지 즉각적인 이점이 있습니다.

-  **애플리케이션 인증을 플랫폼에서 분리합니다**. 공유된 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]로 인해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행해야 하는 애플리케이션의 경우 Azure 및 온-프레미스에 대한 별도의 인증 프로세스를 유지할 필요가 없습니다.
-  데이터베이스 플랫폼 현대화를 수행하는 동안 애플리케이션 및 데이터베이스 플랫폼 계층 업그레이드 주기를 분리하여 중단을 줄이고 변경 관리를 향상할 수 있기 때문에 **업그레이드 위험이 감소합니다**.
-  **코드 변경 없이 업그레이드합니다**. 새 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]로의 업그레이드를 코드 변경 없이 원본 시스템과 동일한 호환성 수준을 유지하며 수행할 수 있고, 애플리케이션에서 더 높은 데이터베이스 호환성 수준에서만 사용할 수 있는 향상된 기능을 활용해야 할 때까지는 즉시 다시 인증할 필요가 없습니다.
- 애플리케이션의 변경이 필요 없고 데이터베이스 호환성 수준으로 제어되지 않는 향상된 기능을 사용하여 **관리 효율성 및 확장성을 향상시킵니다**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 예를 들면 다음과 같습니다. 
  - [시스템 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md), [확장 이벤트](../../relational-databases/extended-events/extended-events.md) 및 [자동 조정](../../relational-databases/automatic-tuning/automatic-tuning.md)을 통한 풍부한 모니터링 및 문제 해결 개선 사항입니다. 
  - [자동 Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)를 통해 확장성이 개선되었습니다.

새 데이터베이스는 여전히 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 버전의 기본 호환성 수준으로 설정됩니다. 하지만 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 버전으로 이동할 때 데이터베이스는 기존 호환성 수준을 유지합니다. 

> [!IMPORTANT]
> 데이터베이스를 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 버전으로 이동하기 전에 데이터베이스 호환성 수준이 여전히 지원되는지 확인합니다. 데이터베이스 호환성 수준 지원 매트릭스는 [여기](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#arguments)에서 볼 수 있습니다. 
>
> 허용된 수준보다 낮은 호환성 수준으로 데이터베이스를 업그레이드하면(예: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 기본값인 90) 데이터베이스를 허용된 가장 낮은 호환성 수준(100)으로 설정합니다.
>
> 현재 호환성 수준을 확인하려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)의 **compatibility_level** 열을 쿼리합니다.

## <a name="compatibility-levels-and-database-engine-upgrades"></a>호환성 수준 및 업그레이드 데이터베이스 엔진
업그레이드 이전의 데이터베이스 호환성 수준과 지원 가능성 상태를 유지하면서 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]을 최신 버전으로 업그레이드하려면 [DMA](https://www.microsoft.com/download/details.aspx?id=53595) 도구(Microsoft Data Migration Assistant)를 사용하여 데이터베이스(저장 프로시저, 함수, 트리거 등의 프로그래밍 기능 개체) 및 애플리케이션(애플리케이션에서 전송된 동적 코드를 캡처하는 워크로드 추적 사용)의 애플리케이션 코드에 대한 정적 기능 노출 영역 유효성 검사를 수행하는 것이 좋습니다. DMA 도구 출력에 누락되거나 호환되지 않는 기능에 대한 오류가 없는 경우 애플리케이션이 새로운 대상 버전의 기능 회귀로부터 보호됩니다. 자세한 내용은 [Data Migration Assistant 개요](../../dma/dma-overview.md)를 참조하세요.

> [!NOTE]
> DMA는 데이터베이스 호환성 수준 100 이상을 지원합니다. 원본 버전 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]는 제외됩니다.   

> [!IMPORTANT]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 업그레이드의 성공 여부를 확인하기 위해 최소한의 테스트를 수행하고, 이전의 데이터베이스 호환성 수준을 유지할 것을 권장합니다. 자신의 애플리케이션 및 시나리오에 의미 있는 최소한의 테스트를 결정해야 합니다.   

> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서는 다음과 같은 경우 쿼리 계획 셰이프 보호를 제공합니다.
>
> - 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전(대상)은 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전(원본)이 실행 중인 하드웨어와 유사한 하드웨어에서 실행됩니다.
> - 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모두에서 동일한 [지원 데이터베이스 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats)이 사용됩니다.
>
> 위의 조건에서 발생하는 모든 쿼리 계획 셰이프 회귀(원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기준)는 해결될 예정입니다. 이 경우 Microsoft 고객 지원팀에 문의하세요.
  
## <a name="see-also"></a>참고 항목 
[ALTER DATABASE 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)       
[데이터베이스의 호환성 수준 보기 또는 변경](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)       
[데이터베이스 호환성 수준 업그레이드 모범 사례](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)      
