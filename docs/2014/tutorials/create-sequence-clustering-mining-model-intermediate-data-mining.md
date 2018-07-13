---
title: 시퀀스 클러스터링 마이닝 모델 구조 (중급 데이터 마이닝 자습서) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c18097b6851bc23522882227158b5aad390570e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189570"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>시퀀스 클러스터링 마이닝 모델 구조 만들기(중급 데이터 마이닝 자습서)
  시퀀스 클러스터링 마이닝 모델을 만드는 첫 번째 단계는 데이터 마이닝 마법사를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 기반으로 하는 새 마이닝 구조 및 마이닝 모델을 만드는 것입니다.  
  
 시장 바구니 분석에 사용된 동일한 데이터 원본 뷰를 사용하지만 `sequence` 식별자가 포함되어 있는 열을 추가합니다. 이 시나리오에서 시퀀스는 고객이 시장 바구니에 항목을 추가한 순서를 의미합니다.  
  
 또한 고객을 인구 통계별로 그룹화하는 모델 중 하나에 사용되는 일부 열을 추가합니다.  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>시퀀스 클러스터링 구조 및 모델을 만들려면  
  
1.  솔루션 탐색기에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 마우스 오른쪽 단추로 클릭 **Mining Structures** 선택한 **새 마이닝 구조**합니다.  
  
2.  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스에서** 를 선택한 다음 클릭 **다음**합니다.  
  
4.  에 **데이터 마이닝 구조 만들기** 페이지에서 옵션 **마이닝 모델을 사용 하 여 마이닝 구조 만들기** 을 선택 합니다. 옵션의 경우 드롭다운 목록에서 클릭 **사용할 데이터 마이닝 기술을 사용 하 시겠습니까?**, 선택한 **Microsoft 시퀀스 클러스터링**합니다. **다음**을 클릭합니다.  
  
     합니다 **데이터 원본 뷰 선택** 페이지가 나타납니다. 아래 **사용 가능한 데이터 원본 뷰**, 선택 `Orders`합니다.  
  
     Orders는 시장 바구니 시나리오에 사용한 동일한 데이터 원본 뷰입니다. 이 데이터 원본 뷰를 만들지 않은 경우 [중첩 테이블을 사용 하 여 데이터 원본 뷰 추가 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)합니다.  
  
5.  **다음**을 클릭합니다.  
  
6.  에 **테이블 유형 지정** 페이지에서를 **사례** 옆에 확인란을 **vAssocSeqOrders** 테이블을 선택한를 **중첩** 확인란 다음에 **vAssocSeqLineItems** 테이블입니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  선택할 때 오류가 발생 하는 경우는 **대/소문자** 하거나 **중첩** 확인란을는 것이 데이터 원본 뷰의 조인이 올바르지 않습니다. 중첩된 테이블 **vAssocSeqLineItems**에서 사례 테이블에 연결 해야 **vAssocSeqOrders를** 다 대 일 조인으로 합니다. 조인 선을 마우스 오른쪽 단추로 클릭한 다음 조인 방향을 반대로 바꿔 관계를 편집할 수 있습니다. 자세한 내용은 [만들거나 관계 편집 대화 상자 &#40;Analysis Services-Multidimensional Data&#41;](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md)합니다.  
  
7.  에 **학습 데이터 지정** 페이지에서 다음과 같이 확인란을 선택 하 여 모델에 사용할 열을 선택 합니다.  
  
    -   **IncomeGroup** 를 선택 합니다 **입력** 확인란 합니다.  
  
         이 열에는 클러스터링에 사용할 수 있는 고객에 대한 유용한 정보가 들어 있습니다. 첫 번째 모델에서 이 열을 사용한 다음 두 번째 모델에서 무시합니다.  
  
    -   **OrderNumber** 선택 된 `Key` 확인란 합니다.  
  
         이 필드는 사례 테이블에 대한 식별자인 `Key`로 사용됩니다. 일반적으로 키에 클러스터링에 유용하지 않은 고유 값이 포함되어 있으므로 사례 테이블의 키 필드를 입력으로 사용할 수 없습니다.  
  
    -   **지역** 를 선택 합니다 **입력** 확인란 합니다.  
  
         이 열에는 클러스터링에 사용할 수 있는 고객에 대한 유용한 정보가 들어 있습니다. 첫 번째 모델에서 이 열을 사용한 다음 두 번째 모델에서 무시합니다.  
  
    -   **LineNumber** 를 선택 합니다 `Key` 하 고 **입력** 확인란 합니다.  
  
         합니다 **LineNumber** 중첩된 테이블에 대 한 식별자로 사용할는 필드 또는 `Sequence Key`합니다. 중첩 테이블의 키는 항상 입력으로 사용해야 합니다.  
  
    -   **모델** 를 선택 합니다 **입력** 하 고 **예측 가능** 확인란 합니다.  
  
     선택 항목을 올바른지를 클릭 한 다음 확인 **다음**합니다.  
  
8.  에 **지정할 열 내용 및 데이터 형식** 페이지, 모눈 열, 콘텐츠 형식 및 다음 표에 표시 된 데이터 형식을 포함 되어 있는지 확인 한 다음 클릭 **다음**합니다.  
  
    |테이블/열|내용 유형|데이터 형식|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|불연속|텍스트 모드|  
    |OrderNumber|Key|텍스트 모드|  
    |Region|불연속|텍스트 모드|  
    |vAssocSeqLineItems|||  
    |Line Number|키 시퀀스|Long|  
    |Model|불연속|텍스트 모드|  
  
9. 에 **테스트 집합 만들기** 페이지에서 변경 합니다 **테스트용 데이터 비율** 20를 클릭 한 다음 **다음**합니다.  
  
10. 에 **마법사 완료** 페이지에 대 한 합니다 **마이닝 구조 이름**, 형식 `Sequence Clustering with Region`합니다.  
  
11. 에 대 한 합니다 **마이닝 모델 이름**, 형식 `Sequence Clustering with Region`합니다.  
  
12. 확인 합니다 **드릴스루 허용** 상자를 선택한 다음 클릭 **마침**합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [시퀀스 클러스터링 모델 처리](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 시퀀스 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  
