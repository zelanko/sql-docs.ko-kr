---
title: "표준 동작 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ccb2928a-f75d-4acb-8ff8-fa80bb0935b2
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ed8e041cef62cb1782d0f00a90fe5c09986c7d81
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="add-a-standard-action"></a>표준 동작 추가
  큐브 디자이너의 동작 뷰를 사용하여 데이터베이스에 동작을 추가합니다. 이 뷰는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 액세스할 수 있습니다. 동작을 만든 후 관련 큐브를 다시 처리하면 사용자가 동작을 사용할 수 있게 됩니다. 자세한 내용은 [Processing Analysis Services Objects](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)을 참조하세요.  
  
### <a name="to-create-an-action"></a>동작을 만들려면  
  
1.  동작을 만들 큐브를 연 다음 **동작** 탭을 클릭합니다.  
  
2.  도구 모음에서 **새 동작** 아이콘을 클릭한 다음 식 창에서 다음을 수행합니다.  
  
    -   **이름**에 동작의 이름을 입력합니다.  
  
    -   **대상 유형** 드롭다운 목록에서 동작을 연결할 개체의 유형을 선택합니다. **대상 유형** 에서 선택한 개체에 따라 사용할 수 있는 개체와 **대상 개체**에서 선택할 수 있는 유형이 결정됩니다. 다음 표에서는 각 대상 유형에 대해 선택할 수 있는 **대상 개체** 를 보여 줍니다.  
  
        |선택한 대상 유형|선택할 수 있는 대상 개체|  
        |---------------------------------------------|---------------------------------------------------|  
        |특성 멤버|단일 특성 계층만 선택할 수 있습니다. 표시되는 모든 특성 멤버는 동작 대상 유형입니다. 즉, 동작이 사용자 정의 계층에도 적용됩니다.|  
        |셀|셀만 선택할 수 있습니다. **셀** 을 대상 유형으로 선택한 경우 **조건** 에 식을 입력하여 동작이 연결되는 셀을 제한할 수 있습니다.|  
        |Cube|CURRENTCUBE만 선택할 수 있습니다. 동작은 현재 큐브와 연결 됩니다.|  
        |차원 멤버|단일 차원을 선택합니다. 동작은 차원의 모든 멤버와 연결 됩니다.|  
        |계층|단일 계층을 선택합니다. 동작은 계층 개체와만 연결 됩니다. 특성 계층은 **AttributeHierarchyEnabled** 및 **AttributeHierarchyVisible** 속성을 **True**로 설정한 경우에만 목록에 나타납니다.|  
        |계층 멤버|단일 계층을 선택합니다. 동작은 선택한 계층의 모든 멤버와 연결 됩니다. 특성 계층은 **AttributeHierarchyEnabled** 및 **AttributeHierarchyVisible** 속성을 **True**로 설정한 경우에만 목록에 나타납니다.|  
        |Level|단일 수준을 선택합니다. 동작은 수준 개체하고만 연결 됩니다.|  
        |수준 멤버|단일 수준을 선택합니다. 동작은 선택한 수준의 모든 멤버와 연결 됩니다.|  
  
    -   **대상 개체**에서 입력란의 오른쪽에 있는 화살표를 클릭하고 표시되는 트리 뷰에서 동작을 연결할 개체를 클릭한 다음 **확인**을 클릭합니다.  
  
    -   필요에 따라 **조건**에서 동작의 대상을 제한하는 MDX 식을 만듭니다. 식을 수동으로 입력하거나 **메타데이터** 및 **함수** 목록에서 항목을 끌어 놓을 수 있습니다.  
  
    -   **유형** 드롭다운 목록에서 만들 동작의 유형을 선택합니다. 다음 표에서는 사용 가능한 동작의 유형을 보여 줍니다.  
  
        |유형|Description|  
        |----------|-----------------|  
        |데이터 집합|데이터 집합을 검색합니다.|  
        |소유|이 표에 나열되지 않은 인터페이스를 사용하여 작업을 수행합니다.|  
        |행 집합|행 집합을 검색합니다.|  
        |문|OLE DB 명령을 실행합니다.|  
        |URL|웹 페이지를 인터넷 브라우저에 표시합니다.|  
  
    -   **동작 식**에서 동작을 정의하는 식을 만듭니다. 식은 문자열로 계산되어야 합니다. 식을 수동으로 입력하거나 **메타데이터** 및 **함수** 목록에서 항목을 끌어 놓을 수 있습니다.  
  
3.  필요에 따라 **추가 속성**을 확장하고 다음 단계 중 하나를 수행합니다.  
  
    -   **호출** 드롭다운 목록에서 동작을 호출하는 방법을 지정합니다. 다음 표에서는 동작을 호출하는 데 사용할 수 있는 옵션에 대해 설명합니다.  
  
        |옵션|Description|  
        |------------|-----------------|  
        |대화형|동작은 사용자 상호 작용에 의해 트리거됩니다.|  
        |일괄 처리|동작이 일괄 처리 작업으로 실행됩니다.|  
        |열 때|사용자가 큐브를 열 때 동작이 실행됩니다.|  
  
    -   **응용 프로그램**에 동작과 연결되는 응용 프로그램의 이름을 입력합니다. 예를 들어 특정 웹 사이트를 연결하는 동작을 만들 경우 동작과 연결되는 응용 프로그램은 Microsoft Internet Explorer 또는 다른 웹 브라우저이어야 합니다.  
  
        > [!NOTE]  
        >  클라이언트 응용 프로그램이 **응용 프로그램**에 지정된 이름과 일치하는 동작만 반환하도록 스키마 행 집합을 명시적으로 제한하지 않으면 소유 동작이 서버에 반환되지 않습니다.  
  
    -   URL 유형을 사용하는 경우 **동작 내용**에서 인터넷 주소를 따옴표로 묶습니다(예: "http://www.adventure-works.com").  
  
    -   **설명**에 동작에 대한 설명을 입력합니다.  
  
    -   **캡션**에서 캡션 또는 캡션으로 계산되는 MDX 식을 입합니다. 이 캡션은 동작이 시작되면 최종 사용자에게 표시됩니다. 캡션을 지정하지 않은 경우 동작의 이름이 대신 사용됩니다.  
  
    -   **MDX 캡션** 드롭다운 목록에서 캡션이 MDX인지 여부를 지정합니다. 이 필드는 **캡션** 의 내용을 MDX 식으로 계산할지 여부를 서버에 알려 줍니다.  
  
  
