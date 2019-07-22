---
title: 계획 지침에 쿼리 힌트 연결 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 2131f796-6359-4f9e-9047-da0b3d4dedaf
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 3b9dd6793cc8b1c8dc43b72369c0c370ace36248
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985021"
---
# <a name="attach-query-hints-to-a-plan-guide"></a>계획 지침에 쿼리 힌트 연결
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  계획 지침에 모든 올바른 쿼리 힌트 조합을 사용할 수 있습니다. 계획 지침이 쿼리와 일치하면 컴파일 및 최적화하기 전에 계획 지침의 힌트 절에 지정된 OPTION 절이 쿼리에 추가됩니다. 계획 지침에 일치하는 쿼리에 이미 OPTION 절이 있으면 계획 지침에 지정된 쿼리 힌트가 쿼리에서 이를 대체합니다. 그러나 이미 OPTION 절이 있는 쿼리에 계획 지침을 일치시키려면 해당 쿼리 텍스트를 지정할 때 sp_create_plan_guide 문이 쿼리의 OPTION 절을 포함해야 합니다. 계획 지침에 지정한 힌트로 이미 쿼리에 있는 힌트를 대체하는 대신 계획 지침에 지정한 힌트를 이미 쿼리에 있는 힌트에 추가하려면 원래 힌트와 추가 힌트를 모두 계획 지침의 OPTION 절에 지정해야 합니다.  
  
> [!CAUTION]  
>  쿼리 힌트를 오용하는 계획 지침을 사용하면 컴파일, 실행 또는 성능 문제가 발생할 수 있습니다. 계획 지침은 숙련된 개발자와 데이터베이스 관리자만 사용해야 합니다.  
  
## <a name="common-query-hints-used-in-plan-guides"></a>계획 지침에 사용되는 일반적인 쿼리 힌트  
 계획 지침을 사용할 경우 도움이 되는 쿼리는 일반적으로 매개 변수 기반이며 매개 변수 값이 최악의 시나리오나 가장 대표적인 시나리오를 나타내지 않는 캐시된 쿼리 계획을 사용하므로 성능이 좋지 않을 수 있습니다. OPTIMIZE FOR 및 RECOMPILE 쿼리 힌트를 사용하면 이러한 문제를 해결할 수 있습니다. OPTIMIZE FOR는 쿼리가 최적화될 때 매개 변수에 특정 값을 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 지시합니다. RECOMPILE은 실행 후 쿼리 계획을 삭제하도록 서버에 지시하여 다음 번에 같은 쿼리를 실행할 때 쿼리 최적화 프로그램이 새로운 쿼리 계획을 다시 컴파일하도록 합니다. 예제를 보려면 [계획 지침](../../relational-databases/performance/plan-guides.md)을 참조하세요.  
  
 또한 INDEX, FORCESCAN 및 FORCESEEK 테이블 힌트를 쿼리 힌트로 지정할 수도 있습니다. 쿼리 힌트로 지정할 경우 이러한 힌트는 인라인 테이블이나 뷰 힌트처럼 동작합니다. INDEX 힌트는 쿼리 최적화 프로그램이 지정한 인덱스만 사용하여 참조된 테이블이나 뷰에 있는 데이터에 액세스하도록 합니다. FORCESEEK 힌트는 최적화 프로그램이 Index Seek 연산만 사용하여 참조된 테이블이나 뷰에 있는 데이터에 액세스하도록 합니다. 이러한 힌트는 추가 계획 지침 기능을 제공하며 계획 지침을 사용하는 쿼리의 최적화에 보다 많은 영향을 줄 수 있습니다.  
  
  
