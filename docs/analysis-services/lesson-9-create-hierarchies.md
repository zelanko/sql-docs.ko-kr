---
title: '9 단원: 계층 만들기 | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da8f3d0fb3f733c5a9307d633025bb67a1a4d8cb
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42791700"
---
# <a name="lesson-9-create-hierarchies"></a>9단원: 계층 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 계층을 만듭니다. 계층은 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층에는 Country, State, County 및 City에 대한 하위 수준이 포함될 수 있습니다. 계층은 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다. 자세한 내용은 참조 하세요 [계층](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)합니다.  
  
계층을 만들려면 모델 디자이너를 사용할지 *다이어그램 보기*합니다. 계층 만들기 및 관리 데이터 뷰에서 지원 되지 않습니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [8 단원: 큐브 뷰 만들기](../analysis-services/lesson-8-create-perspectives.md)합니다.  
  
## <a name="create-hierarchies"></a>계층 만들기  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>DimProduct 테이블에 Category 계층 구조를 만들려면  
  
1.  모델 디자이너 (다이어그램 뷰)에서 마우스 오른쪽 단추로 클릭 합니다 **DimProduct** 테이블 > **계층 만들기**합니다. 새 계층이 테이블 창의 아래쪽에 표시됩니다. 계층 이름을 바꾸고 **범주**합니다.  
  
2.  클릭 하 고 끌어서 합니다 **ProductCategoryName** 새 열 **범주** 계층입니다.  
  
3.  에 **범주** 계층 마우스 오른쪽 단추로 클릭 합니다 **ProductCategoryName** > **이름 바꾸기**, 입력 **범주**.  
  
    > [!NOTE]  
    > 계층에서 열 이름을 바꿔도 테이블의 열 이름은 바뀌지 않습니다. 계층의 열은 테이블 열에 대한 표현일 뿐입니다.  
  
4.  클릭 하 고 끌어서 합니다 **ProductSubcategoryName** 열을 **범주** 계층입니다. 이름을 바꿀 **Subcategory**합니다. 
  
5.  마우스 오른쪽 단추로 클릭 합니다 **ModelName** 열 > **계층 구조를 추가할**를 선택한 후 **범주**합니다. 에 대 한 동일한 작업을 수행할 **EnglishProductName**합니다. 계층 구조에서 이러한 열의 이름을 바꿀 **모델** 하 고 **제품**합니다.  

    ![으로 테이블 형식-lesson9-범주](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>DimDate 테이블에서 계층을 만들려면  
  
1.  에 **DimDate** 테이블, 명명 된 새 계층을 만듭니다 **달력**합니다.  
  
3.  다음 순서 대로 열을 추가 합니다.

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  에 **DimDate** 테이블을 만듭니다는 **회계** 계층입니다. 열을 다음과 같습니다.  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  마지막으로 **DimDate** 테이블을 만듭니다는 **ProductionCalendar** 계층입니다. 열을 다음과 같습니다.  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>다음 단계
다음 단원으로 이동 합니다. [단원 10: 파티션 만들기](../analysis-services/lesson-10-create-partitions.md)합니다. 
  
  
