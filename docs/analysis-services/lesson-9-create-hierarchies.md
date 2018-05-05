---
title: '10 단원: 계층 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9d05a5c401a6ead47652a8859a82a5adbc136f4b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-9-create-hierarchies"></a>9단원: 계층 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 계층을 만듭니다. 계층은 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층에는 Country, State, County 및 City에 대한 하위 수준이 포함될 수 있습니다. 계층은 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다. 자세한 내용은 참고 [계층](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)합니다.  
  
계층 구조를 만들려면 모델 디자이너를 사용 합니다 *다이어그램 보기*합니다. 계층 만들기 및 관리 데이터 보기에서 지원 되지 않습니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [8 단원: 큐브 뷰 만들기](../analysis-services/lesson-8-create-perspectives.md)합니다.  
  
## <a name="create-hierarchies"></a>계층 만들기  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>DimProduct 테이블의 범주 계층을 만들려면  
  
1.  모델 디자이너 (다이어그램 뷰)에서 마우스 오른쪽 단추로 클릭는 **DimProduct** 테이블 > **계층 만들기**합니다. 새 계층이 테이블 창의 아래쪽에 표시됩니다. 계층 이름을 바꾸고 **범주**합니다.  
  
2.  클릭 하 고 끌어는 **ProductCategoryName** 를 새 열 **범주** 계층 구조입니다.  
  
3.  에 **범주** 계층을 마우스 오른쪽 단추로 클릭는 **ProductCategoryName** > **이름 바꾸기**, 한 다음 입력 **범주**합니다.  
  
    > [!NOTE]  
    > 계층에서 열 이름을 바꿔도 테이블의 열 이름은 바뀌지 않습니다. 계층의 열은 테이블 열에 대한 표현일 뿐입니다.  
  
4.  클릭 하 고 끌어는 **ProductSubcategoryName** 열에는 **범주** 계층 구조입니다. 이름을 바꾸거나 **Subcategory**합니다. 
  
5.  마우스 오른쪽 단추로 클릭는 **ModelName** 열 > **계층 구조에 추가**를 선택한 후 **범주**합니다. 에 대 한 동일 하 게 수행 **EnglishProductName**합니다. 계층 구조에서 이러한 열의 이름을 바꿀 **모델** 및 **제품**합니다.  

    ![로-테이블 형식-lesson9-범주](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>DimDate 테이블에서 계층을 만들려면  
  
1.  에 **DimDate** 테이블, 명명 된 새 계층 구조를 만들 **달력**합니다.  
  
3.  다음 순서 대로 열을 추가 합니다.

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  에 **DimDate** 테이블을 만들기는 **회계** 계층 구조입니다. 열을 다음과 같습니다.  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  마지막으로 **DimDate** 테이블을 만들기는 **ProductionCalendar** 계층 구조입니다. 열을 다음과 같습니다.  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [10 단원: 파티션 만들기](../analysis-services/lesson-10-create-partitions.md)합니다. 
  
  
