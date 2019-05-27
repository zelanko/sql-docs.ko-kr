---
title: 팩트 관계 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4b49a078-6848-4286-bc71-cf4862d29064
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 726b5fa4295d68c5b74d4fb3cac711126a8e570b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078568"
---
# <a name="defining-a-fact-relationship"></a>팩트 관계 정의
  사용자는 팩트 테이블에 있는 데이터 항목별로 측정값 차원을 구분하거나 특정 판매 팩트에 관련된 송장 번호나 구매 주문 번호와 같은 특정 추가 관련 정보를 팩트 테이블에서 쿼리할 수 있습니다. 이러한 팩트 테이블 항목을 기반으로 차원을 정의할 경우 이 차원을 *팩트 차원*이라고 합니다. 팩트 차원은 중복 제거 차원이라고도 합니다. 팩트 차원은 특정 송장 번호에 관련된 모든 행과 같은 관련 팩트 테이블 행을 함께 그룹화하는 데 유용합니다. 이 정보를 관계형 데이터베이스에 있는 별도의 차원 테이블에 넣을 수 있는데도 정보에 대한 별도의 차원 테이블을 만들면 차원 테이블이 팩트 테이블과 같은 속도로 커지고 중복 데이터가 발생하며 과도하게 복잡해지기 때문에 좋지 않습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 쿼리 성능 향상을 위해 팩트 차원 데이터를 MOLAP 차원 구조로 복제할지 또는 쿼리 성능을 향상시키는 대신 저장 공간을 절약하기 위해 팩트 차원을 ROLAP 차원으로 정의할지 결정할 수 있습니다. MOLAP 스토리지 모드를 사용하여 차원을 저장하면 모든 차원 멤버는 측정값 그룹의 파티션에 저장될 뿐만 아니라 고도로 압축된 MOLAP 구조로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 저장됩니다. ROLAP 저장소 모드를 사용 하 여 차원을 저장 하면 차원 정의 저장 됩니다 molap에서 구조는 차원 멤버 자체는 기본 관계형 팩트 테이블에서 쿼리 시에 쿼리 합니다. 팩트 차원의 쿼리 빈도, 표준 쿼리에서 반환된 행 수, 쿼리 성능 및 처리 비용에 따라 적절한 스토리지 모드를 결정하십시오. 차원을 ROLAP으로 정의한다고 해서 해당 차원을 사용하는 모든 큐브도 ROLAP 스토리지 모드를 사용하여 저장해야 하는 것은 아닙니다. 각 차원에 대한 스토리지 모드는 독립적으로 구성될 수 있습니다.  
  
 팩트 차원을 정의하면 팩트 차원과 측정값 그룹의 관계를 팩트 관계로 정의할 수 있습니다. 팩트 관계에 적용되는 제약 조건은 다음과 같습니다.  
  
-   세분성 특성이 차원에 대한 키 열이어야 하며 이에 따라 차원과 팩트 테이블의 팩트 간 일 대 일 관계를 만듭니다.  
  
-   차원은 하나의 측정값 그룹에 대한 팩트 관계만 가질 수 있습니다.  
  
> [!NOTE]  
>  매번 팩트 관계에서 참조하는 측정값 그룹을 업데이트한 후에는 팩트 차원을 증분 업데이트해야 합니다.  
  
 자세한 내용은 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)와 [팩트 관계 및 팩트 관계 속성 정의](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)를 참조하세요.  
  
 이 항목의 태스크에서는 **FactInternetSales** 팩트 테이블의 **CustomerPONumber** 열을 기반으로 새 큐브 차원을 추가한 다음 이 새로운 큐브 차원과 **Internet Sales** 측정값 그룹 간 관계를 팩트 관계로 정의합니다.  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>Internet Sales Orders 팩트 차원 정의  
  
1.  솔루션 탐색기에서 **차원**을 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다.  
  
2.  **차원 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **생성 방법 선택** 페이지에서 **기존 테이블 사용** 옵션이 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
4.  **원본 정보 지정** 페이지에서 **Adventure Works DW 2012** 데이터 원본 뷰가 선택되어 있는지 확인합니다.  
  
5.  **주 테이블** 목록에서 **InternetSales**를 선택합니다.  
  
6.  **키 열** 목록에 **SalesOrderNumber** 와 **SalesOrderLineNumber** 가 표시되는지 확인합니다.  
  
7.  **이름 열** 목록에서 **SalesOrderLineNumber**를 선택합니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **관련 테이블 선택** 페이지에서 모든 테이블 옆 확인란의 선택을 취소한 후 **다음**을 클릭합니다.  
  
10. **차원 특성 선택** 페이지에서 헤더의 확인란을 두 번 클릭하여 모든 확인란의 선택을 취소합니다. **Sales Order Number** 특성은 키 특성이므로 선택된 상태로 유지됩니다.  
  
11. **Customer PO Number** 특성을 선택한 후 **다음**을 클릭합니다.  
  
12. **마법사 완료** 페이지에서 이름을 **Internet Sales Order Details** 로 바꾼 후 **마침** 을 클릭하여 마법사를 완료합니다.  
  
13. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
14. 에 **특성** 에 대 한 차원 디자이너의 창 합니다 **Internet Sales Order Details** 차원에 **Sales Order Number**, 변경한 후는  **이름** 속성 창에서 속성 `Item Description.`  
  
15. 에 **NameColumn** 속성 셀에서 찾아보기 단추를 클릭 **(...)** . **이름 열** 대화 상자의 **원본 테이블** 목록에서 **Product** 를 선택하고 **원본 열** 에 **EnglishProductName**을 선택한 후 **확인**을 클릭합니다.  
  
16. **데이터 원본 뷰** 창에서 **InternetSales** 테이블의 **SalesOrderNumber** 열을 **특성** 창으로 끌어다 놓아 **Sales Order Number** 특성을 차원에 추가합니다.  
  
17. 변경 합니다 **이름** 새 속성 **Sales Order Number** 특성을 `Order Number`를 변경 합니다 **OrderBy** 속성을 **키**.  
  
18. 에 **계층** 창 만들기를 **Internet Sales Orders** 포함 된 사용자 계층을 `Order Number` 및 **Item Description** 수준을 순서 대로.  
  
19. **특성** 창에서 **Internet Sales Order Details**를 선택한 다음 속성 창에서 **StorageMode** 속성 값을 검토합니다.  
  
     기본적으로 이 차원은 MOLAP 차원으로 저장됩니다. 스토리지 모드를 ROLAP으로 변경하면 처리 시간과 스토리지 공간이 절약되지만 쿼리 성능이 저하됩니다. 이 자습서에서는 스토리지 모드로 MOLAP을 사용합니다.  
  
20. 새로 만들어진 차원을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 큐브 차원으로 추가하려면 **큐브 디자이너**로 전환합니다. **큐브 구조** 탭에서 **차원** 창을 마우스 오른쪽 단추로 클릭하고 **큐브 차원 추가**를 선택합니다.  
  
21. **큐브 차원 추가**대화 상자에서 **Internet Sales Order Details** 를 선택한 후 **확인**을 클릭합니다.  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>팩트 차원의 팩트 관계 정의  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너에서 **차원 용도** 탭을 클릭합니다.  
  
     **Internet Sales Order Details** 큐브 차원은 고유 아이콘에 표시된 대로 자동으로 팩트 관계를 갖도록 구성되어 있습니다.  
  
2.  찾아보기 단추를 클릭 (**...** )에 **Item Description** 의 교집합에서 셀을 **Internet Sales** 측정값 그룹 및 **Internet Sales Order Details** 차원에 팩트 관계 속성을 검토 합니다.  
  
     **관계 정의** 대화 상자가 열립니다. 어떤 속성도 구성할 수 없습니다.  
  
     다음 그림에서는 **관계 정의** 대화 상자의 팩트 관계 속성을 보여 줍니다.  
  
     ![정의 관계 대화 상자](../../2014/tutorials/media/l5-factrelationship-2.gif "관계 정의 대화 상자")  
  
3.  클릭 **취소**합니다.  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>팩트 차원을 사용하여 큐브 찾아보기  
  
1.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포** 를 클릭하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 변경 내용을 배포하고 데이터베이스를 처리합니다.  
  
2.  배포가 성공적으로 완료된 후 **Tutorial 큐브에 대한 큐브 디자이너에서** 브라우저 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 탭을 클릭한 다음 **다시 연결** 단추를 클릭합니다.  
  
3.  데이터 창에서 모든 측정값과 계층을 제거한 다음 **Internet Sales-Sales Amount** 측정값을 데이터 창의 데이터 영역에 추가합니다.  
  
4.  메타데이터 창에서 **Customer**, **Location**, **Customer Geography**, **Members**, **All Customers**, **Australia**, **Queensland**, **Brisbane**, **4000**을 차례로 확장하고 **Adam Powell**를 마우스 오른쪽 단추로 클릭한 다음 **필터에 추가**를 클릭합니다.  
  
     단일 고객에게 반환되는 판매 주문을 제한하도록 필터링하면 해당 쿼리 성능이 크게 저하되지 않고도 대용량 팩트 테이블에서 기본 정보로 드릴다운할 수 있습니다.  
  
5.  **Internet Sales Order Details** 차원의 **Internet Sales Orders** 사용자 정의 계층을 데이터 창의 행 영역에 추가합니다.  
  
     판매 주문 번호와 Adam Powell의 해당 인터넷 판매량이 데이터 창에 나타납니다.  
  
     다음 이미지에서는 이전 단계의 결과를 보여 줍니다.  
  
     ![Internet Sales-sales Amount 차원 지정](../../2014/tutorials/media/l5-factrelationship-3.gif "Internet Sales-sales Amount 차원 지정")  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [다 대 다 관계 정의](../analysis-services/lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>관련 항목:  
 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [팩트 관계 및 팩트 관계 속성 정의](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
