---
title: '5 단원: 관계 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a80f607c3187e967404ce018b7eed00497d9c01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078575"
---
# <a name="lesson-5-create-relationships"></a>5단원: 관계 만들기
  이 단원에서는 데이터를 가져올 때 자동으로 생성된 관계를 확인하고 다양한 테이블 간에 새 관계를 추가합니다. 관계는 해당 테이블의 데이터가 상호 관련되는 방식을 설정하는 두 테이블 간의 연결입니다. 예를 들어 Product 테이블과 Product Subcategory 테이블은 각 제품이 하위 범주에 속한다는 점에서 관련되어 있습니다. 자세한 내용은 [관계&#40;SSAS 테이블 형식&#41;](tabular-models/relationships-ssas-tabular.md)를 참조하세요.  
  
 이 단원을 완료하기 위한 예상 시간: **10분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원의 태스크를 수행하려면 이전 단원인 [3단원: 열 이름 바꾸기](rename-columns.md)를 완료해야 합니다.  
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>기존 관계를 검토하고 새 관계 추가  
 테이블 가져오기 마법사를 사용하여 데이터를 가져올 때 AdventureWorksDW 데이터베이스에서 7개의 테이블을 가져왔습니다. 일반적으로 관계형 원본에서 데이터를 가져올 경우 데이터와 함께 기존 관계도 자동으로 가져와집니다. 그러나 모델 작성을 진행하기 전에 테이블 간의 관계가 적절히 생성되었는지 확인해야 합니다. 이 자습서에서는 3가지 새로운 관계도 추가합니다.  
  
#### <a name="to-review-existing-relationships"></a>기존 관계를 검토하려면  
  
1.  
  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭하고 **모델 뷰**를 가리킨 다음 **다이어그램 뷰**를 클릭합니다.  
  
     이제 모델 디자이너가 다이어그램 뷰에 표시됩니다. 다이어그램 뷰는 가져온 모든 테이블을 테이블 간의 선으로 표시하는 그래픽 형식입니다. 테이블 간의 선은 데이터를 가져올 때 자동으로 생성된 관계를 나타냅니다.  
  
     모델 디자이너의 오른쪽 위 모퉁이에 있는 미니맵 컨트롤을 사용하여 뷰를 조정하면 테이블을 가능한 한 많이 포함할 수 있습니다. 테이블을 다른 위치로 클릭하여 끌어 가깝게 가져오거나 특정 순서로 배치할 수도 있습니다. 테이블을 이동해도 테이블 간 관계에는 영향을 주지 않습니다. 특정 테이블의 모든 열을 보려면 테이블 가장자리를 클릭하고 끌어 확장하거나 축소합니다.  
  
2.  
  **Customer** 테이블과 **Geography** 테이블 사이의 실선을 클릭합니다. 이러한 두 테이블 간의 실선은 이 관계가 활성 상태임을 나타내므로 기본적으로 DAX 수식을 계산할 때 사용됩니다.  
  
     이제 **Customer** 테이블의 **Geography Id** 열과 **Geography** 테이블의 **Geography Id** 열이 각각 상자 내에 표시되는 것을 확인할 수 있습니다. 이들이 관계에 사용된 열임을 보여 줍니다. 이제 관계의 속성이 **속성** 창에 나타납니다.  
  
    > [!TIP]  
    >  다이어그램 뷰에서 모델 디자이너를 사용 하는 것 외에도 **관계 관리** 대화 상자를 사용 하 여 모든 테이블 간의 관계를 테이블 형식으로 표시할 수 있습니다. 
  **테이블** 메뉴를 클릭한 다음 **관계 관리**를 클릭합니다. 그러면 **관계 관리** 대화 상자에 사용자가 데이터를 가져올 때 자동으로 생성된 관계가 표시됩니다.  
  
3.  다이어그램 뷰에서 모델 디자이너를 사용 하거나 **관계 관리** 대화 상자를 사용 하 여 AdventureWorksDW 데이터베이스에서 각 테이블을 가져올 때 다음 관계가 생성 되었는지 확인 합니다.  
  
    |Active|테이블|관련된 조회 테이블|  
    |------------|-----------|--------------------------|  
    |yes|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |yes|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |yes|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |yes|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |yes|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
 위 표에 나와 있는 관계 중 누락된 항목이 있으면 모델에 Customer, Date, Geography, Product, Product Category, Product Subcategory 및 Internet Sales 테이블이 포함되어 있는지 확인합니다. 동일한 데이터 원본 연결의 테이블을 별도의 시간에 가져오는 경우 해당 테이블 간의 관계가 만들어지지 않으므로 수동으로 만들어야 합니다.  
  
 일부 경우 특정 비즈니스 논리를 지원하기 위해서는 모델에서 테이블 간의 추가 관계를 만들어야 할 수 있습니다. 이 자습서에서는 Internet Sales 테이블과 Date 테이블 간에 세 개의 관계를 추가로 만들어야 합니다.  
  
#### <a name="to-add-new-relationships-between-tables"></a>테이블 간에 새로운 관계를 추가하려면  
  
1.  모델 디자이너의 **Internet Sales** 테이블에서 **Order Date** 열을 클릭한 채로 커서를 **Date** 테이블의 **Date** 열로 끌어다 놓습니다.  
  
     
  **Internet Sales** 테이블의 **Order Date** 열과 **Date** 테이블의 **Date** 열 간에 활성 관계를 만들었음을 보여 주는 실선이 나타납니다.  
  
    > [!NOTE]  
    >  관계를 만들 때 기본 테이블과 관련 조회 테이블 간의 순서는 자동으로 올바르게 설정됩니다.  
  
2.  
  **Internet Sales** 테이블에서 **Due Date** 열을 클릭한 채로 커서를 **Date** 테이블의 **Date** 열로 끌어다 놓습니다.  
  
     
  **Internet Sales** 테이블의 **Due Date** 열과 **Date** 테이블의 **Date** 열 간에 비활성 관계를 만들었음을 보여 주는 점선이 나타납니다. 테이블 간에 여러 관계를 포함할 수 있지만 한 번에 하나의 관계만 활성화될 수 있습니다.  
  
3.  마지막으로 관계를 하나 더 만듭니다. **Internet Sales** 테이블에서 **Ship Date** 열을 클릭한 채로 커서를 **Date** 테이블의 **Date** 열로 끌어다 놓습니다.  
  
     
  **Internet Sales** 테이블의 **Ship Date** 열과 **Date** 테이블의 **Date** 열 간에 비활성 관계를 만들었음을 보여 주는 점선이 나타납니다.  
  
## <a name="next-step"></a>다음 단계  
 이 단원을 계속하려면 다음 단원인 [6단원: 계산 열 만들기](lesson-5-create-calculated-columns.md)로 이동하세요.  
  
  
