---
title: '10 단원: 계층 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: ea741676f07020291c2aa94d130c2f595a50f323
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079157"
---
# <a name="lesson-10-create-hierarchies"></a>10단원: 계층 만들기
  이 단원에서는 계층을 만듭니다. 계층은 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층에는 Country, State, County 및 City에 대한 하위 수준이 포함될 수 있습니다. 계층은 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다. 자세한 내용은 [계층 구조&#40;SSAS 테이블 형식&#41;](tabular-models/hierarchies-ssas-tabular.md)를 참조하세요.  
  
 계층을 만들려면 *다이어그램 뷰*에서 모델 디자이너를 사용합니다. 계층 만들기 및 관리는 데이터 뷰의 모델 디자이너에서는 지원되지 않습니다.  
  
 이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [9단원: 큐브 뷰 만들기](lesson-8-create-perspectives.md)를 완료해야 합니다.  
  
## <a name="create-hierarchies"></a>계층 만들기  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Product 테이블에서 Category 계층을 만들려면  
  
1.  모델 디자이너에서 클릭는 `Model` 메뉴, **모델 뷰**, 클릭 하 고 **다이어그램 보기**합니다.  
  
    > [!TIP]  
    >  모델 디자이너 오른쪽 위 모퉁이에 있는 미니맵 컨트롤을 사용하여 다이어그램 뷰에서의 개체 표시 방식을 변경할 수 있습니다. 다이어그램 뷰에서 개체 위치를 변경하면 프로젝트를 저장할 때 해당 뷰가 유지됩니다.  
  
2.  모델 디자이너에서 마우스 오른쪽 단추로 클릭는 `Product` 테이블을 마우스 클릭 **계층 만들기**합니다. 새 계층이 테이블 창의 아래쪽에 표시됩니다.  
  
3.  계층 이름에 입력 하 여 계층 이름을 바꾸고 `Category`, 한 다음 ENTER 키를 누릅니다.  
  
4.  에 `Product` 테이블에서 **Product Category Name** 열을 끌어는 `Category` 계층과의 맨 위에 놓으면은 `Category` 이름입니다.  
  
5.  에 `Category` 계층 구조를 마우스 오른쪽 단추로 클릭는 **Product Category Name** 열을 클릭 한 다음 **이름 바꾸기**, 한 다음 입력 `Category`합니다.  
  
    > [!NOTE]  
    >  계층에서 열 이름을 바꿔도 테이블의 열 이름은 바뀌지 않습니다. 계층의 열은 테이블 열에 대한 표현일 뿐입니다.  
  
6.  에 `Product` 테이블을 마우스 오른쪽 단추로 클릭는 **Product Subcategory Name** 열에서 다음 상황에 맞는 메뉴를 가리킨 **계층 구조에 추가**, 클릭 하 고 `Category`합니다.  
  
7.  이름 바꾸기 **Product Subcategory Name** 를 `Subcategory`합니다.  
  
8.  클릭 한 후 끌기 또는 사용 하 여는 **계층 구조에 추가** 상황에 맞는 메뉴 명령에 추가 **모델 이름** 및 **제품 이름** (순서) 대로 열 아래에 배치 된 **Product Subcategory Name** 열입니다. 이러한 열의 이름을 바꿀 `Model` 및 `Product`각각.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Date 테이블에서 계층을 만들려면  
  
1.  모델 디자이너에서 **Date** 테이블을 마우스 오른쪽 단추로 클릭한 다음 **계층 만들기**를 클릭합니다.  
  
2.  계층 이름을 **Calendar**로 바꿉니다.  
  
3.  다음 열을 순서대로 추가하고 이름을 바꿉니다.  
  
    |Column|바꾼 후 이름|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  **Date** 테이블에서 위의 단계를 반복하여 다음 열이 포함된 **Fiscal** 계층을 만듭니다.  
  
    |Column|바꾼 후 이름|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  마지막으로 **Date** 테이블에서 위의 단계를 반복하여 다음 열이 포함된 **Production Calendar** 계층을 만듭니다.  
  
    |Column|바꾼 후 이름|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [11단원: 파티션 만들기](lesson-10-create-partitions.md)로 이동하세요.  
  
  