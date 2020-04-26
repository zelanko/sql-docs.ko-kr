---
title: 중첩 테이블이 있는 데이터 원본 뷰 추가 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62822783"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>중첩 테이블이 있는 데이터 원본 뷰 추가(중급 데이터 마이닝 자습서)
  시장 바구니 모델을 만들려면 연관 데이터를 지원하는 데이터 원본 뷰를 사용해야 합니다. 이 데이터 원본 뷰는 시퀀스 클러스터링 시나리오에도 사용됩니다.  
  
 이 데이터 원본 뷰는 *중첩 테이블*을 포함 하기 때문에 사용 된 것과 다른 다른 데이터 원본 뷰를 사용 합니다. *중첩 테이블* 은 사례 테이블의 단일 행에 대 한 여러 행의 정보를 포함 하는 테이블입니다. 예를 들어 모델에서 고객의 구매 동작을 분석하는 경우 일반적으로 각 고객에 대한 고유 행이 있는 테이블을 사례 테이블로 사용합니다. 그러나 각 고객이 여러 제품을 구매할 수 있으며 이 경우 구매 순서 또는 함께 구매되는 빈도가 높은 제품을 분석할 수 있습니다. 모델에서 이러한 구매를 논리적으로 나타내려면 각 고객에 대한 구매를 나열하는 데이터 원본 뷰에 다른 테이블을 추가합니다.  
  
 이 중첩 구매 테이블은 고객 테이블과 다 대 일 관계로 관련됩니다. 중첩 테이블에 각 고객에 대한 행이 많이 포함될 수 있습니다. 구매한 단일 제품을 포함하는 각 행에는 구매가 이루어진 주문, 주문 시 가격 또는 해당 제품에 대해 수행된 모든 홍보에 대한 추가 정보가 포함될 수 있습니다. 중첩 테이블에 있는 정보를 모델에 대한 입력 또는 예측 가능한 특성으로 사용할 수 있습니다.  
  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   데이터 원본에 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터 원본 뷰를 추가 합니다.  
  
-   사례 및 중첩 테이블을 이 뷰에 추가합니다.  
  
-   사례 및 중첩 테이블 간에 다 대 일 관계를 지정합니다.  
  
    > [!NOTE]  
    >  . 사례 테이블과 중첩 테이블 간의 관계를 올바르게 지정하고 모델을 처리할 때 오류를 피하려면 설명된 절차를 정확하게 따르는 것이 중요합니다.  
  
-   모델에서 데이터 열이 사용되는 방법을 정의합니다.  
  
 사례 및 중첩 테이블 작업에 대 한 자세한 내용 및 중첩 테이블 키를 선택 하는 방법에 대 한 자세한 내용은 [중첩 테이블 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)를 참조 하세요.  
  
### <a name="to-add-a-data-source-view"></a>데이터 원본 뷰를 추가하려면  
  
1.  솔루션 탐색기에서 **데이터 원본 뷰**를 마우스 오른쪽 단추로 클릭 한 다음 **새 데이터 원본 뷰**를 선택 합니다.  
  
     데이터 원본 뷰 마법사가 열립니다.  
  
2.  **데이터 원본 뷰 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **데이터 원본 선택** 페이지의 **관계형 데이터 원본**아래에서 기본 데이터 마이닝 자습서에서 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 만든 데이터 원본을 선택 합니다. **다음**을 클릭합니다.  
  
4.  **테이블 및 뷰 선택** 페이지에서 다음 테이블을 선택 하 고 오른쪽 화살표를 클릭 하 여 새 데이터 원본 뷰에 포함 합니다.  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  **다음**을 클릭합니다.  
  
6.  **마법사 완료** 페이지에서는 기본적으로 데이터 원본 뷰의 이름이로 지정 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]됩니다. 이름을로 `Orders`변경 하 고 **마침**을 클릭 합니다.  
  
     데이터 원본 뷰 디자이너가 열리고 `Orders` 데이터 원본 뷰가 나타납니다.  
  
### <a name="to-create-a-relationship-between-tables"></a>테이블 간에 관계를 만들려면  
  
1.  데이터 원본 뷰 디자이너에서 테이블이 가로로 정렬되어 왼쪽에는 vAssocSeqLineItems 테이블이, 오른쪽에는 vAssocSeqOrders 테이블이 있도록 두 테이블을 배치합니다.  
  
2.  VAssocSeqLineItems 테이블에서 **Ordernumber** 열을 선택 합니다.  
  
3.  열을 vAssocSeqOrders 테이블로 끌어 **Ordernumber** 열에 놓습니다.  
  
    > [!IMPORTANT]  
    >  조인의 다를 나타내는 vAssocSeqLineItems 중첩 테이블에서 **Ordernumber** 열을 조인의 한 쪽을 나타내는 vAssocSeqOrders case 테이블로 끌어 놓습니다 (이 경우).  
  
     이제 vAssocSeqLineItems 테이블과 vAssocSeqOrders 테이블 간에 새로운 *다대일 관계가* 있습니다. 테이블을 올바르게 조인한 경우 데이터 원본 뷰는 다음과 같아야 합니다.  
  
     ![중첩 테이블과 사례 테이블에 대 한 다대일 조인이 필요 합니다.](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "중첩 테이블과 사례 테이블에 대 한 다대일 조인이 필요 합니다.")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [&#40;중급 데이터 마이닝 자습서&#41;시장 바구니 구조 및 모델 만들기](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 데이터 마이닝&#41;&#40;중급 데이터 마이닝 자습서](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [마이닝 구조 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 모델&#40;Analysis Services - 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
