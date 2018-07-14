---
title: '6 단원: 계산된 열 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f837fd314cd8a279e03cdfa2aa420920509510a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228413"
---
# <a name="lesson-6-create-calculated-columns"></a>6단원: 계산 열 만들기
  이 단원에서는 계산 열을 추가하여 모델에 새 데이터를 만듭니다. 계산 열은 모델에 이미 있는 데이터를 기반으로 합니다. 자세한 내용은 [계산 열&#40;SSAS 테이블 형식&#41;](tabular-models/ssas-calculated-columns.md)을 참조하세요.  
  
 서로 다른 세 테이블에 다섯 개의 새 계산 열을 만듭니다. 태스크마다 단계가 조금씩 다릅니다. 이는 새 열을 만들고 열의 이름을 바꾸고 테이블의 다양한 위치에 열을 배치하는 데 여러 가지 방법이 있음을 보여 주기 위한 것입니다.  
  
 이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [5단원: 관계 만들기](lesson-4-create-relationships.md)를 완료해야 합니다.  
  
## <a name="create-calculated-columns"></a>계산 열 만들기  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Date 테이블에서 Month Calendar 계산 열 만들기  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭하고 **모델 뷰**를 가리킨 다음 **데이터 보기**를 클릭합니다.  
  
     데이터 뷰에서는 모델 디자이너를 사용하여 계산 열만 만들 수 있습니다.  
  
2.  모델 디자이너에서 **Date** 테이블(탭)을 클릭합니다.  
  
3.  마우스 오른쪽 단추로 클릭 합니다 **Calendar Quarter** 열 및 클릭 **열 삽입**합니다.  
  
     이라는 새 열 **CalculatedColumn1** 왼쪽에 삽입 되는 **Calendar Quarter** 열입니다.  
  
4.  테이블 위의 수식 입력줄에 다음 수식을 입력합니다. 자동 완성 기능을 사용하면 정규화된 열 및 테이블 이름을 입력하고 사용 가능한 함수를 나열할 수 있습니다.  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
     계산 열의 모든 행에 값이 채워집니다. 테이블의 아래쪽으로 스크롤하면 각 행의 데이터에 따라 이 열에서 행마다 서로 다른 값을 포함할 수 있음을 알 수 있습니다.  
  
    > [!NOTE]  
    >  오류 메시지가 표시되면 수식의 열 이름이 [3단원: 열 이름 바꾸기](rename-columns.md)에서 변경한 열 이름과 일치하는지 확인합니다.  
  
5.  이 열의 이름을 바꿀 `Month Calendar`합니다.  
  
 Month Calendar 계산 열은 월에 대해 정렬 가능한 이름을 제공합니다.  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Date 테이블에서 Day of Week 계산 열 만들기  
  
1.  **Date** 테이블을 활성화한 상태로 **열** 메뉴를 클릭한 다음 **열 추가**를 클릭합니다.  
  
     새 열이 테이블의 맨 오른쪽에 추가됩니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
3.  열 이름 바꾸기 `Day of Week`합니다.  
  
4.  열 제목을 클릭한 다음 열을 **Day Name** 열과 **Day of Month** 열 사이로 끕니다.  
  
    > [!TIP]  
    >  테이블에서 열을 이동하여 쉽게 탐색할 수 있습니다.  
  
 Day of Week 계산 열은 요일에 대해 정렬 가능한 이름을 제공합니다.  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Product 테이블에서 Product Subcategory Name 계산 열 만들기  
  
1.  모델 디자이너에서 **Product** 테이블을 선택합니다.  
  
2.  테이블의 맨 오른쪽으로 스크롤합니다. 맨 오른쪽 열 이름은 **열 추가** (기울임꼴)입니다. 열 제목을 클릭합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
4.  열 이름 바꾸기 `Product Subcategory Name`합니다.  
  
 Product Subcategory Name 계산 열은 Product 테이블에서 Product Subcategory 테이블의 Product Subcategory Name 열에 있는 데이터가 포함된 계층을 만드는 데 사용됩니다. 계층은 둘 이상의 테이블에 걸쳐 있을 수 없습니다. 계층은 나중에 7단원에서 만듭니다.  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Product 테이블에서 Product Category Name 계산 열 만들기  
  
1.  **Product** 테이블을 활성화한 상태로 **열** 메뉴를 클릭한 다음 **열 추가**를 클릭합니다.  
  
2.  수식 입력줄에 다음 수식을 입력합니다.  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
3.  열 이름 바꾸기 `Product Category Name`합니다.  
  
 Product Category Name 계산 열은 Product 테이블에서 Product Category 테이블의 Product Category Name 열에 있는 데이터가 포함된 계층을 만드는 데 사용됩니다. 계층은 둘 이상의 테이블에 걸쳐 있을 수 없습니다.  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Internet Sales 테이블에서 Margin 계산 열 만들기  
  
1.  모델 디자이너에서 **Internet Sales** 테이블을 선택합니다.  
  
2.  새 열을 추가합니다.  
  
3.  수식 입력줄에 다음 수식을 입력합니다.  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
4.  열 이름 바꾸기 `Margin`합니다.  
  
5.  열을 **Sales Amount** 열과 **Tax Amt** 열 사이로 끕니다.  
  
 Margin 계산 열은 각(제품) 행의 매출이익률을 분석하는 데 사용됩니다.  
  
## <a name="next-step"></a>다음 단계  
 이 단원을 계속하려면 다음 단원인 [7단원: 측정값 만들기](lesson-6-create-measures.md)로 이동하세요.  
  
  
