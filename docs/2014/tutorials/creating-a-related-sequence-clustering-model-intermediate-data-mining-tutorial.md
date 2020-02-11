---
title: 관련 된 시퀀스 클러스터링 모델 만들기 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62855872"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>관련된 시퀀스 클러스터링 모델 만들기(중급 데이터 마이닝 자습서)
  시퀀스 클러스터링 모델 탐색을 통해 Region 또는 Income과 같은 다른 특성이 모델에 중요한 영향을 준다는 것을 알게 되었습니다. 따라서 시퀀스를 보다 잘 이해하려면 관련된 시퀀스 클러스터링 모델을 만들고 고객 인구 통계와 관련된 특성을 제거합니다.  
  
 이 태스크에서 지역 시퀀스 클러스터링 모델의 복사본을 만들고 모델에서 시퀀스와 직접 관련되지 않은 열을 제거합니다.  
  
 새 모델에 새 모델의 기반이 되는 마이닝 모델과 동일한 열이 모두 들어 있습니다. 그러나 마이닝 구조에서 열을 제거하지 않아도 되며, 새 마이닝 모델이 열을 무시하도록 지정하면 됩니다.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>시퀀스 클러스터링 모델의 복사본을 만들려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]데이터 마이닝 디자이너에서 **마이닝 모델** 탭을 클릭 합니다.  
  
2.  복사할 모델을 마우스 오른쪽 단추로 클릭 하 고 **새 마이닝 모델**을 선택 합니다.  
  
3.  **새 마이닝 모델** 대화 상자에서 모델 이름을 입력 하 고 Microsoft `Sequence Clustering`를 선택 합니다.  
  
     이 자습서에서는 이름을 `Sequence Clustering`입력 합니다.  
  
4.  **확인**을 클릭합니다.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>마이닝 모델에서 열을 제거하려면  
  
1.  **마이닝 모델** 탭의 시퀀스 클러스터링 이라는 새 모델의 열에서 **소득 그룹** 특성에 대 한 행을 클릭 하 고 **무시**를 선택 합니다.  
  
2.  특성 **영역**에 대해이 단계를 반복 합니다.  
  
3.  테이블 이름, **v Assoc Seq Line Items**옆에 있는 더하기 기호를 클릭 하 여 테이블을 확장 하 고 중첩 테이블에서 열을 봅니다.  
  
     새 모델에는 다음 열만 있어야 합니다.  
  
     **주문 번호 키**  
  
     **줄 번호 키**  
  
     **모델 예측**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>새 시퀀스 클러스터링 모델을 처리하려면  
  
1.  **마이닝 모델** 탭에서 라는 `Sequence Clustering`새 모델을 마우스 오른쪽 단추로 클릭 하 고 **모델 처리**를 선택 합니다.  
  
     간단한 새 마이닝 모델은 이미 처리된 구조를 기반으로 하므로 구조를 다시 처리하지 않아도 됩니다. 이제 새 마이닝 모델을 처리할 수 있습니다.  
  
2.  업데이트 된 데이터 마이닝 프로젝트를 서버에 배포 하려면 **예** 를 클릭 합니다.  
  
3.  **마이닝 모델 처리** 대화 상자에서 **실행**을 클릭 합니다.  
  
4.  **닫기** 를 클릭 하 여 **처리 진행률** 대화 상자를 닫은 다음 **마이닝 모델 처리** 대화 상자에서 **닫기** 를 다시 클릭 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [시퀀스 클러스터링 모델에서 예측 만들기 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
