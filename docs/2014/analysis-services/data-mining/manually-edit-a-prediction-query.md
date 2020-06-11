---
title: 예측 쿼리 수동 편집 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8809e025a60a47acb2db5dae312702ee2e3effd3
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522089"
---
# <a name="manually-edit-a-prediction-query"></a>예측 쿼리 수동 편집
  예측 쿼리 작성기를 사용하여 쿼리를 디자인한 후에는 데이터 마이닝 디자이너의 **마이닝 모델 예측** 의 탭에서 쿼리 텍스트 보기로 전환하여 해당 쿼리를 수정할 수 있습니다. 쿼리 작성기가 만든 쿼리를 표시할 텍스트 편집기가 화면 맨 아래에 나타납니다.  
  
 쿼리 텍스트 보기로 전환은 쿼리에 항목을 추가하는 데 유용합니다. 예를 들어 WHERE 절 또는 ORDER BY 절을 추가할 수 있습니다.  
  
 예측 쿼리 작성기의 표를 사용하여 개체 및 열 이름을 삽입하고 개별 예측 함수의 구문을 설정한 다음 수동 편집 모드로 전환하여 매개 변수 값을 변경할 수 있습니다.  
  
> [!NOTE]  
>  **쿼리 텍스트** 뷰에서 **디자인** 뷰로 다시 전환하면 **쿼리 텍스트** 뷰에서 변경한 내용이 모두 손실됩니다.  
  
### <a name="modify-a-query"></a>쿼리 수정  
  
1.  **의 데이터 마이닝 디자이너에 있는** 마이닝 모델 예측 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]탭에서 **SQL**을 클릭합니다.  
  
     화면 맨 아래의 표가 쿼리를 포함하는 텍스트 편집기로 바뀝니다. 이 편집기에서 쿼리 변경 내용을 입력할 수 있습니다.  
  
2.  쿼리를 실행하려면 **마이닝 모델** 메뉴에서 **결과**를 선택하거나 단추를 클릭하여 쿼리 결과로 전환합니다.  
  
    > [!NOTE]  
    >  만든 쿼리가 유효하지 않을 경우 결과 창에 오류도 표시되지 않고 결과도 표시되지 않습니다. **디자인** 단추를 클릭하거나 **마이닝 모델** 메뉴에서 **디자인** 또는 **쿼리** 를 선택하여 문제를 해결하고 쿼리를 다시 실행하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 쿼리](data-mining-queries.md)   
 [예측 쿼리 작성기 &#40;데이터 마이닝&#41;](../prediction-query-builder-data-mining.md)   
 [6단원: 예측 만들기 및 작업&#40;기본 데이터 마이닝 자습서&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
  
