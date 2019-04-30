---
title: DMX 쿼리 편집기 (Analysis Services-데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.dmx.f1
ms.assetid: 7ac877a1-0f29-46b9-9a51-73b02172bef1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 063e78a15a4bd365c4eb061cc54454fb6e6637c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731613"
---
# <a name="dmx-query-editor-analysis-services---data-mining"></a>DMX 쿼리 편집기(Analysis Services - 데이터 마이닝)
  DMX 쿼리 편집기를 사용하여 DMX(Data Mining Extensions) 언어로 작성된 문을 디자인 및 실행할 수 있습니다.  
  
## <a name="features"></a>기능  
  
-   DMX 쿼리 편집기의 쿼리 편집기 창에 스크립트를 입력합니다.  
  
-   스크립트를 실행하려면 **F5**키를 누르거나 도구 모음 또는 **쿼리** 메뉴의 **실행** 을 클릭합니다. 코드의 일부만 선택하면 선택한 부분만 실행됩니다. 코드를 선택하지 않으면 DMX 쿼리 편집기에 있는 코드 전체가 실행됩니다.  
  
-   메타데이터 창에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 포함된 큐브 및 기타 개체의 메타데이터를 봅니다.  
  
-   DMX 구문에 대한 도움말을 보려면 DMX 쿼리 편집기에서 키워드를 선택한 다음 **F1**키를 누릅니다.  
  
-   DMX 구문에 대한 동적 도움말을 보려면 **도움말** 메뉴에서 **동적 도움말** 을 클릭하여 동적 도움말 구성 요소를 엽니다. 동적 도움말을 사용하면 쿼리 편집기에서 키워드를 입력할 때 **동적 도움말** 창에 도움말 항목이 나타납니다.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>SQL Server Analysis Services 편집기 도구 모음  
 DMX 쿼리 편집기를 열면 다음 표에 나열된 단추가 있는 **SQL Server Analysis Services 편집기** 도구 모음이 표시됩니다.  
  
|용어|정의|  
|----------|----------------|  
|**연결**|Analysis Services 인스턴스에 대한 연결을 설정할 수 있는 **서버에 연결** 대화 상자를 엽니다.|  
|**연결 끊기**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 DMX 쿼리 편집기의 연결을 끊습니다.|  
|**연결 변경**|다른 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 설정할 수 있는 **서버에 연결** 대화 상자를 엽니다.|  
|**현재 연결에서의 새 쿼리**|현재 DMX 쿼리 편집기 창의 연결 정보를 사용하여 새 DMX 쿼리 편집기 창을 엽니다.|  
|**사용 가능한 데이터베이스**|같은 인스턴스의 다른 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스로 연결을 변경합니다.|  
|**실행**|선택한 코드를 실행하거나, 코드를 선택하지 않은 경우 DMX 쿼리 편집기에 있는 코드 전체를 실행합니다.|  
|**구문 분석**|선택한 코드의 구문을 검사합니다. 코드를 선택하지 않은 경우 DMX 쿼리 편집기 창에 있는 전체 코드의 구문을 확인합니다.|  
|**쿼리 실행 취소**|취소 요청을 서버로 보냅니다. 일부 쿼리는 바로 취소할 수 없으며 적절한 취소 조건이 될 때까지 기다려야 합니다. 쿼리를 취소해도 트랜잭션이 롤백되는 동안 취소가 지연될 수 있습니다.|  
  
## <a name="dmx-query-editor-window"></a>DMX 쿼리 편집기 창  
 다음 표에 나열된 옵션은 DMX 쿼리 편집기에서 사용할 수 있습니다.  
  
|용어|정의|  
|----------|----------------|  
|**쿼리 편집기 창**|DMX 쿼리 편집기에서 실행할 DMX 문 및 스크립트를 입력합니다.<br /><br /> 쿼리 편집기의 상황에 맞는 메뉴에서는 다음 옵션을 제공합니다.<br /><br /> **잘라내기**: 현재 선택 영역을 클립보드에 복사하고 쿼리 편집기 창에서 선택 영역을 제거합니다.<br /><br /> **복사**: 현재 선택 영역을 클립보드에 복사합니다.<br /><br /> **붙여넣기**: 클립보드의 내용을 현재 선택 영역에 붙여넣습니다.<br /><br /> **연결**: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 설정할 수 있는 **서버에 연결** 대화 상자를 엽니다.<br /><br /> **연결 끊기**: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 현재 쿼리 편집기의 연결을 끊습니다.<br /><br /> **모든 쿼리 연결 끊기**: 열려 있는 모든 쿼리 편집기의 연결을 끊습니다.<br /><br /> **연결 변경**: 다른 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 설정할 수 있는 **서버에 연결** 대화 상자를 엽니다.<br /><br /> **개체 탐색기에서 서버 열기**: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체 탐색기 **에서 현재 쿼리 편집기가 연결된**인스턴스를 엽니다.<br /><br /> **실행**: 선택한 코드를 실행하거나, 코드를 선택하지 않은 경우 현재 쿼리 편집기에 있는 코드 전체를 실행합니다.<br /><br /> **속성 창**: **에서 현재 쿼리 창에 대한** 속성 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 창을 표시합니다.<br /><br /> **쿼리 옵션**: **쿼리 옵션** 대화 상자를 표시합니다.|  
|**메타 데이터 창**|현재 연결된 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 메타데이터를 표시합니다.|  
|**Cube**|현재 연결된 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에서 **메타데이터** 탭의 해당 큐브와 연결된 메타데이터를 표시할 큐브를 선택합니다.|  
|**메타데이터**|측정값 그룹과 측정값, 핵심 성과 지표, 차원, 계층, 수준, 멤버, 멤버 속성 등 **큐브**에서 선택한 큐브의 메타데이터를 표시합니다. 개체의 정규화된 키를 검색하려면 다음 중 하나를 수행하십시오.<br /><br /> 개체를 **메타데이터** 탭에서 쿼리 창으로 끌어 옵니다.<br /><br /> 또는:<br /><br /> 개체를 마우스 오른쪽 단추로 클릭하고 **복사**를 선택한 다음 쿼리 창을 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.|  
|**함수**|DMSCHEMA_MINING_FUNCTIONS 스키마 행 집합에서 검색된 대로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 사용할 수 있는 DMX 함수에 대한 메타데이터를 표시합니다.<br /><br /> 함수 구문을 검색하려면 다음 중 하나를 수행하십시오.<br /><br /> 개체를 **함수** 탭에서 쿼리 창으로 끌어 옵니다.<br /><br /> 또는:<br /><br /> 함수를 마우스 오른쪽 단추로 클릭하고 **복사**를 선택한 다음 쿼리 창을 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.|  
|**결과 창**|DMX 문의 결과를 표에 표시합니다.|  
|**메시지 창**|DMX 문 실행 방법에 대한 정보를 표시합니다. 예를 들어 이 창은 실행 중 발견된 모든 오류 또는 실행 후 검색된 셀 수를 표시합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Data Mining Extensions & #40; DMX & #41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)   
 [MDX 쿼리 편집기 &#40;Analysis Services-다차원 데이터&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [XMLA 쿼리 편집기 &#40;Analysis Services-다차원 데이터&#41;](xmla-query-editor-analysis-services-multidimensional-data.md)   
 [쿼리 및 텍스트 편집기 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [SQL Server Management Studio 바로 가기 키](../ssms/sql-server-management-studio-keyboard-shortcuts.md)   
 [메뉴 및 바로 가기 키 사용자 지정](../ssms/customize-menus-and-shortcut-keys.md)   
 [쿼리 편집기에서 코드 색상 지정](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
