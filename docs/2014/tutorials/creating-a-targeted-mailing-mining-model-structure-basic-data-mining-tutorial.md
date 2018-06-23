---
title: 타겟된 메일링 마이닝 모델 구조 (기본 데이터 마이닝 자습서) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
caps.latest.revision: 54
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3f0a8632df2009846d8b17d956c750ae12356829
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312481"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>타겟 메일링 마이닝 모델 구조 만들기(기본 데이터 마이닝 자습서)
  타겟 메일링 시나리오를 만드는 첫 번째 단계는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 데이터 마이닝 마법사를 사용하여 새 마이닝 구조와 의사 결정 트리 마이닝 모델을 만드는 것입니다.  
  
 이 작업에서는 새 마이닝 구조를 설정 및 기반으로 초기 마이닝 모델을 추가 합니다는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의사 결정 트리 알고리즘입니다. 구조를 만들려면 먼저 테이블 및 뷰를 선택하고 학습에 사용될 열과 테스트에 사용될 열을 식별합니다.  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>타겟 메일링 시나리오의 마이닝 구조를 만들려면  
  
1.  솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **Mining Structures** 선택 **새 마이닝 구조** 데이터 마이닝 마법사를 시작 합니다.  
  
2.  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스에서** 을 선택한 다음 클릭 **다음**합니다.  
  
4.  에 **데이터 마이닝 구조 만들기** 페이지의 **사용할 데이터 마이닝 기술을 사용 하 시겠습니까?** 선택, **Microsoft 의사 결정 트리**합니다.  
  
    > [!NOTE]  
    >  데이터 마이닝 알고리즘을 찾을 수 없다는 경고가 나타나는 경우 프로젝트 속성이 제대로 구성되지 않은 것일 수 있습니다. 이 경고는 프로젝트가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에서 데이터 마이닝 알고리즘의 목록을 검색하려고 할 때 해당 서버를 찾을 수 없으면 발생합니다. 기본적으로 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ´ ֲ **localhost** 서버로 합니다. 다른 인스턴스나 명명된 인스턴스를 사용할 경우에는 프로젝트 속성을 변경해야 합니다. 자세한 내용은 참조 [Analysis Services 프로젝트 만들기 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  에 **데이터 원본 뷰 선택** 페이지는 **사용 가능한 데이터 원본 뷰** 창, 선택 **Targeted Mailing**합니다. 클릭할 수 있는 **찾아보기** 데이터 원본 뷰에서 테이블을 확인 한 다음 클릭 **닫기** 하 고 마법사로 돌아갑니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  에 **테이블 유형 지정** 페이지에 있는 확인란을 선택 합니다는 **대/소문자** vTargetMail 사례 테이블로 사용 하 고 클릭 한 다음에 대 한 열 **다음**합니다. 나중에 테스트를 위해 ProspectiveBuyer 테이블을 사용하겠지만 지금은 무시합니다.  
  
9. 에 **학습 데이터 지정** 페이지에서 하나 이상의 예측 가능한 열, 하나의 키 열을 식별 하면 및 하나의 모델에 대 한 열을 입력 합니다. 확인란을 선택는 **예측 가능** 열에는 **BikeBuyer** 행입니다.  
  
    > [!NOTE]  
    >  창 맨 아래에는 경고가 있습니다. 하나 이상 선택 하 여 다음 페이지로 이동할 수 없습니다 **입력** 하나의 **예측 가능** 열입니다.  
  
10. 클릭 **제안** 열려는 **관련 열 제안** 대화 상자.  
  
     **제안** 단추는 하나 이상의 예측 가능한 특성을 선택할 때마다 활성화 됩니다. **관련 열 제안** 대화 상자와 가장 밀접 한 예측 가능한 열에 있는 열을 나열 하 고 특성의 상관 관계와 예측 가능한 특성을 기준으로 정렬 합니다. 신뢰도가 95%보다 큰 높은 상관 관계의 열이 자동으로 선택되어 모델에 포함됩니다.  
  
     제안을 검토 한 다음 클릭 **취소** toignore 제안 합니다.  
  
    > [!NOTE]  
    >  클릭 하면 **확인**, 나열 된 모든 제안이 마법사에서 입력된 열으로 표시 됩니다. 제안 사항에 일부만 동의하면 값을 수동으로 변경해야 합니다.  
  
11. 확인 확인란에는 **키** 열을 선택는 **r k e y** 행입니다.  
  
    > [!NOTE]  
    >  데이터 원본 뷰의 원본 테이블이 키를 나타내면 데이터 마이닝 마법사에서 해당 열이 모델의 키로 자동 선택됩니다.  
  
12. 에 있는 확인란을 선택는 **입력** 다음 행에 있는 열입니다. 확인란을 선택하는 동안 셀 범위를 강조 표시하고 Ctrl 키를 눌러 여러 열을 선택할 수 있습니다.  
  
    -   **Age**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Gender**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Region**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. 페이지의 가장 왼쪽 열에서 다음 행의 확인란을 선택합니다.  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **LastName**  
  
     왼쪽 열에서만 이러한 행에 확인란이 있습니다. 이러한 열은 구조에 추가되지만 모델에 포함되지는 않습니다. 그러나 모델을 작성하면 드릴스루 및 테스트에 사용할 수 있습니다. 드릴스루에 대 한 자세한 내용은 참조 [드릴스루 쿼리 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. **다음**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [데이터 형식 및 내용 유형 지정 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [테이블 유형 지정 &#40;데이터 마이닝 마법사&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 의사 결정 트리 알고리즘](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  