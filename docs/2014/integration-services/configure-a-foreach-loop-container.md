---
title: Foreach 루프 컨테이너 구성 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9d63a4f168c4a426c06bb00c634f89e328735332
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159763"
---
# <a name="configure-a-foreach-loop-container"></a>Foreach 루프 컨테이너 구성
  이 절차에서는 열거자 및 컨테이너 수준의 속성 식을 비롯한 Foreach 루프 컨테이너를 구성하는 방법에 대해 설명합니다.  
  
### <a name="to-configure-the-foreach-loop-container"></a>Foreach 루프 컨테이너를 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **제어 흐름** 탭을 클릭하고 Foreach 루프를 두 번 클릭합니다.  
  
3.  **Foreach 루프 편집기** 대화 상자에서 **일반** 을 클릭하고 선택적으로 Foreach 루프의 이름과 설명을 수정합니다.  
  
4.  **컬렉션** 을 클릭하고 **Enumerator** 목록에서 열거자 유형을 선택합니다.  
  
5.  열거자를 지정하고 열거자 옵션을 다음과 같이 설정합니다.  
  
    -   Foreach File 열거자를 사용하려면 열거할 파일이 들어 있는 폴더를 제공하고, 파일 이름 및 유형에 대한 필터를 지정하고, 정규화된 파일 이름을 반환할지 여부를 지정합니다. 또한 하위 폴더의 파일에 대해서도 동일 작업을 반복할지 여부를 나타냅니다.  
  
    -   Foreach Item 열거자를 사용하려면 **열**을 클릭하고 **For Each Item 열** 대화 상자에서 **추가** 를 클릭하여 열을 추가합니다. **데이터 형식** 목록에서 각 열에 대한 데이터 형식을 선택하고 **확인**을 클릭합니다.  
  
         열에 값을 입력하거나 목록에서 값을 선택합니다.  
  
        > [!NOTE]  
        >  새 행을 추가하려면 입력한 셀 바깥의 아무 곳이나 클릭합니다.  
  
        > [!NOTE]  
        >  값이 열 데이터 형식과 호환되지 않으면 텍스트가 강조 표시됩니다.  
  
    -   Foreach ADO 열거자를 사용하려면 기존 변수를 선택하거나 **ADO 개체 원본 변수** 목록에서 **새 변수** 를 클릭하여 열거할 ADO 개체의 이름이 들어 있는 변수를 지정하고 열거 모드 옵션을 선택합니다.  
  
         새 변수를 만드는 경우에는 **변수 추가** 대화 상자에서 변수 속성을 설정합니다.  
  
    -   Foreach ADO.NET 스키마 행 집합 열거자를 사용하려면 기존 ADO.NET 연결을 선택하거나 **연결** 목록에서 **새 연결** 을 클릭한 후 스키마를 선택합니다.  
  
         필요에 따라 **제한 설정** 을 클릭하여 스키마 제한을 선택하고, 제한 값이 있는 변수를 선택하거나 제한 값을 입력한 다음 **확인**을 클릭합니다.  
  
    -   Foreach From Variable 열거자를 사용하려면 **변수** 목록에서 변수를 선택합니다.  
  
    -   Foreach NodeList 열거자를 사용하려면 DocumentSourceType을 클릭하고 목록에서 원본 유형을 선택한 다음 DocumentSource를 클릭합니다. DocumentSourceType에 대해 선택한 값에 따라 목록에서 변수 또는 파일 연결을 선택하거나, 새 변수 또는 파일 연결을 만들거나, **문서 원본 편집기**에서 XML 원본을 입력합니다.  
  
         그런 다음 EnumerationType을 클릭하고 목록에서 열거형 형식을 선택합니다. EnumerationType이 **Navigator, Node 또는 NodeText**이면 OuterXPathStringSourceType을 클릭하고 원본 유형을 선택한 다음 OuterXPathString을 클릭합니다. OuterXPathStringSourceType에 대해 설정된 값에 따라 목록에서 변수 또는 파일 연결을 선택하거나, 새 변수 또는 파일 연결을 만들거나, 외부 XPath(XML Path Language) 식에 대한 문자열을 입력합니다.  
  
         EnumerationType이 **ElementCollection**이면 위에서 설명한 대로 OuterXPathStringSourceType 및 OuterXPathString을 설정합니다. 그런 다음 InnerElementType을 클릭하고 내부 요소에 대한 열거형 형식을 선택한 다음 InnerXPathStringSourceType을 클릭합니다. InnerXPathStringSourceType에 대해 설정된 값에 따라 변수 또는 파일 연결을 선택하거나, 새 변수 또는 파일 연결을 만들거나, 내부 XPath 식에 대한 문자열을 입력합니다.  
  
    -   Foreach SMO 열거자를 사용하려면 기존 ADO.NET 연결을 선택하거나 **연결** 목록에서 **새 연결** 을 클릭한 후 사용할 문자열을 입력하거나 **찾아보기**를 클릭합니다. **찾아보기**를 클릭한 경우 **SMO 열거 선택** 대화 상자에서 열거할 개체 유형과 열거 유형을 선택하고 **확인**을 클릭합니다.  
  
6.  선택적으로 **컬렉션** 페이지의 **식** 입력란에서 찾아보기 단추 **(...)** 를 클릭하여 속성 값을 업데이트하는 식을 만듭니다. 자세한 내용은 [속성 식 추가 또는 변경](expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
    > [!NOTE]  
    >  **속성** 목록에 나열되는 속성은 열거자에 따라 다릅니다.  
  
7.  선택적으로 **변수 매핑** 을 클릭하여 컬렉션 값에 개체 속성을 매핑한 후 다음을 수행합니다.  
  
    1.  **변수** 목록에서 변수를 선택하거나 **\<새 변수>** 를 클릭하여 새 변수를 만듭니다.  
  
    2.  새 변수를 추가하는 경우에는 **변수 추가** 대화 상자에서 변수 속성을 설정하고 **확인**을 클릭합니다.  
  
    3.  For Each Item 열거자를 사용하는 경우 **인덱스** 목록에서 인덱스 값을 업데이트할 수 있습니다.  
  
        > [!NOTE]  
        >  인덱스 값은 항목에서 변수로 매핑될 열을 나타냅니다. For Each Item 열거자에서만 0이 아닌 인덱스 값을 사용할 수 있습니다.  
  
8.  선택적으로 **식** 페이지에서 **Expressions** 를 클릭하고 Foreach 루프 컨테이너의 속성에 대한 속성 식을 만듭니다. 자세한 내용은 [속성 식 추가 또는 변경](expressions/add-or-change-a-property-expression.md)을 참조하세요.  
  
9. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Foreach 루프 컨테이너](control-flow/foreach-loop-container.md)  
  
  
