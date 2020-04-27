---
title: 타겟 메일링 마이닝 모델 구조 만들기 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bd2e9d0decc730a59b63ee600bec2d080cc85fb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856159"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>타겟 메일링 마이닝 모델 구조 만들기(기본 데이터 마이닝 자습서)
  타겟 메일링 시나리오를 만드는 첫 번째 단계는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 데이터 마이닝 마법사를 사용하여 새 마이닝 구조와 의사 결정 트리 마이닝 모델을 만드는 것입니다.  
  
 이 태스크에서는 새 마이닝 구조를 설정 하 고 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘을 기반으로 초기 마이닝 모델을 추가 합니다. 구조를 만들려면 먼저 테이블 및 뷰를 선택하고 학습에 사용될 열과 테스트에 사용될 열을 식별합니다.  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>타겟 메일링 시나리오의 마이닝 구조를 만들려면  
  
1.  솔루션 탐색기에서 **마이닝 구조** 를 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 구조** 를 선택 하 여 데이터 마이닝 마법사를 시작 합니다.  
  
2.  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스** 를 선택 했는지 확인 하 고 **다음**을 클릭 합니다.  
  
4.  **데이터 마이닝 구조 만들기** 페이지의 **사용할 데이터 마이닝 기술**선택 페이지에서 **Microsoft 의사 결정 트리**를 선택 합니다.  
  
    > [!NOTE]  
    >  데이터 마이닝 알고리즘을 찾을 수 없다는 경고가 나타나는 경우 프로젝트 속성이 제대로 구성되지 않은 것일 수 있습니다. 이 경고는 프로젝트가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에서 데이터 마이닝 알고리즘의 목록을 검색하려고 할 때 해당 서버를 찾을 수 없으면 발생합니다. 기본적으로에서는 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] **localhost** 를 서버로 사용 합니다. 다른 인스턴스나 명명된 인스턴스를 사용할 경우에는 프로젝트 속성을 변경해야 합니다. 자세한 내용은 [Analysis Services 프로젝트 만들기 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)를 참조 하세요.  
  
5.  **다음**을 클릭합니다.  
  
6.  **데이터 원본 뷰 선택** 페이지의 **사용 가능한 데이터 원본 뷰** 창에서 **대상 메일링**을 선택 합니다. **찾아보기** 를 클릭 하 여 데이터 원본 뷰의 테이블을 확인 한 다음 **닫기** 를 클릭 하 여 마법사로 돌아갈 수 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  **테이블 유형 지정** 페이지에서 사례 테이블로 사용할 vTargetMail의 **사례** 열에 있는 확인란을 선택 하 고 **다음**을 클릭 합니다. 나중에 테스트를 위해 ProspectiveBuyer 테이블을 사용하겠지만 지금은 무시합니다.  
  
9. **학습 데이터 지정** 페이지에서 모델에 대해 하나 이상의 예측 가능한 열, 하나의 키 열 및 하나의 입력 열을 식별 합니다. **Bikebuyer** 행의 **예측 가능한** 열에서 확인란을 선택 합니다.  
  
    > [!NOTE]  
    >  창 맨 아래에는 경고가 있습니다. 하나 이상의 **입력** 및 **예측 가능한** 열을 선택할 때까지 다음 페이지로 이동할 수 없습니다.  
  
10. **제안** 을 클릭 하 여 **관련 열 제안** 대화 상자를 엽니다.  
  
     하나 이상의 예측 가능한 특성을 선택할 때마다 **제안** 단추가 활성화 됩니다. **관련 열 제안** 대화 상자는 예측 가능한 열과 가장 밀접 하 게 관련 된 열을 나열 하 고 예측 가능한 특성과의 상관 관계를 기준으로 특성을 정렬 합니다. 신뢰도가 95%보다 큰 높은 상관 관계의 열이 자동으로 선택되어 모델에 포함됩니다.  
  
     제안 사항을 검토 한 다음 제안 무시 **를 클릭 합니다** .  
  
    > [!NOTE]  
    >  **확인**을 클릭 하면 나열 된 모든 제안이 마법사에서 입력 열로 표시 됩니다. 제안 사항에 일부만 동의하면 값을 수동으로 변경해야 합니다.  
  
11. **Customerkey** 행에서 **키** 열의 확인란을 선택 했는지 확인 합니다.  
  
    > [!NOTE]  
    >  데이터 원본 뷰의 원본 테이블이 키를 나타내면 데이터 마이닝 마법사에서 해당 열이 모델의 키로 자동 선택됩니다.  
  
12. 다음 행의 **입력** 열에서 확인란을 선택 합니다. 확인란을 선택하는 동안 셀 범위를 강조 표시하고 Ctrl 키를 눌러 여러 열을 선택할 수 있습니다.  
  
    -   **발전할**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **구분**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **지역**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. 페이지의 가장 왼쪽 열에서 다음 행의 확인란을 선택합니다.  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **성이**  
  
     왼쪽 열에서만 이러한 행에 확인란이 있습니다. 이러한 열은 구조에 추가되지만 모델에 포함되지는 않습니다. 그러나 모델을 작성하면 드릴스루 및 테스트에 사용할 수 있습니다. 드릴스루에 대 한 자세한 내용은 [데이터 마이닝 &#40;드릴스루 쿼리](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md) 를 참조 하세요&#41;  
  
14. **다음**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [기본 데이터 마이닝 자습서 &#40;데이터 형식 및 내용 유형 지정&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 마법사 &#40;테이블 형식을 지정&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 의사 결정 트리 알고리즘](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
