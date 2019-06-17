---
title: 모델에 예측 함수 적용 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41c7c447af3eb7e0f40c10b98be827caa59867e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086139"
---
# <a name="apply-prediction-functions-to-a-model"></a>모델에 예측 함수 적용
  예측 쿼리를 만들려면 먼저 쿼리의 기반이 될 마이닝 모델을 선택해야 합니다. 현재 프로젝트에 있는 모든 마이닝 모델을 선택할 수 있습니다.  
  
 모델을 선택한 후에는 쿼리에 *예측 함수* 를 추가합니다. 예측 함수는 많은 용도로 예에 사용 되는 값을 예측할 수 있지만 예측을 생성 하는 데 사용 된 정보 뿐만 아니라 관련된 통계를 가져올 수도 있습니다를 이해 하는 가져오기 이며 예측 함수는 다음과 같은 유형의 값을 반환할 수 있습니다.  
  
-   예측 가능한 특성의 이름과 예측된 값  
  
-   예측된 값의 분포 및 편차에 대한 통계  
  
-   지정된 결과 또는 가능한 모든 결과의 확률  
  
-   최상위/최하위 점수 또는 값  
  
-   지정된 노드, 개체 또는 특성과 연관된 값  
  
 다양한 예측 함수를 사용할 수 있지만 작성한 모델의 유형에 적합한 함수를 선택해야 합니다. 일반적으로 함수 선택은 모델을 만드는 데 사용된 알고리즘에 따라 달라집니다.  
  
-   거의 모든 모델 유형에 대해 지원되는 예측 함수 목록은 [일반 예측 함수&#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)를 참조하세요.  
  
-   또한 개별 알고리즘에서 다양한 특수 함수를 지원합니다. 예를 들어 Microsoft 클러스터링 알고리즘을 기반으로 하는 마이닝 모델을 만드는 경우 특수 예측 함수를 사용하여 데이터 값에서 클러스터 중심까지의 거리와 같은 클러스터 관련 정보를 확인할 수 있습니다.  
  
     특정 유형의 마이닝 모델을 쿼리하는 방법에 대한 예제는 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](data-mining-algorithms-analysis-services-data-mining.md)에서 알고리즘 참조 항목을 참조하세요.  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>예측에 사용할 마이닝 모델 선택  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 모델을 마우스 오른쪽 단추로 클릭하고 **예측 쿼리 작성**을 선택합니다.  
  
     --또는--  
  
     [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **마이닝 모델 예측**탭을 클릭한 다음 **마이닝 모델** 테이블에서  **모델 선택** 을 클릭합니다.  
  
2.  **마이닝 모델 선택** 대화 상자에서 마이닝 모델을 선택한 다음 **확인**을 클릭합니다.  
  
     현재 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내의 모든 모델을 선택할 수 있습니다. 다른 데이터베이스의 모델을 사용하여 쿼리를 만들려면 해당 데이터베이스의 컨텍스트에서 새 쿼리 창을 열거나 해당 모델이 포함된 솔루션 파일을 열어야 합니다.  
  
### <a name="add-prediction-functions-to-a-query"></a>쿼리에 예측 함수 추가  
  
1.  **예측 쿼리 작성기**에서 **단일 쿼리 입력** 대화 상자에 값을 제공하거나 외부 데이터 원본에 모델을 매핑하여 예측에 사용할 입력 데이터를 구성합니다.  
  
     자세한 내용은 [예측 쿼리에 대한 입력 데이터 선택 및 매핑](choose-and-map-input-data-for-a-prediction-query.md)을 참조하세요.  
  
    > [!WARNING]  
    >  입력을 제공하지 않아도 예측을 생성할 수 있습니다. 입력이 없으면 일반적으로 알고리즘에서 가능한 모든 입력 중 가능성이 가장 높은 예측 값을 반환합니다.  
  
2.  **원본** 열을 클릭하고 목록에서 값을 선택합니다.  
  
    |||  
    |-|-|  
    |**\<모델 이름 >**|마이닝 모델의 값을 출력에 포함하려면 이 옵션을 선택합니다. 예측 가능한 열만 추가할 수 있습니다.<br /><br /> 모델에서 열을 추가하면 해당 열의 고유하지 않은 값 목록이 결과로 반환됩니다.<br /><br /> 이 옵션을 사용하여 추가한 열은 결과 DMX 문의 SELECT 부분에 포함됩니다.|  
    |**Prediction Function**|예측 함수 목록을 찾아보려면 이 옵션을 선택합니다.<br /><br /> 선택한 값 또는 함수는 결과 DMX 문의 SELECT 부분에 추가됩니다.<br /><br /> 예측 함수 목록은 선택한 모델 유형에 의해 제한되거나 필터링되지 않습니다. 따라서 함수가 현재 모델 유형에 대해 지원되는지 잘 모를 경우 해당 함수를 목록에 추가하고 오류가 발생하는지 확인하면 됩니다.<br /><br /> $가 앞에 오는 목록 항목(예: $AdjustedProbability)은 `PredictHistogram` 함수를 사용할 때의 출력인 중첩 테이블의 열을 나타냅니다. 이는 중첩 테이블이 아니라 단일 열을 반환하는 데 사용할 수 있는 간편한 방법입니다.|  
    |**사용자 지정 식**|사용자 지정 식을 입력한 다음 출력에 별칭을 할당하려면 이 옵션을 선택합니다.<br /><br /> 사용자 지정 식은 결과 DMX 예측 쿼리의 SELECT 부분에 추가됩니다.<br /><br /> 이 옵션은 각 행과 함께 출력 텍스트를 추가하거나, VB 함수를 호출하거나, 사용자 지정 저장 프로시저를 호출하려는 경우에 유용합니다.<br /><br /> DMX에서 VBA 및 Excel 함수를 사용하는 방법은 [MDX 및 DAX의 VBA 함수](/sql/mdx/vba-functions-in-mdx-and-dax)를 참조하세요.|  
  
3.  각 함수나 식을 추가한 후에는 DMX 뷰로 전환하여 함수가 DMX 문 내에 어떻게 추가되었는지를 확인합니다.  
  
    > [!WARNING]  
    >  예측 쿼리 작성기는 **결과**를 클릭할 때까지 DMX에 대한 유효성을 검사하지 않습니다. 쿼리 작성기에서 생성된 식이 유효한 DMX가 아닌 경우를 종종 발견하게 됩니다. 일반적으로 이는 예측 가능한 열과 관련되지 않은 열을 참조하거나 중첩 테이블에서 열을 예측(하위 SELECT 문이 필요함)하려는 경우에 발생합니다. 이제 DMX 뷰로 전환하여 문을 계속 편집할 수 있습니다.  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>예: 클러스터링 모델에서 쿼리 만들기  
  
1.  이 예제 쿼리를 작성하는 데 사용할 수 있는 클러스터링 모델이 없는 경우 [기본 데이터 마이닝 자습서](../../tutorials/basic-data-mining-tutorial.md)를 사용하여 [TM_Clustering] 모델을 만듭니다.  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [TM_Clustering] 모델을 마우스 오른쪽 단추로 클릭하고 **예측 쿼리 작성**을 선택합니다.  
  
3.  **마이닝 모델** 메뉴에서 **단일 쿼리**를 선택합니다.  
  
4.  **단일 쿼리 입력** 대화 상자에서 다음 값을 입력으로 설정합니다.  
  
    -   Gender = M  
  
    -   Commute Distance = 5-10 miles  
  
5.  표 형태 창에서 **원본**에 대해 TM_Clustering 마이닝 모델을 선택하고 [Bike Buyer] 열을 추가합니다.  
  
6.  에 대 한 **소스**를 선택 **예측 함수**에 함수를 추가 하 고 `Cluster`입니다.  
  
7.  에 대 한 **원본**를 선택 **예측 함수**, 함수를 추가 `PredictSupport`,으로 [Bike Buyer] 모델 열을 끌어서 합니다 **조건/인수** 상자입니다. **별칭** 열에 **Support** 를 입력합니다.  
  
     **조건/인수** 상자에서 예측 함수 및 열 참조를 나타내는 식을 복사합니다.  
  
8.  **원본**에 대해 **사용자 지정 식**을 선택하고 별칭을 입력한 후 다음 구문을 사용하여 Excel CEILING 함수를 참조합니다.  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     열 참조를 함수의 인수로 붙여넣습니다.  
  
     예를 들어 다음 식은 지원 값의 CEILING을 반환합니다.  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     **별칭** 열에 CEILING을 입력합니다.  
  
9. **쿼리 텍스트 뷰로 전환** 을 클릭하여 생성된 DMX 문을 검토한 다음 **쿼리 결과 뷰로 전환** 을 클릭하여 예측 쿼리에서 출력된 열을 확인합니다.  
  
     다음 표에는 예상 결과가 나와 있습니다.  
  
    |Bike Buyer|$Cluster|SUPPORT|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|클러스터 8|954|953.948638926372|  
  
 문에 절을 다른 곳에서 추가 하려는 경우-예를 들어, WHERE 절을 추가 하려는 경우-; 표를 사용 하 여 추가할 수 없습니다 먼저 DMX 뷰로 전환 해야 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 쿼리](data-mining-queries.md)  
  
  
