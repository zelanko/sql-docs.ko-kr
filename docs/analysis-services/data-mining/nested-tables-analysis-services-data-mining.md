---
title: "중첩 테이블 (Analysis Services-데이터 마이닝) | Microsoft Docs"
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
- data mining [Analysis Services], nested tables
- tables [Analysis Services], nested
- nested tables
ms.assetid: cb192aa2-597e-4d4f-ac34-3556d037fed4
caps.latest.revision: 52
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ad436f2cfa5da5381ad683a1fc804468c5a40d3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="nested-tables-analysis-services---data-mining"></a>중첩 테이블(Analysis Services - 데이터 마이닝)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 데이터가 사례 테이블에 포함된 일련의 사례로 데이터 마이닝 알고리즘에 공급되어야 합니다. 그러나 한 개의 데이터 행으로 설명할 수 없는 사례도 있습니다. 예를 들어 한 사례가 두 테이블, 즉 고객 정보가 포함된 한 테이블과 고객 구매 내용이 포함된 다른 테이블에서 파생될 수 있습니다. 고객 정보 테이블의 단일 고객이 고객 구매 테이블에서 여러 항목을 가질 수 있으므로 단일 행을 사용하여 데이터를 설명하기 어렵습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 *중첩 테이블*을 사용하여 이러한 사례를 처리하는 고유한 방법을 제공합니다. 다음 그림에서는 중첩 테이블의 개념을 보여 줍니다.  
  
 ![중첩된 테이블을 사용 하 여 두 테이블 결합](../../analysis-services/data-mining/media/nested-tables.gif "중첩된 테이블을 사용 하 여 두 테이블 결합")  
  
 이 다이어그램에서 부모 테이블인 첫 번째 테이블에는 고객 정보가 들어 있으며 각 고객의 고유 식별자와 연결됩니다. 자식 테이블인 두 번째 테이블에는 각 고객의 구매 내용이 들어 있습니다. 자식 테이블의 구매 내용은 고유 식별자인 **CustomerKey** 열에 의해 부모 테이블에 연결됩니다. 다이어그램의 세 번째 테이블은 결합된 두 테이블을 보여 줍니다.  
  
 중첩 테이블은 **TABLE**데이터 형식을 갖는 특수 열로 사례 테이블에 표시됩니다. 이러한 종류의 열은 특정 사례 행에 대해 부모 테이블과 관련된 자식 테이블에서 선택한 행을 포함합니다.  
  
 중첩된 테이블의 데이터는 예측이나 입력 또는 둘 다에 사용할 수 있습니다. 예를 들어 모델에 두 개의 중첩된 테이블 열이 있을 수 있으며 이 중 하나의 중첩된 테이블 열에는 고객이 구매한 제품의 목록이 포함되어 있고 다른 하나의 중첩된 테이블 열에는 설문 조사를 통해 얻은 고객의 취미와 관심사에 대한 정보가 포함되어 있을 수 있습니다. 이 시나리오에서 고객의 취미와 관심사를 입력으로 사용하여 구매 행동을 분석하고 구매할 가능성이 높은 제품을 예측할 수 있습니다.  
  
## <a name="joining-case-tables-and-nested-tables"></a>사례 테이블 및 중첩 테이블 조인  
 중첩 테이블을 만들려면 한 테이블의 항목이 다른 테이블에 연결될 수 있도록 두 원본 테이블이 정의된 관계를 포함해야 합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서는 데이터 원본 뷰에서 이러한 관계를 정의할 수 있습니다.  
  
> [!NOTE]  
>  **CustomerKey** 필드는 데이터 원본 뷰 정의 내에서 사례 테이블과 중첩 테이블을 연결하고 마이닝 구조 내에서 열의 관계를 설정하는 데 사용되는 관계형 키입니다. 그러나 일반적으로 해당 구조에서 만들어진 마이닝 모델에는 이 관계형 키를 사용해서는 안 됩니다. 관계형 키 열이 테이블 조인을 위한 목적으로만 사용되어 분석에 유용한 정보를 제공하지 않는 경우 마이닝 모델에서 관계형 키 열을 생략하는 것이 가장 좋습니다.  
  
 DMX(Data Mining Extensions) 또는 AMO(Analysis Management Objects)를 사용하여 프로그래밍 방식으로 중첩 테이블을 만들거나 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 데이터 마이닝 마법사 및 데이터 마이닝 디자이너를 사용할 수 있습니다.  
  
## <a name="using-nested-table-columns-in-a-mining-model"></a>마이닝 모델에서 중첩 테이블 열 사용  
 사례 테이블에서 키는 종종 고객 ID, 제품 이름 또는 계열의 날짜와 같이 테이블의 행을 고유하게 식별하는 데이터를 나타냅니다. 을 사용하여 이러한 사례를 처리하는 고유한 방법을 제공합니다. 그러나 중첩 테이블에서 키는 일반적으로 관계형 키(외래 키)가 아니라 모델링하고 있는 특성을 나타내는 열입니다.  
  
 예를 들어 사례 테이블에 주문이 포함되어 있고 중첩 테이블에 주문 항목이 포함되어 있는 경우 사례 테이블에 저장되어 있는 여러 개의 주문에서 중첩 테이블에 저장된 항목 간의 관계를 모델링하고자 할 수 있습니다. 따라서 관계형 키 **OrderID** 에 의해 **Items** 중첩 테이블이 **Orders**사례 테이블에 조인되었더라도 **OrderID** 를 중첩 테이블 키로 사용해서는 안 됩니다. 대신 **Items** 열을 중첩 테이블 키로 선택해야 합니다. 왜냐하면 이 열에는 모델링하려는 데이터가 포함되어 있기 때문입니다. 대부분의 경우 사례 테이블과 중첩 테이블 간의 관계가 데이터 원본 뷰 정의에 의해 이미 설정되어 있으므로 마이닝 모델에서 **OrderID** 를 무시해도 괜찮습니다.  
  
 중첩 테이블 키로 사용할 열을 선택할 때 해당 열의 값은 각 사례에 대해 고유해야 합니다. 예를 들어 사례 테이블은 고객을 나타내고 중첩 테이블은 고객이 구매한 항목을 나타낼 경우 고객 한 명당 항목이 한 번만 나열되어야 합니다. 한 고객이 같은 항목을 두 번 이상 구매한 경우 각 제품에 대한 구매 수를 집계하는 열이 포함된 다른 뷰를 만들 수도 있습니다.  
  
 중첩 테이블에서 중복 값을 처리하는 방법은 만들고 있는 마이닝 모델과 해결 중인 비즈니스 문제에 따라 달라집니다. 일부 시나리오에서는 고객이 특정 제품을 구매한 횟수보다는 한 번 이상의 구매가 있었는지만 확인하고자 할 수 있습니다. 다른 시나리오에서는 구매 수량과 순서가 매우 중요할 수 있습니다.  
  
 항목 순서가 중요한 경우 순서를 나타내는 열이 추가로 필요할 수 있습니다. 시퀀스 클러스터링 알고리즘을 사용하여 모델을 만드는 경우 항목의 순서를 나타내는 *KEY SEQUENCE* 열을 추가로 선택해야 합니다. KEY SEQUENCE 열은 시퀀스 클러스터링 모델에만 사용되는 특별한 종류의 중첩 키로 고유한 숫자 데이터 형식을 필요로 합니다. 예를 들어 정수와 날짜 모두 KEY SEQUENCE 열로 사용할 수 있지만 모든 시퀀스 값은 고유해야 합니다. KEY SEQUENCE 열 이외에도 시퀀스 클러스터링 모델에는 구매한 제품과 같이 모델링되고 있는 특성을 나타내는 중첩 테이블 키도 있습니다.  
  
### <a name="using-non-key-nested-columns-from-a-nested-table"></a>중첩 테이블에서 키가 아닌 중첩 열 사용  
 사례 테이블과 중첩 테이블 간의 조인을 정의하고 중첩 테이블 키로 사용할 관심 있는 고유 특성이 포함된 열을 선택한 후에는 중첩 테이블의 다른 열을 포함시켜 모델에 대한 입력으로 사용할 수 있습니다. 중첩 테이블의 모든 열은 입력, 예측 및 입력 또는 예측용으로 사용할 수 있습니다.  
  
 예를 들어 중첩 테이블에 **Product**, **ProductQuantity**및 **ProductPrice**열이 포함되어 있는 경우 **Product** 는 중첩 테이블 키로 선택하고 **ProductQuantity** 는 마이닝 구조에 추가하여 입력으로 사용할 수 있습니다.  
  
## <a name="filtering-nested-table-data"></a>중첩 테이블 데이터 필터링  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 데이터 마이닝 모델 학습 또는 테스트에 사용되는 데이터에 대한 필터를 만들 수 있습니다. 필터를 사용하여 모델 컴퍼지션에 영향을 주거나 사례 하위 집합에서 모델을 테스트할 수 있습니다. 필터를 중첩 테이블에 적용할 수도 있습니다. 그러나 중첩 테이블에서 사용할 수 있는 구문에는 제한이 있습니다.  
  
 대개 특성의 존재 여부를 테스트할 때 필터를 중첩 테이블에 적용합니다. 예를 들어 모델에 사용된 사례를 중첩 테이블에 지정된 값을 갖는 사례로 제한하는 필터를 적용할 수 있습니다. 또는 모델에 사용된 사례를 특정 항목을 구매하지 않은 고객으로 제한할 수도 있습니다.  
  
 중첩 테이블에 필터를 만들 때 보다 큼 또는 보다 작음과 같은 연산자를 사용할 수도 있습니다. 예를 들어 모델에 사용된 사례를 대상 제품을 n개 이상 구매한 고객으로 제한할 수 있습니다. 중첩 테이블 특성 필터링 기능을 사용하면 모델을 보다 유연하게 사용자 지정할 수 있습니다.  
  
 모델 필터를 만들고 사용하는 방법은 [마이닝 모델에 대한 필터&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  

