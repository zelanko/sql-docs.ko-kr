---
title: 대상 메일 구조에 새 모델 추가 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 512c6888-60f1-46e4-9639-bc448395b8d7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 285ee82110ffdef521d75fb43343f4889663e981
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822644"
---
# <a name="adding-new-models-to-the-targeted-mailing-structure-basic-data-mining-tutorial"></a>대상 메일 구조에 새 모델 추가(기본 데이터 마이닝 자습서)
  이 태스크에서는 데이터 마이닝 디자이너의 **마이닝 모델** 탭을 사용 하 여 두 개의 추가 모델을 정의 합니다. Microsoft 클러스터링 및 Microsoft Naive Bayes 알고리즘을 사용하여 모델을 만듭니다. 이 두 알고리즘의 기능으로 불연속 값(예: 자전거 구매)을 예측할 수 있으므로 이 알고리즘이 선택되었습니다. 이러한 알고리즘에 대 한 자세한 내용은 [Microsoft 클러스터링 알고리즘](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md) 및 [Microsoft Naive Bayes 알고리즘](../../2014/analysis-services/data-mining/microsoft-naive-bayes-algorithm.md) 을 참조 하세요.  
  
### <a name="to-create-a-clustering-mining-model"></a>클러스터링 마이닝 모델을 만들려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]데이터 마이닝 디자이너에서 **마이닝 모델** 탭으로 전환 합니다.  
  
     디자이너에는 마이닝 구조에 대 한 열과 이전 단원에서 만든 `TM_Decision_Tree` 마이닝 모델에 대 한 두 개의 열이 표시 됩니다.  
  
2.  **구조** 열을 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 모델**을 선택 합니다.  
  
3.  **새 마이닝 모델** 대화 상자의 **모델 이름**에을 입력 `TM_Clustering`합니다.  
  
4.  **알고리즘 이름**에서 **Microsoft 클러스터링**을 선택 합니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 이제 데이터 마이닝 디자이너의 **마이닝 모델** 탭에 새 모델이 나타납니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 클러스터링 알고리즘을 사용 하 여 작성 된이 모델은 클러스터에 유사한 특성을 가진 고객을 그룹화 하 고 각 클러스터에 대 한 자전거 구매를 예측 합니다. 새 모델에 대 한 열 사용 및 속성을 수정할 수 있지만이 자습서에서는 `TM_Clustering` 모델을 변경할 필요가 없습니다.  
  
### <a name="to-create-a-naive-bayes-mining-model"></a>Naive Bayes 마이닝 모델을 만들려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 **구조** 열을 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 모델**을 선택 합니다.  
  
2.  **새 마이닝 모델** 대화 상자의 **모델 이름**에을 입력 `TM_NaiveBayes`합니다.  
  
3.  **알고리즘 이름**에서 **Microsoft Naive Bayes**를 선택한 다음 **확인**을 클릭 합니다.  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes 알고리즘이 연속 인 **Age** 및 **연간 소득** 열을 지원 하지 않음을 나타내는 메시지가 표시 됩니다.  
  
4.  **예** 를 클릭 하 여 메시지를 승인 하 고 계속 합니다.  
  
 데이터 마이닝 디자이너의 **마이닝 모델** 탭에 새 모델이 나타납니다. 이 탭의 모든 모델에 대 한 열 사용 및 속성을 수정할 수 있지만이 자습서에서는 `TM_NaiveBayes` 모델을 변경할 필요가 없습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [기본 데이터 마이닝 자습서 &#40;대상 메일 구조에서 모델 처리&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 데이터 마이닝 &#40;구조에 마이닝 모델을 추가&#41;](../../2014/analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)   
 [데이터 마이닝 디자이너](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [데이터 마이닝 개체 이동](../../2014/analysis-services/data-mining/moving-data-mining-objects.md)  
  
  
