---
title: 'Analysis Services 자습서 단원 9: 계층 만들기 | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 92f83e1e2b3553f85301574e98f95ed7e22c1184
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469788"
---
# <a name="create-hierarchies"></a>계층 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 계층 구조를 만듭니다. 계층은 수준별로 정렬 된 열 그룹입니다. 예를 들어 Geography 계층 구조는 국가, 상태, County 및 City에 대 한 하위 수준이 있을 수 있습니다. 계층은 보고 클라이언트 애플리케이션 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다. 자세한 내용은를 참조 하세요. [계층](../tabular-models/hierarchies-ssas-tabular.md)
  
모델 디자이너를 사용 하 여 계층을 만들려면 *다이어그램 보기*합니다. 계층 만들기 및 관리 데이터 뷰에서 지원 되지 않습니다.  
  
예상이 단원을 완료 시간: **20 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [8단원: 큐브 뷰 만들기](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)합니다.  
  
## <a name="create-hierarchies"></a>계층 만들기  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>DimProduct 테이블에 Category 계층 구조를 만들려면  
  
1.  모델 디자이너 (다이어그램 뷰)에서 마우스 오른쪽 단추로 클릭 합니다 **DimProduct** 테이블 > **계층 만들기**합니다. 새 계층이 테이블 창의 아래쪽에 표시됩니다. 계층 이름을 바꾸고 **범주**합니다.  
  
2.  클릭 하 고 끌어서 합니다 **ProductCategoryName** 새 열 **범주** 계층입니다.  
  
3.  에 **범주** 계층 마우스 오른쪽 단추로 클릭 **ProductCategoryName** > **이름 바꾸기**를 차례로 **범주**.  
  
    > [!NOTE]  
    > 계층에서 열 이름을 바꿔도 테이블의 열 이름은 바뀌지 않습니다. 계층의 열은 테이블 열에 대한 표현일 뿐입니다.  
  
4.  클릭 하 고 끌어서 합니다 **ProductSubcategoryName** 열을 **범주** 계층입니다. 이름을 바꿀 **Subcategory**합니다. 
  
5.  마우스 오른쪽 단추로 클릭 합니다 **ModelName** 열 > **계층 구조를 추가할**를 선택한 후 **범주**합니다. 이름을 바꿀 **모델**합니다.

6.  마지막으로, 추가할 **EnglishProductName** 범주 계층에 있습니다. 이름을 바꿀 **제품**합니다.  

    ![as-lesson9-category](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>DimDate 테이블에서 계층을 만들려면  
  
1.  에 **DimDate** 테이블, 명명 된 계층 구조를 만들 **달력**합니다.  
  
3.  다음 순서 대로 열을 추가 합니다.

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  에 **DimDate** 테이블을 만듭니다는 **회계** 계층입니다. 다음 열에서 순서 대로 다음과 같습니다.  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  마지막으로 **DimDate** 테이블을 만듭니다는 **ProductionCalendar** 계층입니다. 다음 열에서 순서 대로 다음과 같습니다.  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>다음 단계

[10 단원: 파티션을 만들](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)합니다. 
  
  
