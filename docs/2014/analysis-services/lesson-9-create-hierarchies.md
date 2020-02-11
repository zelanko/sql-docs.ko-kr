---
title: '10 단원: 계층 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb70d7d495d88ee62e98bf27f2b92bf569c98387
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078186"
---
# <a name="lesson-10-create-hierarchies"></a>10단원: 계층 만들기
  이 단원에서는 계층을 만듭니다. 계층 구조는 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층 구조는 Country, State, County 및 City에 대한 하위 수준을 포함할 수 있습니다. 계층 구조는 보고 클라이언트 애플리케이션 필드 목록에서 다른 열과 별도로 표시될 수 있으므로 클라이언트 사용자가 보고서에서 쉽게 탐색 및 포함할 수 있습니다. 자세한 내용은 [계층 구조&#40;SSAS 테이블 형식&#41;](tabular-models/hierarchies-ssas-tabular.md)를 참조하세요.  
  
 계층을 만들려면 *다이어그램 뷰*에서 모델 디자이너를 사용합니다. 계층 만들기 및 관리는 데이터 뷰의 모델 디자이너에서는 지원되지 않습니다.  
  
 이 단원을 완료하기 위한 예상 시간: **20분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원의 태스크를 수행하려면 이전 단원인 [9단원: 큐브 뷰 만들기](lesson-8-create-perspectives.md)를 완료해야 합니다.  
  
## <a name="create-hierarchies"></a>계층 만들기  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Product 테이블에서 Category 계층을 만들려면  
  
1.  모델 디자이너에서 `Model` 메뉴를 클릭 하 고 **모델 뷰**를 가리킨 다음 **다이어그램 뷰**를 클릭 합니다.  
  
    > [!TIP]  
    >  모델 디자이너 오른쪽 위 모퉁이에 있는 미니맵 컨트롤을 사용하여 다이어그램 뷰에서의 개체 표시 방식을 변경할 수 있습니다. 다이어그램 뷰에서 개체 위치를 변경하면 프로젝트를 저장할 때 해당 뷰가 유지됩니다.  
  
2.  모델 디자이너에서 `Product` 테이블을 마우스 오른쪽 단추로 클릭 한 다음 **계층 만들기**를 클릭 합니다. 새 계층 구조가 테이블 창 맨 아래에 나타납니다.  
  
3.  계층 이름에서를 입력 `Category`하 여 계층 이름을 바꾸고 enter 키를 누릅니다.  
  
4.  테이블에서 **Product Category Name** 열을 클릭 한 다음 `Category` 계층으로 끌고 `Category` 이름 위에 놓습니다. `Product`  
  
5.  계층에서 **Product Category Name** 열을 마우스 오른쪽 단추로 클릭 한 다음 **이름 바꾸기**를 클릭 하 고을 `Category`입력 합니다. `Category`  
  
    > [!NOTE]  
    >  계층 구조에서 열 이름을 변경해도 테이블의 열 이름은 변경되지 않습니다. 계층 구조의 열은 테이블의 열을 표현한 것일 뿐입니다.  
  
6.  테이블에서 **Product 하위 범주 이름** 열을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **계층에 추가**를 가리킨 다음를 클릭 `Category`합니다. `Product`  
  
7.  **Product 하위 범주 이름을** 으로 `Subcategory`바꿉니다.  
  
8.  클릭 및 끌기를 사용 하거나 상황에 맞는 메뉴에서 **계층에 추가** 명령을 사용 하 여 **모델 이름** 및 **product name** 열을 순서 대로 추가 하 고 **product 하위 범주 이름** 열 아래에 놓습니다. 이러한 열의 `Model` 이름을 각각 `Product`로 바꿉니다.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Date 테이블에서 계층을 만들려면  
  
1.  모델 디자이너에서 **Date** 테이블을 마우스 오른쪽 단추로 클릭한 다음 **계층 만들기**를 클릭합니다.  
  
2.  계층 이름을 **Calendar**로 바꿉니다.  
  
3.  다음 열을 순서대로 추가하고 이름을 바꿉니다.  
  
    |열|바꾼 후 이름|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|일|  
  
4.  
  **Date** 테이블에서 위의 단계를 반복하여 다음 열이 포함된 **Fiscal** 계층을 만듭니다.  
  
    |열|바꾼 후 이름|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|일|  
  
5.  마지막으로 **Date** 테이블에서 위의 단계를 반복하여 다음 열이 포함된 **Production Calendar** 계층을 만듭니다.  
  
    |열|바꾼 후 이름|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|일|  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [11단원: 파티션 만들기](lesson-10-create-partitions.md)로 이동하세요.  
  
  
