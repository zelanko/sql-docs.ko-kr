---
title: 'Analysis Services tutorial 9 단원: 계층 만들기 | Microsoft Docs'
description: ''
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 95953da3ff2fc71ac39db75daeea6dacdc0854f5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-hierarchies"></a>계층 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 계층 구조를 만듭니다. 계층은 수준별로 정렬 된 열 그룹입니다. 예를 들어 Geography 계층에는 Country, State, County 및 City 하위 수준이 있을 수 있습니다. 계층은 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다. 자세한 내용은 참고 [계층](../tabular-models/hierarchies-ssas-tabular.md)
  
계층을 만들려면 모델 디자이너에서 사용 하 여 *다이어그램 보기*합니다. 계층 만들기 및 관리 데이터 보기에서 지원 되지 않습니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [8 단원: 큐브 뷰 만들기](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)합니다.  
  
## <a name="create-hierarchies"></a>계층 만들기  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>DimProduct 테이블의 범주 계층을 만들려면  
  
1.  모델 디자이너 (다이어그램 뷰)에서 마우스 오른쪽 단추로 클릭는 **DimProduct** 테이블 > **계층 만들기**합니다. 새 계층이 테이블 창의 아래쪽에 표시됩니다. 계층 이름을 바꾸고 **범주**합니다.  
  
2.  클릭 하 고 끌어는 **ProductCategoryName** 를 새 열 **범주** 계층 구조입니다.  
  
3.  에 **범주** 계층을 마우스 오른쪽 단추로 클릭 **ProductCategoryName** > **이름 바꾸기**, 한 다음 입력 **범주**합니다.  
  
    > [!NOTE]  
    > 계층에서 열 이름을 바꿔도 테이블의 열 이름은 바뀌지 않습니다. 계층의 열은 테이블 열에 대한 표현일 뿐입니다.  
  
4.  클릭 하 고 끌어는 **ProductSubcategoryName** 열에는 **범주** 계층 구조입니다. 이름을 바꾸거나 **Subcategory**합니다. 
  
5.  마우스 오른쪽 단추로 클릭는 **ModelName** 열 > **계층 구조에 추가**를 선택한 후 **범주**합니다. 이름을 바꾸거나 **모델**합니다.

6.  마지막으로 추가 **EnglishProductName** 범주 계층에 있습니다. 이름을 바꾸거나 **제품**합니다.  

    ![as-lesson9-category](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>DimDate 테이블에서 계층을 만들려면  
  
1.  에 **DimDate** 테이블, 명명 된 계층 구조를 만들 **달력**합니다.  
  
3.  다음 순서 대로 열을 추가 합니다.

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  에 **DimDate** 테이블을 만들기는 **회계** 계층 구조입니다. 다음 순서 대로 열을 포함 합니다.  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  마지막으로 **DimDate** 테이블을 만들기는 **ProductionCalendar** 계층 구조입니다. 다음 순서 대로 열을 포함 합니다.  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>다음 단계

[10 단원: 파티션 만들기](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)합니다. 
  
  
