---
title: 'Analysis Services 자습서 추가 단원: 비정형 계층 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc5a2164576e2e6142d8835dad6f6c114b7a9c5b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38042307"
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>추가 단원-불규칙된 한 계층 구조

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 추가 단원에서는 다양 한 수준에서 빈 값 (멤버)를 포함 하는 계층 구조를 피벗할 때 일반적인 문제를 해결 합니다. 예를 들어, 조직 부서 관리자와 비-직속 부하로 고위 관리자가 하는 위치입니다. 또는 국가-지역-도시로 일부 도시는 상위 시 /도, 같은 Washington D.C., Vatican City에 없는 지리적 계층으로 구성 합니다. 계층에 빈 멤버가 종종 다르거나 불규칙 한 수준으로 이어집니다.

![as-lesson-detail-ragged-hierarchies-table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

1400 호환성 수준의 테이블 형식 모델을 추가 했습니다 **멤버 숨기기** 계층에 대 한 속성입니다. 합니다 **기본** 설정은 모든 수준에 빈 멤버가 없다고 가정 합니다. 합니다 **빈 멤버 숨기기** 설정 피벗 테이블 또는 보고서에 추가 하는 경우 계층에서 빈 멤버를 제외 합니다.  
  
이 단원에 소요되는 예상 시간: **20분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 추가 단원 문서는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원의 작업을 수행 하기 전에 완료 해야 이전의 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트가 또는 합니다. 

자습서의 일부로 AW Internet Sales 프로젝트를 만든 모델에 아직 없는 경우 모든 데이터 또는 비정형된 계층입니다. 이 추가 단원을 완료 하려면 먼저 경우 몇 가지 추가 테이블을 추가 하 여 문제를 만들기, 관계, 계산된 열, 측정값 및 새 조직 계층 구조 만들기 해당 부분에는 15 분 정도 걸립니다. 그런 다음 몇 분 내에 해결 하기 위해 가져올 수도 있습니다.  

## <a name="add-tables-and-objects"></a>테이블 및 개체를 추가 합니다.
  
### <a name="to-add-new-tables-to-your-model"></a>새 테이블 모델을 추가 하려면
  
1.  테이블 형식 모델 탐색기에서 확장 **데이터 원본**, 한 다음 연결을 마우스 오른쪽 단추로 클릭 > **새 테이블 가져오기**합니다.
  
2.  탐색 창에서 선택 **DimEmployee** 하 고 **FactResellerSales**를 클릭 하 고 **확인**합니다.

3.  쿼리 편집기에서 클릭 **가져오기**

4.  다음 항목을 만듭니다 [관계](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | 표 1           | Column       | 필터 방향   | 표 2     | Column      | 활성 |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Default            | FactOnlineSales     | Date        | 예    |
    | FactResellerSales | DueDate      | Default            | FactOnlineSales     | Date        | 아니요     |
    | FactResellerSales | ShipDateKey  | Default            | FactOnlineSales     | Date        | 아니요     |
    | FactResellerSales | ProductKey   | Default            | DimProduct  | ProductKey  | 예    |
    | FactResellerSales | EmployeeKey  | 두 테이블에 | DimEmployee | EmployeeKey | 예    |

5. 에 **DimEmployee** 테이블에서 다음 항목을 만듭니다 [계산 된 열](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

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

6.  에 **DimEmployee** 테이블을 만듭니다는 [계층](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) 이라는 **조직**합니다. 다음 순서 대로 열을 추가: **Level1**, **Level2**를 **Level3**를 **Level4**를 **Level5**합니다.

7.  에 **FactResellerSales** 테이블에서 다음 항목을 만듭니다 [측정값](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  사용 하 여 [Excel에서 분석](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) Excel을 열고 피벗 테이블을 자동으로 만듭니다.

9.  **피벗 테이블 필드**를 추가 합니다 **조직** 계층을 **DimEmployee** 테이블 **행**, 및  **ResellerTotalSales** 에서 측정 합니다 **FactResellerSales** 테이블 **값**합니다.

    ![as-lesson-detail-ragged-hierarchies-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    피벗 테이블에서 보면 계층 불규칙 하는 행을 표시 합니다. 빈 멤버가 표시 되어 있는 행의 수 있습니다.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>멤버 숨기기 속성을 설정 하 여 불규칙된 한 계층 구조를 수정 하려면

1.  **테이블 형식 모델 탐색기**를 확장 하 고 **테이블** > **DimEmployee** > **계층**  >  **조직**합니다.

2.  **속성** > **멤버 숨기기**선택 **빈 멤버 숨기기**합니다. 

    ![as-lesson-detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  다시 Excel에서에서 피벗 테이블을 새로 고칩니다. 

    ![as-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    이제 훨씬 보입니다!

## <a name="see-also"></a>관련 항목   
[9단원: 계층 만들기](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[추가 단원-동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[추가 단원-세부 정보 행](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
