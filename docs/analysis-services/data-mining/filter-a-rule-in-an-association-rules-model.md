---
title: "필터 규칙에 연결 규칙 모델 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- filtering rules [Analysis Services]
- Mining Model Viewer [Analysis Services], rules
- Rules Viewer
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 88eb75188ed36a8a79178f6b893c5301ffd2d47e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="filter-a-rule-in-an-association-rules-model"></a>연결 규칙 모델에서 규칙 필터링
  연결 모델에 필터링을 사용하여 보고자 하는 연결로만 결과를 제한할 수 있습니다. 예를 들어 특정 제품이 포함된 규칙만 표시하도록 규칙을 필터링할 수 있습니다.  
  
 데이터 마이닝 디자이너에서는 **연결 규칙 뷰어의** 규칙 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 탭의 컨트롤을 사용하여 표시되는 규칙을 필터링할 수 있습니다.  또한 모델에 쿼리를 만들어 특정 값이 포함된 항목 집합만 표시할 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 Microsoft 연결 알고리즘을 사용하여 만든 마이닝 모델에만 사용할 수 있습니다.  
  
### <a name="filter-a-rule-in-an-association-model"></a>연결 모델에서 규칙 필터링  
  
1.  **연결 규칙 뷰어**를 사용하여 마이닝 모델을 엽니다. SQL Server Management Studio에서 마이닝 모델을 열려면 모델 이름을 마우스 오른쪽 단추로 클릭하고 **찾아보기**를 선택합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 마이닝 모델을 열려면 모델이 들어 있는 마이닝 구조를 두 번 클릭한 다음 **데이터 마이닝 디자이너** 의 **마이닝 모델 뷰어**탭을 클릭합니다.  
  
2.  **연결 규칙 뷰어** 에서 **규칙**탭을 클릭합니다.  
  
3.  **규칙 필터** 상자에 규칙 조건을 입력합니다. 예를 들어 "Bike Stand"와 같은 규칙 조건을 입력합니다. 이 규칙 조건은 "Bike Stands"도 반환합니다.  
  
     **규칙 필터** 입력란에는 .NET 언어에서 정의하는 정규식을 입력할 수 있습니다. 따라서 `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))`와 같은 식을 사용할 수 있습니다. 이 식은 순서에 관계없이 Helmets와 Fenders라는 단어가 있는 특성이 포함된 모든 항목 집합을 반환합니다.  
  
4.  **최소 확률**에서 결과 규칙 수를 줄이려면 확률 값을 늘리고 결과 규칙 수를 늘리려면 확률 값을 줄입니다.  
  
5.  **최소 중요도**에서 결과 규칙 수를 줄이려면 중요도 값을 늘리고 결과 규칙 수를 늘리려면 중요도 값을 줄입니다.  
  
6.  **표시**에서 **특성 이름 및 값 표시**, **특성 이름만 표시**또는 **특성 값만 표시**옵션 중 하나를 선택합니다.  
  
7.  **최대 행 수**에서 지정한 조건을 만족하는 총 규칙 수를 늘리려면 값을 늘리고 반환되는 규칙 수를 제한하려면 값을 줄입니다. 확률을 기준으로 규칙이 정렬되므로 확률 또는 중요도에 대해 지정한 조건을 만족하는 추가 규칙을 제거할 수도 있습니다.  
  
8.  규칙 이름의 표시 방법을 전환하려면 **긴 이름 표시** 확인란을 선택하거나 취소합니다.  
  
     이렇게 하면 규칙이 필터링되어 지정한 항목을 포함하는 규칙만 표시됩니다. 필터 조건은 규칙 구분자("->") 앞이나 뒤에 있는 특성 값에 적용됩니다.  
  
    > [!NOTE]  
    >  뷰어에서는 마이닝 모델에 대한 쿼리를 기준으로 초기 규칙 목록을 캐시하며 최대 행 수, 확률, 중요도 또는 긴 이름 표시 옵션을 설정하여 쿼리 조건을 변경하지 않는 한 이 규칙 목록을 새로 고치지 않습니다. 따라서 조건을 입력했는데 화면이 곧바로 새로 고쳐지지 않으면 **긴 이름 표시** 확인란을 선택한 다음 선택을 취소하여 뷰어의 데이터를 새로 고칠 수 있습니다.  
  
### <a name="create-a-query-on-the-itemsets-in-an-association-model"></a>연결 모델의 항목 집합에 대한 쿼리 만들기  
  
-   [연결 모델 쿼리 예제](../../analysis-services/data-mining/association-model-query-examples.md)  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 모델 뷰어 태스크 및 방법](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 연결 규칙 뷰어를 사용 하 여 모델 찾아보기](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [3 단원: 시장 바구니 시나리오 &#40; 중급 데이터 마이닝 자습서 &#41; 구축](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)  
  
  

