---
title: "10단원: 계층 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 10단원: 계층 만들기
이 단원에서는 계층을 만듭니다. 계층은 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층에는 Country, State, County 및 City에 대한 하위 수준이 포함될 수 있습니다. 계층은 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다. 자세한 내용은 [계층 구조&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)를 참조하세요.  
  
계층을 만들려면 *다이어그램 뷰*에서 모델 디자이너를 사용합니다. 계층 만들기 및 관리는 데이터 뷰의 모델 디자이너에서는 지원되지 않습니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## 필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [9단원: 큐브 뷰 만들기](../Topic/Lesson%209:%20Create%20Perspectives.md)를 완료해야 합니다.  
  
## 계층 만들기  
  
#### Product 테이블에서 Category 계층을 만들려면  
  
1.  모델 디자이너에서 **모델** 메뉴를 클릭하고 **모델 뷰**를 가리킨 다음 **다이어그램 뷰**를 클릭합니다.  
  
  
  
2.  **Product** 테이블을 마우스 오른쪽 단추로 클릭한 다음 **계층 만들기**를 클릭합니다. 새 계층이 테이블 창의 아래쪽에 표시됩니다.  
  
3.  계층 이름에 **Category**를 입력하여 계층 이름을 바꾸고 Enter 키를 누릅니다.  
  
4.  **Product** 테이블에서 **Product Category Name** 열을 클릭하고 **Category** 계층으로 끌어 **Category** 위에 놓습니다.  
  
5.  **Category** 계층에서 **Product Category Name** 열을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 다음 **Category**를 입력합니다.  
  
    > [!NOTE]  
    > 계층에서 열 이름을 바꿔도 테이블의 열 이름은 바뀌지 않습니다. 계층의 열은 테이블 열에 대한 표현일 뿐입니다.  
  
6.  **Product** 테이블에서 **Product Subcategory Name** 열을 클릭하고 **Category** 계층으로 끕니다.  
  
7.  **Product Subcategory Name**을 **Subcategory**로 바꿉니다.  
  
8.  **Model Name**과 **Product Name** 열을 순서대로 클릭한 후 끌어서 **Product Subcategory Name** 열 아래에 놓습니다. 이러한 열의 이름을 각각 **Model**과 **Product**로 바꿉니다.  
  
#### Date 테이블에서 계층을 만들려면  
  
1.  모델 디자이너에서 **Date** 테이블을 마우스 오른쪽 단추로 클릭한 다음 **계층 만들기**를 클릭합니다.  
  
2.  계층 이름을 **Calendar**로 바꿉니다.  
  
3.  다음 열을 순서대로 추가하고 이름을 바꿉니다.  
  
    |열|바꾼 후 이름|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  **Date** 테이블에서 위의 단계를 반복하여 다음 열이 포함된 **Fiscal** 계층을 만듭니다.  
  
    |열|바꾼 후 이름|  
    |----------|--------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  마지막으로 **Date** 테이블에서 위의 단계를 반복하여 다음 열이 포함된 **Production Calendar** 계층을 만듭니다.  
  
    |열|바꾼 후 이름|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## 다음 단계  
이 자습서를 계속하려면 다음 단원인 [11단원: 파티션 만들기](../analysis-services/lesson-11-create-partitions.md)로 이동하세요.  
  
  
  
