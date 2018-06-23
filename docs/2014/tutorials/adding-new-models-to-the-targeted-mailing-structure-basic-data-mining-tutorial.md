---
title: (기본 데이터 마이닝 자습서)의 대상된 메일 구조에 새 모델 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c5e31e06a489b1807335f63dd1675fc9e77c45b4
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312381"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>대상 메일 구조에 새 모델 추가(기본 데이터 마이닝 자습서)
  이 작업에서 사용 하 여 두 개의 추가 모델 정의 합니다는 **마이닝 모델** 데이터 마이닝 디자이너의 탭 합니다. Microsoft 클러스터링 및 Microsoft Naive Bayes 알고리즘을 사용하여 모델을 만듭니다. 이 두 알고리즘의 기능으로 불연속 값(예: 자전거 구매)을 예측할 수 있으므로 이 알고리즘이 선택되었습니다. 이러한 알고리즘에 대 한 자세한 내용은 참조 [Microsoft 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) 및 [Microsoft Naive Bayes 알고리즘](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)  
  
### <a name="to-create-a-clustering-mining-model"></a>클러스터링 마이닝 모델을 만들려면  
  
1.  전환 하는 **마이닝 모델** 탭의 데이터 마이닝 디자이너에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]합니다.  
  
     디자이너에는 두 개의 열에 대 한 여러 개 있는 마이닝 구조에 대 한 표시는 `TM_Decision_Tree` 이전 단원에서 만든 마이닝 모델에 있습니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **구조** 선택 **새 마이닝 모델**합니다.  
  
3.  에 **새 마이닝 모델** 대화 상자의 **모델 이름**, 형식 `TM_Clustering`합니다.  
  
4.  **알고리즘 이름**선택, **Microsoft 클러스터링**합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 새 모델에 이제 표시는 **마이닝 모델** 데이터 마이닝 디자이너의 탭 합니다. 이 모델을 사용 하 여 빌드한는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 알고리즘, 고객 비슷한 특징을 가진 클러스터로 그룹화 하 고 자전거 각 클러스터에 대 한 구매를 예측 합니다. 열 사용 및 새 모델의 변경에 대 한 속성을 수정할 수 있지만 `TM_Clustering` 모델은이 자습서에 필요 합니다.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Naive Bayes 마이닝 모델을 만들려면  
  
1.  에 **마이닝 모델** 데이터 마이닝 디자이너의 오른쪽 번 누릅니다 **구조** 열 및 선택 **새 마이닝 모델**합니다.  
  
2.  에 **새 마이닝 모델** 대화 상자의 **모델 이름**, 형식 `TM_NaiveBayes`합니다.  
  
3.  **알고리즘 이름**선택, **Microsoft Naive Bayes**, 클릭 **확인**합니다.  
  
     내용을 입력 하는 메시지가 표시는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 알고리즘을 지원 하지 않습니다는 **Age** 및 **Yearly Income** 연속 하는 열입니다.  
  
4.  클릭 **예** 메시지를 확인 하 고 계속 합니다.  
  
 새 모델이 나타납니다는 **마이닝 모델** 데이터 마이닝 디자이너의 탭 합니다. 열 사용 및이 모든 모델에 대 한 속성을 수정할 수 있지만 탭 변경 없이 `TM_NaiveBayes` 모델은이 자습서에 필요 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [대상된 메일 구조에서 모델 처리 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [구조에 마이닝 모델 추가 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [데이터 마이닝 개체 이동](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  