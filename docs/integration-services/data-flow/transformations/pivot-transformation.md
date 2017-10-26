---
title: "피벗 변환 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79a12bf64f2ec27306a5ca8776b33acdb79ca82d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="pivot-transformation"></a>피벗 변환
  피벗 변환은 입력 데이터를 열 값으로 피벗함으로써 정규화된 데이터 집합을 정규화 상태는 낮지만 좀 더 압축된 버전으로 만듭니다. 예를 들어 고객 이름, 제품 및 구매 수량이 나열된 정규화된 **Orders** 데이터 집합에는 일반적으로 여러 제품을 구매한 고객에 대해 여러 행이 포함되어 있으며, 각 행에는 해당 고객의 각 제품 주문 정보가 표시되어 있습니다. 피벗 변환을 사용하여 이 데이터 집합을 제품 열로 피벗하면 각 고객별로 단일 행만 포함된 데이터 집합을 출력할 수 있습니다. 이 단일 행에는 해당 고객의 모든 구매 정보가 나열되며, 제품 이름은 열 이름으로, 그리고 수량은 제품 열에 값으로 표시됩니다. 모든 고객이 모든 제품을 구매하는 것은 아니기 때문에 여러 열에 Null 값이 포함될 수 있습니다.  
  
 데이터 집합이 피벗되면 입력 열은 피벗 프로세스에서 서로 다른 역할을 수행합니다. 열은 다음과 같은 방식으로 사용될 수 있습니다.  
  
-   열이 변경되지 않은 상태로 출력에 전달됩니다. 여러 입력 행이 단일 출력 행으로 될 수 있기 때문에 변환에서 열의 첫 번째 입력 값만 복사됩니다.  
  
-   열이 레코드 집합을 식별하는 키 또는 키의 일부 역할을 수행합니다.  
  
-   열이 피벗을 정의합니다. 이 열의 값은 피벗된 데이터 집합의 열과 연결됩니다.  
  
-   열에 포함된 값이 피벗으로 생성된 열에 배치됩니다.  
  
 이 변환에는 하나의 입력, 하나의 일반 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="sort-and-duplicate-rows"></a>행 정렬 및 중복  
 출력 데이터 집합에서 레코드를 가능한 적게 만들 수 있도록 데이터를 효율적으로 피벗하려면 입력 데이터가 피벗 열에서 정렬되어 있어야 합니다. 데이터가 정렬되어 있지 않을 때 피벗 변환을 수행하면 집합 멤버 자격을 정의하는 열인 집합 키에서 각 값에 대해 여러 레코드가 생성됩니다. 예를 들어 데이터 집합을 **Name** 열로 피벗할 때 이름이 정렬되어 있지 않으면 **Name** 의 값이 변경될 때마다 피벗이 발생하기 때문에 각 고객에 대해 두 개 이상의 행이 출력 데이터 집합에 포함될 수 있습니다.  
  
 입력 데이터에는 중복 행이 포함될 수 있는데 이 경우 피벗 변환이 실패합니다. "중복 행"은 집합 키 열과 피벗 열에 동일한 값이 있는 행을 의미합니다. 오류를 방지하려면 오류 행이 오류 출력으로 리디렉션되도록 변환을 구성하거나 중복 행이 없도록 값을 미리 집계합니다.  
  
##  <a name="options"></a> 피벗 대화 상자의 옵션  
 **피벗** 대화 상자에서 옵션을 설정하여 피벗 작업을 구성합니다. **피벗** 대화 상자를 열려면 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 피벗 변환을 패키지에 추가한 후 구성 요소를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  
  
 다음 목록에서는 **피벗** 대화 상자의 옵션에 대해 설명합니다.  
  
 **피벗 키**  
 테이블의 맨 위 행(머리글 행)에서 값에 사용할 열을 지정합니다.  
  
 **키 설정**  
 테이블의 왼쪽 열에 있는 값에 사용할 열을 지정합니다. 입력 날짜는 이 열에서 정렬되어야 합니다.  
  
 **피벗 값**  
 머리글 행 및 왼쪽 열에 있는 값이 아닌 다른 값으로 테이블 값에 사용할 열을 지정합니다.  
  
 **일치하지 않는 피벗 키 값을 무시하고 DataFlow 실행 후 보고**  
 패키지를 실행할 때 **피벗 키** 열에서 인식되지 않은 값이 포함된 행을 무시하고 모든 피벗 키 값을 로그 메시지로 출력하도록 피벗 변환을 구성하려면 이 옵션을 선택합니다.  
  
 **PassThroughUnmatchedPivotKeys** 사용자 지정 속성을 **True**로 설정하여 값을 출력하도록 변환을 구성할 수도 있습니다.  
  
 **값에서 피벗 출력 열 생성**  
 각 값에 대해 출력 열을 만들기 위해 피벗 변환을 설정하려면 이 상자에 피벗 키 값을 입력합니다. 패키지를 실행하기 전 값을 입력하거나 다음을 수행할 수 있습니다.  
  
1.  **일치하지 않는 피벗 키 값을 무시하고 DataFlow 실행 후 보고** 옵션을 선택한 후 **피벗** 대화 상자에서 **확인** 을 클릭하여 피벗 변환에 대한 변경 사항을 저장합니다.  
  
2.  패키지를 실행합니다.  
  
3.  패키지가 성공하면 **진행률** 탭을 클릭하고 피벗 변환에서 피벗 키 값이 포함된 정보 로그를 찾아 봅니다.  
  
4.  메시지를 마우스 오른쪽 단추로 클릭한 다음 **메시지 텍스트 복사**를 클릭합니다.  
  
5.  **디버그** 메뉴에서 **디버깅 중지** 를 클릭하여 디자인 모드로 전환합니다.  
  
6.  피벗 변환을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
7.  **일치하지 않는 피벗 키 값을 무시하고 DataFlow 실행 후 보고** 옵션을 선택 취소하고 다음 형식을 사용하여 **값에서 피벗 출력 열 생성** 상자에 피벗 키 값을 붙여넣습니다.  
  
     [value1],[value2],[value3]  
  
 **지금 열 생성**  
 **값에서 피벗 출력 열 생성** 상자에 나열된 각 피벗 키 값에 대해 출력 열을 만들려면 클릭합니다.  
  
 출력 열이 **피벗된 기존 출력 열** 상자에 표시됩니다.  
  
 **피벗된 기존 출력 열**  
 피벗 키 값에 대한 출력 열 나열  
  
 다음 표에서는 **Year** 열로 데이터가 피벗되기 전의 데이터 집합을 보여 줍니다.  
  
|Year|제품 이름|Total|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Road Tire Tube|35920.50|  
|2004|Water Bottle – 30 oz.|2805.00|  
|2002|Touring Tire|62364.225|  
  
 다음 표에서는 **Year** 열로 데이터를 피벗한 후의 데이터 집합을 보여 줍니다.  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Road Tire Tube|3592.05|35920.50|89801.25|  
|Water Bottle – 30 oz.|*NULL*|*NULL*|2805.00|  
|Touring Tire|62364.225|375051.60|1041810.00|  
  
 **Year** 열로 데이터를 피벗하기 위해 아래 표시된 것처럼 다음과 같은 옵션이 **피벗** 대화 상자에 설정됩니다.  
  
-   **피벗 키** 목록 상자에는 Year가 선택되어 있습니다.  
  
-   **집합 키** 목록 상자에는 Product Name이 선택되어 있습니다.  
  
-   **피벗 값** 목록 상자에는 Total이 선택되어 있습니다.  
  
-   **값에서 피벗 출력 열 생성** 상자에는 다음 값이 입력되어 있습니다.  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>피벗 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-content"></a>관련 내용  
 이 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [피벗 해제 변환](../../../integration-services/data-flow/transformations/unpivot-transformation.md)   
 [데이터 흐름](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

