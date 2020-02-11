---
title: 연결 예측 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bee5ca4ded1b2fd5cbda0712cb766c825b9d0318
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62472848"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>연결 예측(중급 데이터 마이닝 자습서)
  모델이 처리되면 모델에 저장된 연결 정보를 사용하여 예측을 만들 수 있습니다. 이 단원의 마지막 태스크에서는 만든 연결 모델에 대해 예측 쿼리를 작성하는 방법에 대해 설명합니다. 이 단원에서는 사용자가 예측 쿼리 작성기를 사용하는 방법에 익숙하며 연결 모델에 대해 예측 쿼리를 작성하는 방법을 알아보려 한다고 가정합니다. 예측 쿼리 작성기를 사용 하는 방법에 대 한 자세한 내용은 [데이터 마이닝 쿼리 인터페이스](../../2014/analysis-services/data-mining/data-mining-query-tools.md)를 참조 하세요.  
  
## <a name="creating-a-singleton-prediction-query"></a>단일 예측 쿼리 만들기  
 연결 모델에 대한 예측 쿼리는 매우 유용할 수 있습니다.  
  
-   이전 또는 관련 구매에 따라 고객에게 항목을 권장합니다.  
  
-   관련된 이벤트를 찾습니다.  
  
-   트랜잭션 집합에서 관계를 식별합니다.  
  
 예측 쿼리를 작성하려면 먼저 사용하려는 연결 모델을 선택한 다음 입력 데이터를 지정합니다. 값 목록과 같은 외부 데이터 원본에서 입력 값을 가져오거나, 단일 쿼리를 작성하여 필요할 때마다 값을 제공할 수 있습니다.  
  
 이 시나리오에서는 예측의 동작 방식을 알아보기 위해 먼저 몇 가지 단일 예측 쿼리를 만듭니다. 그런 다음 고객의 현재 구매 항목을 기반으로 권장 사항을 만드는 데 사용할 수 있는 일괄 처리 예측을 위한 쿼리를 만듭니다.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>연결 모델에 대한 예측 쿼리를 만들려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델 예측** 탭을 클릭 합니다.  
  
2.  **마이닝 모델** 창에서 **모델 선택**을 클릭 합니다. 올바른 모델이 이미 선택되어 있는 경우 이 단계와 다음 단계를 건너뛸 수 있습니다.  
  
3.  **마이닝 모델 선택** 대화 상자에서 마이닝 구조 **연결**을 나타내는 노드를 확장 하 고 모델 **연결**을 선택 합니다. **확인**을 클릭합니다.  
  
     여기서는 입력 창을 무시합니다.  
  
4.  표에서 **원본** 아래의 빈 셀을 클릭 하 고 **예측 함수를 선택 합니다.** **필드**아래의 셀에서를 선택 `PredictAssociation`합니다.  
  
     또한 **predict** 함수를 사용 하 여 연결을 예측할 수 있습니다. 이 경우 테이블 열을 인수로 사용 하는 **Predict** 함수 버전을 선택 해야 합니다.  
  
5.  **마이닝 모델** 창에서 중첩 테이블 `vAssocSeqLineItems`을 선택 하 여 표 형태의 `PredictAssociation` 함수에 대 한 **조건/인수** 상자로 끌어다 놓습니다.  
  
     테이블 및 열 이름을 끌어다 놓으면 구문 오류 없이 복잡한 문을 작성할 수 있습니다. 그러나이 `PredictAssociation` 함수는 함수에 대 한 다른 선택적 인수를 포함 하는 셀의 현재 내용을 대체 합니다. 다른 인수를 보려면 참조를 위해 임시로 함수의 두 번째 인스턴스를 표에 추가합니다.  
  
6.  **조건/인수** 상자를 클릭 하 고 테이블 이름 뒤에 다음 텍스트를 입력 합니다.`,3`  
  
     **조건/인수** 상자의 전체 텍스트는 다음과 같아야 합니다.  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  예측 쿼리 작성기 위쪽 모퉁이에 있는 **결과** 단추를 클릭 합니다.  
  
 예상 결과에는 머리글 **식이**포함 된 단일 열이 포함 됩니다. **식** 열에는 단일 열이 있는 중첩 테이블 및 다음 세 개의 행이 포함 됩니다. 입력 값을 지정하지 않았으므로 이러한 예측은 전체 모델에 대해 가능성이 가장 높은 제품 연결을 나타냅니다.  
  
|모델|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 다음에는 **단일 쿼리 입력** 창을 사용 하 여 제품을 쿼리에 대 한 입력으로 지정 하 고 해당 항목과 연결 될 가능성이 가장 높은 제품을 확인 합니다.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>중첩 테이블 입력을 사용하여 단일 예측 쿼리를 만들려면  
  
1.  예측 쿼리 작성기의 모퉁이에 있는 **디자인** 단추를 클릭 하 여 쿼리 작성 표로 다시 전환 합니다.  
  
2.  **마이닝 모델** 메뉴에서 **단일 쿼리**를 선택 합니다.  
  
3.  **마이닝 모델** 대화 상자에서 **연결** 모델을 선택 합니다.  
  
4.  표에서 **원본** 아래의 빈 셀을 클릭 하 고 **예측 함수를 선택 합니다.** **필드**아래의 셀에서를 선택 `PredictAssociation`합니다.  
  
5.  **마이닝 모델** 창에서 중첩 테이블 `vAssocSeqLineItems`을 선택 하 여 표 형태의 `PredictAssociation` 함수에 대 한 **조건/인수** 상자로 끌어다 놓습니다. 이전 `,3` 절차에서와 같이 중첩 테이블 이름 뒤에를 입력 합니다.  
  
6.  **단일 쿼리 입력** 대화 상자에서 **vassoc Seq Line Items**옆의 **값** 상자를 클릭 한 다음 **(...)** 단추를 클릭 합니다.  
  
7.  **중첩 테이블 입력** 대화 상자의 **키 열** 창에서 `Touring Tire` 를 선택한 다음 **추가**를 클릭 합니다.  
  
8.  **결과** 단추를 클릭 합니다.  
  
 이제 결과에 Touring Tire와 연결될 가능성이 가장 높은 제품에 대한 예측이 표시됩니다.  
  
|모델|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 그러나 모델 탐색을 통해 Touring Tire와 함께 Touring Tire Tube가 구매되는 경우가 많음을 이미 알고 있으므로 이러한 항목을 함께 구매하는 고객에게 권장할 수 있는 제품을 확인할 필요가 있습니다. 이에 따라 바구니에 있는 두 항목을 기반으로 관련 제품이 예측되도록 쿼리를 변경하고 예측된 각 제품에 대한 확률이 추가되도록 쿼리를 수정합니다.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>단일 예측 쿼리에 입력 및 확률을 추가하려면  
  
1.  예측 쿼리 작성기의 모퉁이에 있는 **디자인** 단추를 클릭 하 여 쿼리 작성 표로 다시 전환 합니다.  
  
2.  **단일 쿼리 입력** 대화 상자에서 **vassoc Seq Line Items**옆의 **값** 상자를 클릭 한 다음 **(...)** 단추를 클릭 합니다.  
  
3.  **키 열** 창에서을 선택 `Touring Tire`하 고 **추가**를 클릭 합니다.  
  
4.  표에서 **원본** 아래의 빈 셀을 클릭 하 고 **예측 함수를 선택 합니다.** **필드**아래의 셀에서를 선택 `PredictAssociation`합니다.  
  
5.  **마이닝 모델** 창에서 중첩 테이블 `vAssocSeqLineItems`을 선택 하 여 표 형태의 `PredictAssociation` 함수에 대 한 **조건/인수** 상자로 끌어다 놓습니다. 이전 `,3` 절차에서와 같이 중첩 테이블 이름 뒤에를 입력 합니다.  
  
6.  **중첩 테이블 입력** 대화 상자의 **키 열** 창에서 `Touring Tire Tube` 를 선택한 다음 **추가**를 클릭 합니다.  
  
7.  표의 `PredictAssociation` 함수 행에서 **조건/인수** 상자를 클릭 하 고 인수를 변경 하 여 INCLUDE_STATISTICS 인수를 추가 합니다.  
  
     **조건/인수** 상자의 전체 텍스트는 다음과 같아야 합니다.  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  **결과** 단추를 클릭 합니다.  
  
 이제 중첩 테이블의 결과가 변경되어 예측과 함께 지원 및 확률이 표시됩니다. 이러한 값을 해석 하는 방법에 대 한 자세한 내용은 [연결 모델에 대 한 마이닝 모델 콘텐츠 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)를 참조 하세요.  
  
|모델|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291 ...|0.252 ...|  
|Water Bottle|2866|0.192 ...|0.175 ...|  
|Patch Kit|2113|0.142 ...|0.132|  
  
## <a name="working-with-results"></a>결과 작업  
 결과에 중첩 테이블이 많이 있는 경우 결과를 보다 쉽게 볼 수 있도록 평면화할 수 있습니다. 이렇게 하려면 수동으로 쿼리를 수정하고 `FLATTENED` 키워드를 추가합니다.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>예측 쿼리에서 중첩 행 집합을 평면화하려면  
  
1.  예측 쿼리 작성기의 모서리에 있는 **SQL** 단추를 클릭 합니다.  
  
     표가 열린 창으로 변경됩니다. 이 창에서는 예측 쿼리 작성기에서 만든 DMX 문을 보고 수정할 수 있습니다.  
  
2.  
  `SELECT` 키워드 다음에 `FLATTENED`를 입력합니다.  
  
     쿼리의 전체 텍스트가 다음과 같아야 합니다.  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  예측 쿼리 작성기 위쪽 모퉁이에 있는 **결과** 단추를 클릭 합니다.  
  
 수동으로 쿼리를 편집한 후에는 디자인 뷰로 다시 전환하면 변경 내용이 손실됩니다. 쿼리를 저장하려면 수동으로 만든 DMX 문을 텍스트 파일에 복사합니다. 디자인 뷰로 다시 변경하면 쿼리가 디자인 뷰에서 유효했던 마지막 버전으로 되돌려집니다.  
  
## <a name="creating-multiple-predictions"></a>여러 예측 만들기  
 이전 구매 항목을 기반으로 개별 고객에 대한 최상의 예측 정보를 얻으려 한다고 가정하면 고객 ID 및 가장 최근 구매한 제품을 포함하는 테이블과 같은 외부 데이터를 예측 쿼리에 대한 입력으로 사용할 수 있습니다. 이때 데이터 테이블은 이미 Analysis Services 데이터 원본 뷰로 정의되어 있어야 하며 입력 데이터에 모델에 사용된 것과 같은 사례 및 중첩 테이블이 있어야 합니다. 이름은 같을 필요가 없지만 구조는 비슷해야 합니다. 이 자습서에서는 모델이 학습된 원래 테이블을 사용합니다.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>예측 쿼리에 대한 입력 방법을 변경하려면  
  
1.  **마이닝 모델** 메뉴에서 **단일 쿼리** 를 다시 선택 하 여 확인 표시를 지웁니다.  
  
2.  단일 쿼리가 손실된다는 오류 메시지가 나타납니다. **예**를 클릭합니다.  
  
     입력 대화 상자의 이름이 **입력 테이블 선택**으로 변경 됩니다.  
  
 고객 ID 및 제품 목록을 입력으로 제공하는 예측 쿼리를 만들려고 하기 때문에 고객 테이블을 사례 테이블로 추가하고 구매 테이블은 중첩 테이블로 추가합니다. 그런 다음 권장 사항을 만드는 예측 함수를 추가합니다.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>중첩 테이블 입력을 사용하여 예측 쿼리를 만들려면  
  
1.  마이닝 모델 창에서 Association Filtered 모델을 선택합니다.  
  
2.  **입력 테이블 선택** 대화 상자에서 **사례 테이블 선택**을 클릭 합니다.  
  
3.  **테이블 선택** 대화 상자에서 **데이터 원본**에 대해 AdventureWorksDW2008를 선택 합니다. **테이블/뷰 이름** 목록에서 vAssocSeqOrders를 선택 하 고 **확인**을 클릭 합니다.  
  
     창에 vAssocSeqOrders 테이블이 추가됩니다.  
  
4.  **입력 테이블 선택** 대화 상자에서 **중첩 테이블 선택**을 클릭 합니다.  
  
5.  **테이블 선택** 대화 상자에서 **데이터 원본**에 대해 AdventureWorksDW2008를 선택 합니다. **테이블/뷰 이름** 목록에서 vAssocSeqLineItems를 선택 하 고 **확인**을 클릭 합니다.  
  
     창에 vAssocSeqLineItems 테이블이 추가됩니다.  
  
6.  **중첩 조인 지정** 대화 상자에서 ordernumber 필드를 사례 테이블에서 끌어 중첩 테이블의 ordernumber 필드에 놓습니다.  
  
     **관계 추가** 를 클릭 하 고 목록에서 열을 선택 하 여 관계를 만들 수도 있습니다.  
  
7.  **관계 지정** 대화 상자에서 ordernumber 필드가 올바르게 매핑되는지 확인 한 다음 **확인**을 클릭 합니다.  
  
8.  **확인** 을 클릭 하 여 **중첩 조인 지정** 대화 상자를 닫습니다.  
  
     디자인 창에서 사례 및 중첩 테이블이 업데이트되어 모델의 열과 외부 데이터 열을 연결하는 조인이 표시됩니다. 관계가 잘못 된 경우 조인 선을 마우스 오른쪽 단추로 클릭 하 고 **연결 수정** 을 선택 하 여 열 매핑을 편집 하거나 조인 선을 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 선택 하 여 관계를 완전히 제거할 수 있습니다.  
  
9. 표에 새 행을 추가합니다. **원본**에 대해 **vAssocSeqOrders 테이블**을 선택 합니다. **필드**에 대해 customerkey를 선택 합니다.  
  
10. 표에 새 행을 추가합니다. **원본**에 대해 **vAssocSeqOrders 테이블**을 선택 합니다. **필드**에 대해 지역을 선택 합니다.  
  
11. 표에 새 행을 추가합니다. **원본**에 대해 **예측 함수**를 선택 하 고 **필드**에 대해 `PredictAssociation`를 선택 합니다.  
  
12. VAssocSeqLineItems을 `PredictAssociation` 행의 **조건/인수** 상자로 끕니다. **조건/인수** 상자의 끝을 클릭 하 고 다음 텍스트를 입력 합니다.`INCLUDE_STATISTICS,3`  
  
     **조건/인수** 상자의 전체 텍스트는 다음과 같아야 합니다.`[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. **결과** 단추를 클릭 하 여 각 고객에 대 한 예측을 봅니다.  
  
 여러 모델에 대해 비슷한 예측 쿼리를 만들어 필터링으로 예측 결과가 변경되는지 여부를 확인할 수 있습니다. 예측 및 다른 쿼리 유형을 만드는 방법에 대 한 자세한 내용은 [연결 모델 쿼리 예제](../../2014/analysis-services/data-mining/association-model-query-examples.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [연결 모델에 대 한 마이닝 모델 콘텐츠 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)   
 [예측 쿼리 작성기를 사용하여 예측 쿼리 만들기](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
