---
title: "Analysis Services tutorial 추가 단원: 비정형 계층 | Microsoft Docs"
description: "Analysis Services 자습서에서 비정형된 계층 구조를 수정 하는 방법에 설명 합니다."
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: ebadf3498d7047873bfcd79099a02c387618367e
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>추가 단원-비정형된 계층 구조

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 추가 단원에서는 다양 한 수준에서 빈 값 (멤버)를 포함 하는 계층 구조를 피벗 하는 경우 일반적인 문제를 해결 합니다. 예를 들어 조직 고위 관리자가 부서 관리자와 부하 직원으로 비-관리자입니다. 또는 국가-지역-도시의 부모 시 /도, 같은 Washington D.C., Vatican City 일부 도시에 없는 지역 계층으로 구성 합니다. 계층 구조에 새 멤버가 종종 다른 또는 비정형, 수준으로 이어집니다.

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

1400 호환성 수준에서 테이블 형식 모델은 추가 **멤버 숨기기** 계층에 대 한 속성입니다. **기본** 설정에서는 빈 멤버가 모든 수준에서 한다고 가정 합니다. **빈 멤버를 숨기도록** 설정 피벗 테이블 또는 보고서에 추가 될 때 계층에서 빈 멤버를 제외 시킵니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 추가 단원은 문서는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원 태스크를 수행 하기 전에 완료 해야 이전 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트 수도 있고 합니다. 

AW Internet Sales 프로젝트 자습서의 일부로 만든 모델에 아직 없는 경우 데이터 나 비정형된 계층. 이 추가 단원을 완료 하려면 먼저 해야 몇 가지 추가 테이블을 추가 하 여 문제를 만들고, 관계, 계산된 열, 측정값 및 새로운 조직 계층을 만듭니다. 해당 부분에는 15 분 정도 걸립니다. 그런 다음 몇 분 후에 해결 하기 위해 가져올 수도 있습니다.  

## <a name="add-tables-and-objects"></a>테이블 및 개체를 추가 합니다.
  
### <a name="to-add-new-tables-to-your-model"></a>모델에 새 테이블을 추가 하려면
  
1.  테이블 형식 모델 탐색기에서 확장 **데이터 원본**, 연결을 마우스 오른쪽 단추로 클릭 > **새 테이블 가져오기를**합니다.
  
2.  탐색 창의 선택 **DimEmployee** 및 **FactResellerSales**, 클릭 하 고 **확인**합니다.

3.  쿼리 편집기에서 클릭 **가져오기**

4.  다음 만듭니다 [관계](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | 표 1           | 열       | 필터 방향   | 표 2     | 열      | 활성 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | 기본값            | FactOnlineSales     | 날짜        | 예    |
    | FactResellerSales | DueDate      | 기본값            | FactOnlineSales     | 날짜        | 아니요     |
    | FactResellerSales | ShipDateKey  | 기본값            | FactOnlineSales     | 날짜        | 아니요     |
    | FactResellerSales | ProductKey   | 기본값            | DimProduct  | ProductKey  | 예    |
    | FactResellerSales | EmployeeKey  | 두 테이블 모두로 | DimEmployee | EmployeeKey | 예    |

5. 에 **DimEmployee** 테이블을 만드는 다음 [계산 된 열](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **경로** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  에 **DimEmployee** 테이블을 만들기는 [계층](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) 라는 **조직**합니다. 다음 순서에 열 추가: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**합니다.

7.  에 **FactResellerSales** 테이블을 만드는 다음 [측정값](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  사용 하 여 [Excel에서 분석](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) Excel을 열고 피벗 테이블을 자동으로 만듭니다.

9.  **피벗 테이블 필드**, 추가 **조직** 에서 계층 구조는 **DimEmployee** 테이블 **행**, 및  **ResellerTotalSales** 에서 측정 된 **FactResellerSales** 테이블 **값**합니다.

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    피벗 테이블에 보시 계층 구조는 비정형 않은 행을 표시 합니다. 빈 멤버 표시 되어 있는 행 수 있습니다.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>숨기기 멤버 속성을 설정 하 여 비정형된 계층 구조를 수정 하려면

1.  **테이블 형식 모델 탐색기**를 확장 하 고 **테이블** > **DimEmployee** > **계층**  >  **조직**합니다.

2.  **속성** > **멤버 숨기기**선택, **빈 멤버를 숨기도록**합니다. 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Excel에서 다시 피벗 테이블을 새로 고칩니다. 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    이제 훨씬 좋아보이지!

## <a name="see-also"></a>관련 항목:   
[9단원: 계층 만들기](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[추가 단원-동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[추가 단원-정보 행](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
