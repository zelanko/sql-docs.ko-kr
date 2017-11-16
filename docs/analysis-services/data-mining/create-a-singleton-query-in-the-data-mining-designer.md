---
title: "데이터 마이닝 디자이너에서 단일 쿼리를 작성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- singleton queries [Analysis Services]
- Mining Model Prediction [Analysis Services], singleton queries
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dfbb55881c274dee8560cbba14319bcc831b38c2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>데이터 마이닝 디자이너에서 단일 쿼리 작성
  단일 쿼리는 단일 사례에 대한 예측을 만들려는 경우 유용합니다. 단일 쿼리에 대한 자세한 내용은 [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)를 참조하세요.  
  
 데이터 마이닝 디자이너의 **마이닝 모델 예측** 탭에서 많은 다양한 쿼리 유형을 만들 수 있습니다. 디자이너를 사용하거나 DMX(Data Mining Extensions) 문을 입력하여 쿼리를 만들 수 있습니다. 디자이너로 시작한 다음  DMX 문을 변경하거나 WHERE 또는 ORDER BY 절을 추가하여 디자이너에서 만든 쿼리를 수정할 수도 있습니다.  
  
 쿼리 디자인 뷰와 쿼리 텍스트 뷰 사이를 전환하려면 도구 모음에서 첫 번째 단추를 클릭합니다. 쿼리 텍스트 뷰에서는 예측 쿼리 작성기에서 생성된 DMX 코드를 볼 수 있습니다. 쿼리를 실행하고 쿼리를 수정하며 수정된 쿼리를 실행할 수도 있습니다. 그러나 쿼리 디자인 보기로 다시 전환하면 수정된 쿼리가 지속되지 않습니다.  
  
 다음 코드에서는 대상 메일 모델인 TM_Decision_Tree에 대한 단일 쿼리의 예를 보여 줍니다.  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 다음 단계에서는 이 예측 쿼리를 만드는 방법에 대해 설명합니다.  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>데이터 마이닝 디자이너를 사용하여 단일 쿼리를 만들려면  
  
1.  데이터 마이닝 디자이너에서 **마이닝 모델 예측** 탭을 클릭합니다.  
  
2.  **마이닝 모델** 테이블에서 **모델 선택** 을 클릭합니다.  
  
     **마이닝 모델 선택** 대화 상자가 열리고 현재 프로젝트에 있는 모든 마이닝 구조를 표시합니다.  
  
     예측을 만드는 데 사용할 모델을 선택합니다.  
  
     예를 들어 이 항목의 시작 부분에 표시된 샘플 코드를 만들려면 TM_Decision_Tree를 선택한 다음 **확인**을 클릭합니다.  
  
3.  **마이닝 모델 예측** 탭의 도구 모음에서 **단일 쿼리** 를 클릭합니다.  
  
     탭에 **단일 쿼리 입력** 테이블이 나타납니다. 이 테이블의 열은 **마이닝 모델** 테이블의 열에 자동으로 매핑됩니다.  
  
4.  **단일 쿼리 입력** 테이블의 **값** 열에서 값을 선택하여 예측을 만들 사례를 설명합니다.  
  
     예를 들어 **Number Children At Home** 에 대해 **2**를 선택한 다음 **Age** 에 **45**를 입력합니다.  
  
5.  **마이닝 모델** 테이블의 예측 가능한 열을 탭의 아래쪽에 있는 **원본** 열로 끌어 놓습니다. 필요에 따라 열에 대한 별칭을 입력할 수 있습니다.  
  
     예를 들어 **Bike Buyer** 를 **Source** 열로 끌어 놓습니다.  
  
6.  **원본** 열의 드롭다운 목록에서 **예측 함수** **사용자 지정 식** 을 선택하여 쿼리에 함수를 추가합니다.  
  
     예를 들어 **예측 함수**를 클릭하고 **PredictProbability**를 선택합니다.  
  
7.  **PredictProbability** 행의 **조건/인수** 를 클릭하고 예측할 열의 이름 및 예측할 특정 값(옵션)을 입력합니다.  
  
     예를 들어 **[Bike Buyer], 1**을 입력합니다.  
  
8.  **PredictProbability** 행의 **별칭** 상자를 클릭하고 새 열을 참조할 이름을 입력합니다.  
  
     예를 들어 **ProbableBuyer**과 같이 입력합니다.  
  
9. **마이닝 모델 예측** 탭의 도구 모음에서 **쿼리 결과 뷰로 전환** 을 클릭합니다.  
  
     새 화면이 열리고 쿼리 결과를 표시합니다. 방금 만든 DMX 문을 보려면 **SQL**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [예측 쿼리&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  

