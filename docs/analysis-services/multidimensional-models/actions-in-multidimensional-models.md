---
title: "다차원 모델의 동작 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services], creating
- report actions [Analysis Services]
- drillthrough actions [Analysis Services]
- cubes [Analysis Services], actions
ms.assetid: b9fee2b9-05a5-4077-848d-d8457326dc27
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a4b7d3b0523fb19b9b0d7e0542cc587fb1585992
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="actions-in-multidimensional-models"></a>다차원 모델의 동작
  동작이란 선택한 큐브 또는 큐브의 일부분에 대해 최종 사용자가 시작하는 동작입니다. 작업은 선택한 항목을 매개 변수로 응용 프로그램을 시작하거나 선택한 항목에 대한 정보를 검색할 수 있습니다. 동작에 대한 자세한 내용은 [동작&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)을 참조하세요.  
  
 큐브 디자이너의 **동작** 탭을 사용하여 큐브에 대한 작업을 만들 수 있습니다. 다음을 지정합니다.  
  
 **이름**  
 동작을 식별하는 이름을 선택합니다.  
  
 **동작 대상**  
 동작을 연결할 개체를 선택합니다. 클라이언트 응용 프로그램에서는 일반적으로 최종 사용자가 대상 개체를 선택할 때 작업이 표시되지만 동작을 표시하는 최종 사용자의 동작은 클라이언트 응용 프로그램에 따라 다릅니다. 다음 개체 중에서 **대상 유형**을 선택합니다.  
  
-   특성 멤버  
  
-   셀  
  
-   Cube  
  
-   차원 멤버  
  
-   계층  
  
-   계층 멤버  
  
-   Level  
  
-   수준 멤버  
  
 대상 개체 유형을 선택한 후 **대상 개체**에서 지정된 유형의 큐브 개체를 선택합니다.  
  
 **조건(옵션)**  
 부울 값으로 확인되는 선택적 MDX(Multidimensional Expression) 식을 지정합니다. 값이 **True**이면 지정된 대상에서 동작이 수행됩니다. 값이 **False**이면 동작이 수행되지 않습니다.  
  
 **동작 내용**  
 동작의 유형을 선택합니다. 다음 표에는 사용 가능한 유형이 요약되어 있습니다.  
  
|형식|Description|  
|----------|-----------------|  
|데이터 집합|데이터 집합을 검색합니다.|  
|소유|이 표에 나열되지 않은 인터페이스를 사용하여 작업을 수행합니다.|  
|행 집합|행 집합을 검색합니다.|  
|문|OLE DB 명령을 실행합니다.|  
|URL|가변 페이지를 인터넷 브라우저로 표시합니다.|  
  
 **동작 식**의 경우 작업이 실행될 때 전달되는 매개 변수를 지정합니다. 구문은 문자열로 평가되어야 하며 MDX로 작성된 식이 포함되어야 합니다. 예를 들어 MDX 식으로 구문에 포함되는 큐브의 일부를 나타낼 수 있습니다. MDX 식은 매개 변수가 전달되기 전에 평가됩니다. 또한 MDX 식 작성을 도와 주는 MDX 작성기를 사용할 수 있습니다.  
  
 **추가 속성**  
 속성을 선택합니다. 다음 표에는 사용 가능한 속성이 요약되어 있습니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**호출**|동작 실행 방법을 지정합니다. 기본값인 대화형은 사용자가 개체에 액세스할 때 동작이 실행되도록 지정합니다. 가능한 설정은 아래와 같습니다.<br /><br /> 일괄 처리<br /><br /> 대화형<br /><br /> 열 때|  
|**응용 프로그램**|동작의 응용 프로그램을 나타냅니다.|  
|**Description**|동작에 대한 설명입니다.|  
|**캡션**|동작에 대해 표시되는 캡션을 제공합니다. 캡션이 MDX이면 **MDX 캡션** 을 **True**로 지정합니다.|  
|**True**|캡션이 MDX이면 **True** 를 지정하고 그렇지 않으면 **False** 를 지정합니다.|  
  
> [!NOTE]  
>  HTML 및 명령줄 동작 유형을 정의하려면 ASSL(Analysis Services Scripting Language)이나 AMO(Analysis Management Objects)를 사용해야 합니다. 자세한 내용은 [Action 요소&#40;ASSL&#41;](../../analysis-services/scripting/objects/action-element-assl.md), [Type 요소&#40;Action&#41;&#40;ASSL&#41;](../../analysis-services/scripting/properties/type-element-action-assl.md) 및 [AMO OLAP 고급 개체 프로그래밍](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)을 참조하세요.  
  
## <a name="creating-a-reporting-action"></a>보고 동작 만들기  
 보고서 서버는 URL 기반 보고서 요청에 응답합니다. 보고 동작을 만들려면 **큐브** 메뉴에서 **새 보고 작업**을 클릭합니다. 보고 동작에 다음 옵션을 사용할 수 있습니다.  
  
 **보고서 서버**  
 보고서 서버에 다음 표에서 설명하는 속성을 지정합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**서버 이름**|보고서 서버를 실행 중인 컴퓨터의 이름입니다.|  
|**서버 경로**|보고서 서버를 나타내는 경로입니다.|  
|**보고서 형식**|HTML5, HTML3, Excel 또는 PDF입니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 서버 이름 속성에 전송 계층 보안(https:)을 지정할 수 있습니다.  
  
 **매개 변수(옵션)**  
 매개 변수는 동작이 생성될 때 URL 문자열의 일부로 서버에 전송됩니다. 이러한 매개 변수에는 MDX 식인 **매개 변수 이름** 과 **매개 변수 값**이 포함됩니다.  
  
 보고서 서버 URL의 형식은 다음과 같습니다.  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 예를 들어  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>드릴스루 동작 만들기  
 드릴스루 동작은 클라이언트 응용 프로그램에 드릴스루 문으로 반환되는 행 집합 작업으로 정의됩니다. 동작 대상은 측정값 그룹의 멤버입니다. 새 드릴스루 작업을 만들려면 **큐브** 메뉴에서 **새 드릴스루 동작**을 클릭합니다. 드릴스루 동작에 다음 옵션을 사용할 수 있습니다.  
  
 **드릴스루 열**  
 하나 이상의 차원을 선택하고 각 차원에 대해 동작에 따라 클라이언트 응용 프로그램에 반환되는 드릴스루 열을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 큐브](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
