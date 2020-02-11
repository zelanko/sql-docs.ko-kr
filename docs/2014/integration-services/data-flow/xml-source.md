---
title: XML 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28e7a7395c02e44e52469992f3738f0d873e227f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62899946"
---
# <a name="xml-source"></a>XML 원본
  XML 원본은 XML 데이터 파일을 읽고 원본 출력의 열을 해당 데이터로 채웁니다.  
  
 XML 파일의 데이터에 계층 관계가 포함되어 있는 경우가 많습니다. 예를 들어 XML 데이터 파일은 카탈로그 및 카탈로그의 항목을 나타낼 수 있습니다. 데이터가 데이터 흐름을 시작할 수 있으려면 먼저 XML 데이터 파일에 있는 각 요소의 관계를 결정하고 파일의 각 요소에 대해 출력을 생성해야 합니다.  
  
## <a name="schemas"></a>스키마  
 XML 원본은 스키마를 사용하여 XML 데이터를 해석합니다. XML 원본은 XML 데이터를 테이블 형식으로 변환하는 인라인 스키마 또는 XML 스키마 정의(XSD) 파일 사용을 지원합니다. 
  **XML 원본 편집기** 대화 상자를 사용하여 XML 원본을 구성하면 사용자 인터페이스가 지정한 XML 데이터 파일에서 XSD를 생성할 수 있습니다.  
  
> [!NOTE]  
>  DTD는 지원되지 않습니다.  
  
 스키마는 하나의 네임스페이스만 지원할 수 있으며 스키마 컬렉션을 지원하지 않습니다.  
  
> [!NOTE]  
>  XML 원본은 XSD와 비교하여 XML 파일 데이터의 유효성을 검사하지 않습니다.  
  
## <a name="xml-source-editor"></a>XML 원본 편집기  
 XML 파일의 데이터에 계층 관계가 포함되어 있는 경우가 많습니다. 
  **XML 원본 편집기** 대화 상자는 지정한 스키마를 사용하여 XML 원본 출력을 생성합니다. XSD 파일을 지정하거나 인라인 스키마를 사용하거나 지정한 XML 데이터 파일에서 XSD를 생성할 수 있습니다. 디자인 타임에 해당 스키마를 사용할 수 있어야 합니다.  
  
 XML 원본은 XML 파일의 다른 요소가 포함된 모든 요소에 대해 출력을 만들어 XML 데이터에서 테이블 구조를 생성합니다. 예를 들어 XML 데이터가 카탈로그 및 카탈로그의 항목을 나타내는 경우 XML 원본은 카탈로그에 대한 출력과 카탈로그에 포함된 각 항목 유형에 대한 출력을 만듭니다. 각 항목의 출력에는 해당 항목의 속성에 대한 출력 열이 포함됩니다.  
  
 출력에서 데이터 계층 관계에 대한 정보를 제공하기 위해 XML 원본은 각 자식 요소의 부모 요소를 식별하는 열을 출력에 추가합니다. 여러 유형의 항목이 포함된 카탈로그를 예로 들면 각 항목은 해당 항목이 속해 있는 카탈로그를 식별하는 열 값을 갖습니다.  
  
 XML 원본은 모든 요소에 대해 출력을 만들지만 모든 출력을 사용할 필요는 없습니다. 사용하지 않을 출력을 삭제하거나 다운스트림 구성 요소에 연결하지 않을 수 있습니다.  
  
 또한 XML 원본은 출력 이름을 생성하여 이름이 명확하게 구분되게 합니다. 이러한 이름이 너무 길면 출력을 식별하는 데 도움이 되지 않을 수도 있습니다. 고유한 이름을 지정한다면 출력 이름을 바꿀 수 있습니다. 출력 열의 길이와 데이터 형식도 수정할 수 있습니다.  
  
 XML 원본은 모든 출력에 대해 오류 출력을 추가합니다. 기본적으로 오류 출력의 열은 길이가 255인 유니코드 문자열 데이터 형식(DT_WSTR)이지만 데이터 형식과 길이를 수정하여 오류 출력의 열을 구성할 수 있습니다.  
  
 XSD에 없는 요소가 XML 데이터 파일에 포함되어 있으면 해당 요소는 무시되며 출력이 생성되지 않습니다. 반면 XSD에 표시된 요소가 XML 데이터 파일에 없을 경우 Null 값을 가진 열이 출력에 포함됩니다.  
  
 XML 데이터 파일에서 데이터를 추출하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환됩니다. 그러나 XML 원본은 DT_TIME2 또는 DT_DBTIMESTAMP2 데이터 형식을 지원하지 않기 때문에 XML 데이터를 이러한 데이터 형식으로 변환할 수 없습니다. 자세한 내용은 [Integration Services 데이터 형식](integration-services-data-types.md)을 참조 하세요.  
  
 XSD 또는 인라인 스키마에서 요소의 데이터 형식을 지정할 수도 있지만 그렇지 않을 경우 **XML 원본 편집기** 대화 상자는 요소가 포함된 출력 열에 유니코드 문자열 데이터 형식(DT_WSTR)을 할당하고 열 길이를 255자로 설정합니다.  
  
 스키마에서 요소의 최대 길이를 지정하는 경우 출력 열의 길이는 이 값으로 설정됩니다. 요소가 변환되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에서 지원되는 길이보다 최대 길이가 큰 경우 해당 데이터 형식의 최대 길이로 데이터가 잘립니다. 예를 들어 문자열의 길이가 5,000자인 경우 DT_WSTR 데이터 형식의 최대 길이는 4,000자이므로 4,000자로 잘리며 BYTE 데이터는 DT_BYTES 데이터 형식의 최대 길이인 8,000자로 잘립니다. 스키마에서 최대 길이를 지정하지 않는 경우 두 데이터 형식의 열 기본 길이는 255자로 설정됩니다. XML 원본에서의 데이터 잘림은 다른 데이터 흐름 구성 요소에서의 잘림과 동일하게 처리됩니다. 자세한 내용은 [데이터 오류 처리](error-handling-in-data.md)를 참조하세요.  
  
 데이터 형식과 열 길이는 수정할 수 있습니다. 자세한 내용은 [Integration Services 데이터 형식](integration-services-data-types.md)을 참조 하세요.  
  
## <a name="configuration-of-the-xml-source"></a>XML 원본 구성  
 XML 원본은 3가지 데이터 액세스 모드를 지원합니다. XML 데이터 파일의 파일 위치, 이 파일 위치가 포함된 변수 또는 XML 데이터가 포함된 변수를 지정할 수 있습니다.  
  
 XML 원본은 패키지 로드 시 속성 식을 사용하여 업데이트할 수 있는 `XMLData` 및 `XMLSchemaDefinition` 사용자 지정 속성을 포함합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../expressions/use-property-expressions-in-packages.md) 및 [XML 원본 사용자 지정 속성](xml-source-custom-properties.md)을 참조하세요.  
  
 XML 원본은 여러 개의 일반 출력과 여러 개의 오류 출력을 지원합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] xml 원본을 구성 하기 위한 **xml 원본 편집기**대화 상자를 포함 합니다. 이 대화 상자는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 사용할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 
  **XML 원본 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [연결 관리자 페이지 &#40;XML 원본 편집기&#41;](../xml-source-editor-connection-manager-page.md)  
  
-   [XML 원본 편집기 &#40;열 페이지&#41;](../xml-source-editor-columns-page.md)  
  
-   [XML 원본 편집기 &#40;오류 출력 페이지&#41;](../xml-source-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [XML 원본 사용자 지정 속성](xml-source-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [XML 원본을 사용하여 데이터 추출](xml-source.md)  
  
## <a name="related-content"></a>관련 내용  
 [XML 파일을 사용 하 여 SSIS 패키지를 구성](https://www.sqlshack.com/using-xml-file-configure-ssis-package/)하는 기술 문서.  
  
  
