---
title: Actions (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services]
- actions [Analysis Services], about actions
- MDX [Analysis Services], actions
- cubes [Analysis Services], actions
- OLAP objects [Analysis Services], actions
ms.assetid: 07229bb2-805c-427e-8455-69c9ca5d01e0
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e5828886d047c6b8fcec0d511a8d1ddbd94bbae5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182353"
---
# <a name="actions-analysis-services---multidimensional-data"></a>동작(Analysis Services - 다차원 데이터)
  동작에는 여러 유형이 있을 수 있으므로 동작을 만들려면 이러한 유형을 고려해야 합니다. 다음과 같은 유형의 동작이 있을 수 있습니다.  
  
-   동작이 발생하는 큐브에서 선택된 셀에 대한 기본 데이터를 나타내는 행 집합을 반환하는 드릴스루 동작  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 동작이 발생하는 큐브에서 선택된 섹션과 연관된 보고서를 반환하는 보고 동작  
  
-   동작이 발생하는 큐브에서 선택된 섹션과 연관된 동작 요소(URL, HTML, DataSet, RowSet 및 기타 요소)를 반환하는 표준 동작  
  
 ADOMD.NET과 같은 쿼리 인터페이스는 클라이언트 응용 프로그램에서 동작을 검색하여 최종 사용자에게 노출하는 데 사용됩니다. 자세한 내용은 [ADOMD.NET을 사용하여 개발](adomd-net/developing-with-adomd-net.md)을 참조하세요.  
  
 단순 <xref:Microsoft.AnalysisServices.Action> 개체는 기본 정보, 동작이 발생하는 대상, 동작 범위를 제한하는 조건 및 유형으로 구성되어 있습니다. 기본 정보에는 동작의 이름, 동작에 대한 설명, 동작에 제안된 캡션 등이 포함됩니다.  
  
 대상은 큐브에서 동작이 발생하는 실제 위치로, 대상 유형과 대상 개체로 구성됩니다. 대상 유형은 큐브에서 동작을 활성화할 개체의 종류를 나타냅니다. 대상 유형은 수준 멤버, 셀, 계층, 계층 멤버 등일 수 있습니다. 대상 개체는 대상 유형의 특정 개체로, 대상 유형이 개체이면 대상 개체는 큐브에 정의된 계층 중 하나입니다.  
  
 조건이 `Boolean` 동작 이벤트에서 평가 되는 MDX 식입니다. 조건이를 반환 하는 경우 `true`, 동작이 실행 됩니다. 그렇지 않으면 동작이 실행되지 않습니다.  
  
 유형은 실행할 동작의 종류입니다. <xref:Microsoft.AnalysisServices.Action> 은 추상 클래스이므로 이 동작을 실행하려면 파생 클래스 중 하나를 사용해야 합니다. 두 가지 동작, 드릴스루와 보고는 미리 정의되어 있는데 해당 파생 클래스로 각각 <xref:Microsoft.AnalysisServices.DrillThroughAction> 및 <xref:Microsoft.AnalysisServices.ReportAction>을 참조하세요. 나머지 동작은 <xref:Microsoft.AnalysisServices.StandardAction> 클래스에서 처리됩니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 동작은 클라이언트 응용 프로그램에 제공되어 사용될 수 있는 저장 MDX 문입니다. 즉, 동작은 서버에 정의되고 저장되는 클라이언트 명령입니다. 동작에는 클라이언트 응용 프로그램에서 MDX 문을 표시하고 처리해야 하는 시기 및 방법을 지정하는 정보도 들어 있습니다. 작업이 지정하는 동작은 작업의 정보를 매개 변수로 사용하여 응용 프로그램을 시작하거나 작업이 제공하는 조건을 기반으로 정보를 검색할 수 있습니다.  
  
 업무용 사용자는 동작을 통해 분석 결과에 대한 작업을 수행할 수 있습니다. 동작을 저장하여 다시 사용하면 비즈니스 인텔리전스 응용 프로그램을 큐브 범위 밖으로 확장할 수 있으므로 최종 사용자가 데이터를 표시하는 일반적인 분석 이상의 작업을 수행할 수 있으며 발견된 문제와 결함을 해결할 수 있습니다. 동작은 클라이언트 응용 프로그램을 복잡한 데이터 렌더링 도구에서 기업 운영 체제의 필수 부분으로 바꿀 수 있습니다. 최종 사용자는 데이터를 작업용 응용 프로그램의 입력 항목으로 보내는 작업에 초점을 맞추는 대신 의사 결정 과정을 "마무리"할 수 있습니다. 분석 데이터를 의사 결정으로 변환하는 이 기능은 성공적인 비즈니스 인텔리전스 응용 프로그램에 매우 중요합니다.  
  
 예를 들어 큐브를 검색하는 업무용 사용자가 특정 제품의 현재 재고가 부족함을 발견한다고 가정합니다. 이 경우 클라이언트 응용 프로그램은 업무용 사용자에게 Analysis Services 데이터베이스에서 검색되었으며 모두 부족한 제품 재고 값과 관련된 동작 목록을 제공합니다. 업무용 사용자는 해당 제품을 나타내는 큐브의 멤버에 대해 주문 작업을 선택합니다. 그러면 주문 동작은 작업용 데이터베이스에서 저장 프로시저를 호출하여 새 주문을 시작합니다. 이 저장 프로시저는 주문 입력 시스템으로 보낼 적절한 정보를 생성합니다.  
  
 동작을 만들 때 유연성을 발휘할 수 있습니다. 예를 들어 동작으로 응용 프로그램을 시작하거나 데이터베이스에서 정보를 검색할 수 있습니다. 차원, 수준, 멤버 및 셀을 비롯한 대부분의 큐브 부분에서 동작이 트리거되도록 구성하거나 큐브의 같은 부분에 대해 여러 작업을 만들 수 있습니다. 동작 실행 시 시작된 응용 프로그램에 문자열 매개 변수를 전달할 수 있으며 최종 사용자에게 표시되는 캡션을 지정할 수도 있습니다.  
  
> [!IMPORTANT]  
>  업무용 사용자가 동작을 사용하려면 해당 클라이언트 응용 프로그램에서 작업을 지원해야 합니다.  
  
## <a name="types-of-actions"></a>동작 유형  
 다음 표에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 포함된 동작의 유형을 나열합니다.  
  
|동작 유형|Description|  
|-----------------|-----------------|  
|명령줄|명령 프롬프트에서 명령을 실행합니다.|  
|Dataset|데이터 집합을 클라이언트 응용 프로그램으로 반환합니다.|  
|드릴스루|행 집합을 반환하기 위해 클라이언트가 실행하는 드릴스루 문을 식으로 반환합니다.|  
|Html|인터넷 브라우저에서 HTML 스크립트를 실행합니다.|  
|소유|이 표에 나열되지 않은 인터페이스를 사용하여 작업을 수행합니다.|  
|보고서|매개 변수가 있는 URL 기반 요청을 보고서 서버로 전송하고 보고서를 클라이언트 응용 프로그램으로 반환합니다.|  
|행 집합|행 집합을 클라이언트 응용 프로그램으로 반환합니다.|  
|인수를 제거합니다.|OLE DB 명령을 실행합니다.|  
|URL|동적 웹 페이지를 인터넷 브라우저로 표시합니다.|  
  
## <a name="resolving-and-executing-actions"></a>동작 확인 및 실행  
 업무용 사용자가 명령 개체가 정의된 개체에 액세스하면 해당 동작과 연관된 문이 자동으로 확인되므로 클라이언트 응용 프로그램에서 해당 문을 사용할 수 있지만 작업이 자동으로 실행되지는 않습니다. 동작을 시작하는 클라이언트별 작업을 업무용 사용자가 수행할 때만 작업이 실행됩니다. 예를 들어 업무용 사용자가 특정 멤버나 셀을 마우스 오른쪽 단추로 클릭하는 경우 클라이언트 응용 프로그램에서 동작 목록을 팝업 메뉴로 표시할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 동작](actions-in-multidimensional-models.md)  
  
  