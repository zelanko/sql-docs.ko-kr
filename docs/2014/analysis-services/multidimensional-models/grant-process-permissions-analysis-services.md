---
title: 프로세스 권한 부여 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], process
- process permissions [Analysis Services]
ms.assetid: c1531c23-6b46-46a8-9ba3-b6d3f2016443
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49b8a1c8ce566b18143b6b693a227fba4a5bd094
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074884"
---
# <a name="grant-process-permissions-analysis-services"></a>처리 권한 부여(Analysis Services)
  관리자는 Analysis Services 처리 작업의 전용 역할을 만들어, 다른 사용자 또는 자동 일정 처리를 위해 사용되는 애플리케이션에 특정 작업을 위임할 수 있습니다. 처리 권한은 데이터베이스,  큐브,  차원 및 마이닝 구조 수준에서 부여할 수 있습니다. 대규모 큐브 또는 테이블 형식 데이터베이스에서 작업하지 않는다면 서로 종속된 개체를 비롯한 모든 개체를 포함하여 데이터베이스 수준에서 처리 권한을 부여하는 것이 좋습니다.  
  
 권한은, 개체를 권한 및 Windows 사용자 또는 그룹 계정과 연결하는 역할을 통해 부여됩니다. 이러한 권한은 부가적입니다. 한 역할이 큐브를 처리하는 권한을 부여하고 두 번째 역할은 동일한 사용자에게 차원을 처리하는 권한을 부여하는 경우 두 가지 역할의 권한이 결합되어 해당 데이터베이스 내에서 큐브를 처리하고 지정된 차원을 처리하는 권한을 모두 사용자에게 부여합니다.  
  
> [!IMPORTANT]  
>  처리 권한만 가진 역할의 사용자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용해서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 연결하여 개체를 처리할 수 없습니다. 이러한 도구를 사용하려면 개체 메타데이터에 액세스할 수 있는 `Read Definition` 권한이 있어야 합니다. 두 가지 도구를 사용할 수 없는 경우 처리 작업을 실행하려면 XMLA 스크립트를 사용해야 합니다.  
>   
>  테스트를 위해 `Read Definition` 권한을 부여하는 것도 좋습니다. `Read Definition` 및 `Process Database` 권한을 모두 가진 사용자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체를 대화형으로 처리할 수 있습니다. 자세한 내용은 [Grant read definition permissions on object metadata &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md) 를 참조하세요.  
  
## <a name="set-processing-permissions-at-the-database-level"></a>데이터베이스 수준에서 처리 권한 설정  
 이 섹션에서는 데이터베이스의 모든 큐브, 차원, 마이닝 구조 및 마이닝 모델에 대해 관리자가 아닌 사용자의 처리를 사용하도록 설정하는 방법을 설명합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 데이터베이스 폴더를 열고 데이터베이스를 선택합니다.  
  
2.  **역할** | **새 역할**을 마우스 오른쪽 단추로 클릭합니다. 이름 및 설명을 입력합니다.  
  
3.  에 **일반적인** 창은 `Process Database` 확인란 합니다. 또한 선택 하 고 `Read Definition` 도 대화형 SQL Server 도구 중 하나를 통해 같은 처리를 사용 하도록 설정 하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
4.  **멤버 자격** 창에서 이 데이터베이스의 모든 개체를 처리할 수 있는 권한을 가진 Windows 사용자 및 그룹 계정을 추가합니다.  
  
5.  **확인** 을 클릭하여 역할 정의를 완료합니다.  
  
## <a name="set-processing-permissions-on-individual-objects"></a>개별 개체에 대한 처리 권한 설정  
 개별 큐브, 차원, 데이터 마이닝 구조 또는 모델에 대한 처리 권한을 설정할 수 있습니다.  
  
 함께 처리해야 하는 개체를 실수로 제외하는 경우(예를 들어 관련 차원은 제외하고 큐브에 대한 처리를 사용하도록 설정하는 경우) 처리가 실패할 수 있습니다. 개체 종속성은 놓치기 쉬우므로 개별 개체에 대한 처리 권한을 설정할 때 철저한 테스트가 중요합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 데이터베이스 폴더를 열고 데이터베이스를 선택합니다.  
  
2.  **역할** | **새 역할**을 마우스 오른쪽 단추로 클릭합니다. 이름 및 설명을 입력합니다.  
  
3.  에 **일반적인** 창 지우기는 `Process Database` 확인란 합니다. 데이터베이스 권한은 역할 옵션을 회색으로 표시하거나 선택하지 못하도록 설정하여 하위 수준의 개체에 대한 권한을 설정하는 기능을 재정의합니다.  
  
     기술적으로, 전용 처리 역할의 경우 데이터베이스 권한은 필요하지 않습니다. 없이 `Read Definition` 데이터베이스 수준에서 데이터베이스를 볼 수 없습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]테스트가 더 어려워집니다.  
  
4.  처리할 개별 개체를 선택합니다.  
  
    -   **큐브** 창에서 각 큐브에 대한 **처리** 확인란을 선택합니다.  
  
    -   **차원** 창에서 **모든 데이터베이스 차원**을 선택한 다음 각 차원에 대한 **처리** 확인란을 선택합니다. 또는 모든 행을 선택한 다음 Shift를 클릭하여 확인란 선택을 전환합니다.  
  
5.  **멤버 자격** 창에서 이러한 개체를 처리할 수 있는 권한을 가진 Windows 사용자 및 그룹 계정을 추가합니다.  
  
6.  **확인** 을 클릭하여 역할 정의를 완료합니다.  
  
## <a name="test-processing"></a>테스트 처리  
  
1.  Shift 키를 누르고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 마우스 오른쪽 단추로 클릭하고, **다른 사용자 권한으로 실행** 을 선택하고 테스트 중인 역할에 할당된 Windows 계정을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  데이터베이스 폴더를 열고 데이터베이스를 선택합니다. 사용 중인 계정이 멤버 자격을 가진 역할에 표시되는 데이터베이스만 볼 수 있습니다.  
  
3.  큐브 또는 차원을 마우스 오른쪽 단추로 클릭하고 **처리**를 선택합니다. 처리 옵션을 선택합니다. 모든 개체 조합에 대해 모든 옵션을 테스트합니다. 개체가 누락되어 오류가 발생하는 경우 역할에 개체를 추가하세요.  
  
## <a name="set-processing-permissions-on-a-data-mining-structure"></a>데이터 마이닝 구조에 대한 처리 권한 설정  
 데이터 마이닝 구조를 처리할 수 있는 권한을 부여하는 역할을 만들 수 있습니다. 여기에는 모든 마이닝 모델의 처리가 포함됩니다.  
  
 **드릴스루** 고 `Read Definition` 마이닝 모델 및 구조를 검색 하는 것에 대 한 사용 권한은 원자성과 동일한 역할에 추가 하거나 여러 역할로 분리할 수 있습니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 데이터베이스 폴더를 열고 데이터베이스를 선택합니다.  
  
2.  **역할** | **새 역할**을 마우스 오른쪽 단추로 클릭합니다. 이름 및 설명을 입력합니다. **일반** 창에서 데이터베이스 권한 확인란을 선택 취소합니다. 데이터베이스 권한은 역할 옵션을 회색으로 표시하거나 선택하지 못하도록 설정하여 하위 수준의 개체에 대한 권한을 설정하는 기능을 재정의합니다.  
  
3.  **마이닝 구조** 창에서 각 마이닝 구조에 대한 **처리** 확인란을 선택합니다.  
  
4.  **멤버 자격** 창에서 이 데이터베이스의 모든 개체를 처리할 수 있는 권한을 가진 Windows 사용자 및 그룹 계정을 추가합니다.  
  
5.  **확인** 을 클릭하여 역할 정의를 완료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스, 테이블 또는 파티션 처리](../tabular-models/process-database-table-or-partition-analysis-services.md)   
 [다차원 모델 개체 처리](processing-a-multidimensional-model-analysis-services.md)   
 [Grant 데이터베이스 사용 권한 & #40; Analysis Services & #41;](grant-database-permissions-analysis-services.md)   
 [정의 읽기 권한 부여 개체 메타 데이터 & #40; Analysis Services & #41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
  
