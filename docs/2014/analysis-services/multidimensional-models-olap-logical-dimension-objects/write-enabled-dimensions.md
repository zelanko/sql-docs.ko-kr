---
title: 쓰기 가능 차원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- write-enabled dimensions [Analysis Services]
- dimensions [Analysis Services], write-enabled
- dimension writeback [Analysis Services]
- write-enabled cubes [Analysis Services]
- writeback [Analysis Services], dimensions
ms.assetid: 0bac050d-cd3b-427b-884a-65a91be89500
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bf87518328e036b69dfc8596ec239b4770c1edab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225133"
---
# <a name="write-enabled-dimensions"></a>쓰기 가능 차원
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 차원의 데이터는 일반적으로 읽기 전용입니다. 그러나 특정 시나리오에 대한 차원을 쓰기 가능으로 설정할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 차원을 쓰기 가능으로 설정하면 업무용 사용자가 차원의 내용을 수정하고 변경 내용이 차원 계층에 미치는 직접적인 영향을 확인할 수 있습니다. 단일 테이블을 기반으로 하는 모든 차원을 쓰기 가능으로 설정할 수 있습니다. 쓰기 가능한 차원에서는 비즈니스 사용자와 관리자가 차원 내의 특성 멤버를 변경, 이동, 추가 및 삭제할 수 있습니다. 이러한 업데이트는 *차원 쓰기 저장(writeback)* 으로 통칭됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 모든 차원 특성에서 차원 쓰기 저장을 지원하며 차원의 멤버는 수정될 수 있습니다. 쓰기 가능 큐브 또는 파티션의 경우 업데이트 내용이 큐브의 원본 테이블과는 별개의 쓰기 저장 테이블에 저장됩니다. 그러나 쓰기 가능 차원의 경우에는 업데이트 내용이 차원 테이블에 직접 기록됩니다. 또한 쓰기 가능 차원이 여러 파티션으로 구성된 큐브에 포함되어 있고 파티션의 전체 또는 일부 데이터 원본에 차원 테이블의 복사본이 있는 경우 쓰기 저장 과정에서 원본 차원 테이블만 업데이트됩니다.  
  
 쓰기 가능 차원과 쓰기 가능 큐브에는 서로 다르지만 상호 보완되는 기능이 있습니다. 쓰기 가능 차원은 업무용 사용자에게 멤버를 업데이트할 수 있는 기능을 제공하고 쓰기 가능 큐브는 셀 값을 업데이트할 수 있는 기능을 제공합니다. 이 두 기능은 상호 보완적이지만 두 기능을 함께 사용할 필요는 없습니다. 차원이 큐브에 포함되어 있어야 차원 쓰기 저장이 가능한 것은 아닙니다. 쓰기 가능 차원이 쓰기 가능하지 않은 큐브에 포함될 수도 있습니다. 차원과 큐브를 쓰기 가능으로 설정하는 작업과 보안을 유지하는 작업의 절차는 다릅니다.  
  
 다음은 차원 쓰기 저장(writeback)에 적용되는 제한 사항입니다.  
  
-   새 멤버를 만들 때 차원에 모든 특성을 포함해야 합니다. 차원의 키 특성 값을 지정하지 않고 멤버를 삽입할 수 없습니다. 따라서 멤버를 만들 때는 차원 테이블에 정의된 모든 제약 조건(예: Null이 아닌 키 값)이 적용됩니다.  
  
-   차원 쓰기 저장은 별모양 스키마에 대해서만 지원됩니다. 즉, 차원이 팩트 테이블과 직접 관련된 단일 차원 테이블을 기반으로 해야 합니다. 차원을 쓰기 가능으로 설정하면 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 배포하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 빌드할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 이 요구 사항이 유효한지 검사합니다.  
  
 쓰기 저장 차원의 기존 멤버는 수정하거나 삭제할 수 있습니다. 멤버를 삭제하면 모든 자식 멤버도 삭제됩니다. 예를 들어 CountryRegion, Province, City 및 Customer 특성을 포함하는 Customer 차원에서 Country/Region을 삭제하면 이 Country/Region에 속하는 모든 Province, City 및 Customer가 삭제됩니다. Country/Region에 Province가 하나만 있는 경우 이 Province를 삭제하면 Country/Region도 삭제됩니다.  
  
 쓰기 저장 차원의 멤버는 같은 수준 내에서만 이동 가능합니다. 예를 들어 City를 다른 Country/Region이나 Province의 City 수준으로 이동할 수 있지만 Province나 CountryRegion 수준으로 이동할 수는 없습니다. 부모-자식 계층에서는 모든 멤버가 리프 멤버이므로 `(All)` 수준이 아닌 모든 수준으로 멤버를 이동할 수 있습니다.  
  
 부모-자식 계층의 멤버를 삭제하면 해당 멤버의 자식이 멤버의 부모로 이동됩니다. 삭제된 멤버에는 관계형 테이블에 대한 업데이트 권한이 필요하지만 이동된 멤버에는 아무 권한도 필요하지 않습니다. 응용 프로그램에서 부모-자식 계층의 멤버를 이동할 때 하위 항목을 멤버와 함께 이동할지 또는 멤버의 부모로 이동할지 여부를 UPDATE 작업에 지정할 수 있습니다. 부모-자식 계층의 멤버를 재귀적으로 삭제하려면 이 멤버와 이 멤버의 모든 하위 항목에 대해 관계형 테이블에 대한 업데이트 권한이 있어야 합니다.  
  
> [!NOTE]  
>  부모-자식 계층의 부모 특성에 대한 업데이트에 다른 속성이나 특성에 대한 업데이트를 포함할 수 없습니다.  
  
 차원을 변경하면 항상 차원 구조가 수정됩니다. 각 차원 변경은 단일 트랜잭션으로 간주되므로 증분 처리에서 차원 구조를 업데이트해야 합니다. 쓰기 가능 차원의 처리 요구 사항은 다른 차원과 동일합니다.  
  
> [!NOTE]  
>  연결된 차원에서는 차원 쓰기 저장이 지원되지 않습니다.  
  
## <a name="security"></a>보안  
 쓰기 가능 차원에 대한 읽기/쓰기 권한이 부여된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 역할의 업무용 사용자만 쓰기 가능 차원을 업데이트할 수 있습니다. 각 역할에 대해 업데이트할 수 있는 멤버와 업데이트할 수 없는 멤버를 제어할 수 있습니다. 업무용 사용자가 쓰기 가능 차원을 업데이트하기 위해서는 클라이언트 응용 프로그램에서 이 기능을 지원해야 합니다. 또한 쓰기 가능 차원이 마지막으로 변경된 이후에 처리된 큐브에 차원이 포함되어 있어야 합니다. 자세한 내용은 [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)을 참조하세요.  
  
 Administrators 역할의 사용자와 그룹은 큐브에 포함되어 있지 않은 쓰기 가능 차원의 특성 멤버도 업데이트할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 차원 속성](database-dimension-properties.md)   
 [쓰기 가능 파티션](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [차원 &#40;Analysis Services-다차원 데이터&#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
