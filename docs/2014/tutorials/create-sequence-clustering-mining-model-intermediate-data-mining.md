---
title: 시퀀스 클러스터링 마이닝 모델 구조 만들기 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7f4f543952fd86cf6c3c66f9f4b2c51019b1869
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63273474"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>시퀀스 클러스터링 마이닝 모델 구조 만들기(중급 데이터 마이닝 자습서)
  시퀀스 클러스터링 마이닝 모델을 만드는 첫 번째 단계는 데이터 마이닝 마법사를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 기반으로 하는 새 마이닝 구조 및 마이닝 모델을 만드는 것입니다.  
  
 시장 바구니 분석에 사용된 동일한 데이터 원본 뷰를 사용하지만 `sequence` 식별자가 포함되어 있는 열을 추가합니다. 이 시나리오에서 시퀀스는 고객이 시장 바구니에 항목을 추가한 순서를 의미합니다.  
  
 또한 고객을 인구 통계별로 그룹화하는 모델 중 하나에 사용되는 일부 열을 추가합니다.  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>시퀀스 클러스터링 구조 및 모델을 만들려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]솔루션 탐색기에서 **마이닝 구조** 를 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 구조**를 선택 합니다.  
  
2.  
  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스** 를 선택 했는지 확인 하 고 **다음**을 클릭 합니다.  
  
4.  **데이터 마이닝 구조 만들기** 페이지에서 **마이닝 모델을 사용 하 여 마이닝 구조 만들기** 옵션이 선택 되어 있는지 확인 합니다. 그런 다음 **사용 하려는 데이터 마이닝 기술**옵션의 드롭다운 목록을 클릭 하 고 **Microsoft 시퀀스 클러스터링**을 선택 합니다. **다음**을 클릭합니다.  
  
     **데이터 원본 뷰 선택** 페이지가 나타납니다. **사용 가능한 데이터 원본 뷰**에서을 `Orders`선택 합니다.  
  
     Orders는 시장 바구니 시나리오에 사용한 동일한 데이터 원본 뷰입니다. 이 데이터 원본 뷰를 만들지 않은 경우 [중첩 테이블을 사용 하 여 데이터 원본 뷰 추가 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)를 참조 하세요.  
  
5.  **다음**을 클릭합니다.  
  
6.  **테이블 유형 지정** 페이지에서 **vAssocSeqOrders** 테이블 옆의 **사례** 확인란을 선택 하 고 **vAssocSeqLineItems** 테이블 옆의 **중첩** 된 확인란을 선택 합니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  **사례** 또는 **중첩** 된 확인란을 선택할 때 오류가 발생 하는 경우 데이터 원본 뷰의 조인이 올바르지 않을 수 있습니다. 중첩 테이블 **vAssocSeqLineItems**는 다 대 일 조인으로 사례 테이블 **vAssocSeqOrders** 에 연결 되어야 합니다. 조인 선을 마우스 오른쪽 단추로 클릭한 다음 조인 방향을 반대로 바꿔 관계를 편집할 수 있습니다. 자세한 내용은 [Analysis Services-다차원 데이터&#41;&#40;관계 만들기 또는 편집 대화 상자 ](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md)를 참조 하세요.  
  
7.  **학습 데이터 지정** 페이지에서 다음과 같이 확인란을 선택 하 여 모델에서 사용할 열을 선택 합니다.  
  
    -   **IncomeGroup** **입력** 확인란을 선택 합니다.  
  
         이 열에는 클러스터링에 사용할 수 있는 고객에 대한 유용한 정보가 들어 있습니다. 첫 번째 모델에서 이 열을 사용한 다음 두 번째 모델에서 무시합니다.  
  
    -   **Ordernumber** 확인란을 `Key` 선택 합니다.  
  
         이 필드는 사례 테이블에 대한 식별자인 `Key`로 사용됩니다. 일반적으로 키에 클러스터링에 유용하지 않은 고유 값이 포함되어 있으므로 사례 테이블의 키 필드를 입력으로 사용할 수 없습니다.  
  
    -   **영역** **입력** 확인란을 선택 합니다.  
  
         이 열에는 클러스터링에 사용할 수 있는 고객에 대한 유용한 정보가 들어 있습니다. 첫 번째 모델에서 이 열을 사용한 다음 두 번째 모델에서 무시합니다.  
  
    -   **LineNumber** `Key` 및 **입력** 확인란을 선택 합니다.  
  
         **LineNumber** 필드는 중첩 테이블에 대 한 식별자로 사용 됩니다 `Sequence Key`. 중첩 테이블의 키는 항상 입력으로 사용해야 합니다.  
  
    -   **모델** **입력** 및 **예측** 가능 확인란을 선택 합니다.  
  
     선택 항목이 올바른지 확인 하 고 **다음**을 클릭 합니다.  
  
8.  **열 내용 및 데이터 형식 지정** 페이지에서 표에 다음 표에 표시 된 열, 내용 유형 및 데이터 형식이 포함 되어 있는지 확인 하 **고 다음을 클릭 합니다**.  
  
    |테이블/열|콘텐츠 형식|데이터 형식|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|불연속|텍스트|  
    |OrderNumber|키|텍스트|  
    |지역|불연속|텍스트|  
    |vAssocSeqLineItems|||  
    |Line Number|키 시퀀스|long|  
    |모델|불연속|텍스트|  
  
9. **테스트 집합 만들기** 페이지에서 **테스트에 사용할 데이터의 백분율** 을 20으로 변경 하 고 **다음**을 클릭 합니다.  
  
10. **마법사 완료** 페이지에서 **마이닝 구조 이름**에을 입력 `Sequence Clustering with Region`합니다.  
  
11. **마이닝 모델 이름**에을 입력 `Sequence Clustering with Region`합니다.  
  
12. **드릴스루 허용** 상자를 선택 하 고 **마침**을 클릭 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [시퀀스 클러스터링 모델 처리](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 시퀀스 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  
