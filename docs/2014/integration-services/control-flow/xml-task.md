---
title: XML 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.xmltask.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8278f24e51e6288eb31f2f8ac4ec941a7f23e3aa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093127"
---
# <a name="xml-task"></a>XML 태스크
  XML 태스크는 XML 데이터를 통한 작업 시 사용됩니다. 패키지는 이 태스크를 사용하여 XML 문서를 검색하고, XSLT(Extensible Stylesheet Language Transformations) 스타일시트 및 XPath 식을 통해 문서에 작업을 적용하고, 여러 문서를 병합하거나 업데이트된 문서를 파일 및 변수에 대해 유효성을 검사하고, 비교 및 저장할 수 있습니다.  
  
 이 태스크를 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 XML 문서를 런타임에 동적으로 수정할 수 있습니다. XML 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   XML 문서 형식을 다시 지정합니다. 예를 들어 태스크에서 XML 파일에 있는 보고서에 액세스하고 XSLT 스타일시트를 동적으로 적용하여 문서를 사용자 지정 방식으로 표현할 수 있습니다.  
  
-   XML 문서의 섹션을 선택합니다. 예를 들어 태스크에서 XML 파일에 있는 보고서에 액세스하고 XPath 식을 동적으로 적용하여 문서의 섹션을 선택할 수 있습니다. 이 작업은 문서의 값을 가져오고 처리할 수도 있습니다.  
  
-   여러 원본으로부터 문서를 병합합니다. 예를 들어 태스크에서 여러 원본으로부터 보고서를 다운로드하고 이를 하나의 포괄적인 XML 문서로 동적으로 병합할 수 있습니다.  
  
-   XML 문서의 유효성을 검사하고 필요에 따라 자세한 오류 출력을 가져옵니다. 자세한 내용은 [Validate XML with the XML Task](xml-task.md)를 참조하십시오.  
  
 XML 원본을 사용하여 XML 문서에서 값을 추출하면 데이터 흐름에 XML 데이터를 포함시킬 수 있습니다. 자세한 내용은 [XML Source](../data-flow/xml-source.md)을 참조하세요.  
  
## <a name="xml-operations"></a>XML 작업  
 XML 태스크에서 수행하는 첫 번째 동작은 특정 XML 문서를 검색하는 것입니다. 이 동작은 XML 태스크에 포함되며 자동으로 발생합니다. 검색된 XML 문서는 XML 태스크에서 수행하는 작업에 대한 데이터 원본으로 사용됩니다.  
  
 비교, 병합 및 패치와 같은 XML 작업에는 두 개의 피연산자가 필요합니다. 첫 번째 피연산자는 원본 XML 문서를 지정합니다. 두 번째 피연산자도 XML 문서를 지정하지만 이 문서의 내용은 작업 요구 사항에 따라 달라집니다. 예를 들어 비교 작업은 두 문서를 비교하므로 두 번째 피연산자는 원본 XML 문서가 비교될 비슷한 다른 XML 문서를 지정합니다.  
  
 XML 태스크는 변수나 파일 연결 관리자를 원본으로 사용하거나 태스크 속성에 XML 데이터를 포함시킬 수 있습니다.  
  
 원본이 변수인 경우 지정된 변수에는 XML 문서의 경로가 포함됩니다.  
  
 원본이 파일 연결 관리자인 경우 지정된 파일 연결 관리자는 원본 정보를 제공합니다. 파일 연결 관리자는 XML 태스크와 별도로 구성되며 XML 태스크에서 참조됩니다. 파일 연결 관리자의 연결 문자열은 XML 파일의 경로를 지정합니다. 자세한 내용은 [File Connection Manager](../connection-manager/file-connection-manager.md)를 참조하세요.  
  
 XML 태스크는 작업 결과를 변수나 파일로 저장하도록 구성될 수 있습니다. 파일로 저장하는 경우 XML 태스크는 파일 연결 관리자를 사용하여 파일에 액세스합니다. 또한 비교 작업으로 생성된 Diffgram의 결과를 파일 및 변수로 저장할 수 있습니다.  
  
## <a name="predefined-xml-operations"></a>미리 정의된 XML 작업  
 XML 태스크에는 XML 문서 작업을 위해 미리 정의된 일련의 작업이 포함됩니다. 다음 표에서는 이러한 작업을 설명합니다.  
  
|연산|Description|  
|---------------|-----------------|  
|Diff|두 개의 XML 문서를 비교합니다. 원본 XML 문서를 기본 문서로 사용하는 비교 작업은 원본 XML 문서를 보조 XML 문서와 비교하고, 차이점을 검색하고, 해당 차이점을 XML Diffgram 문서에 기록합니다. 이 작업에는 비교를 사용자 지정하기 위한 속성이 포함됩니다.|  
|병합|두 개의 XML 문서를 병합합니다. 원본 XML 문서를 기본 문서로 사용하는 병합 작업은 보조 문서의 내용을 기본 문서에 추가합니다. 이 작업에서는 기본 문서 내의 병합 위치를 지정할 수 있습니다.|  
|Patch|Diffgram 문서로 불리는 비교 작업의 출력을 XML 문서에 적용하여 Diffgram 문서 내용이 포함된 새로운 상위 문서를 만듭니다.|  
|유효성 검사|DTD(문서 유형 정의) 또는 XSD(XML 스키마 정의) 스키마와 비교하여 XML 문서의 유효성을 검사합니다.|  
|XPath|XPath 쿼리 및 계산을 수행합니다.|  
|XSLT|XML 문서에 대해 XSL 변환을 수행합니다.|  
  
### <a name="diff-operation"></a>비교 작업  
 비교 작업의 속도 또는 정확도가 필요한지 여부에 따라 다른 비교 알고리즘을 사용하도록 비교 작업을 구성할 수 있습니다. 또한 비교되는 문서의 크기를 기준으로 빠른 비교나 정확한 비교를 자동으로 선택하도록 작업을 구성할 수 있습니다.  
  
 비교 작업에는 XML 비교를 사용자 지정하는 일련의 옵션이 포함됩니다. 다음 표에서는 옵션에 대해 설명합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**IgnoreComments**|열 노드가 비교되는지 여부를 지정하는 값입니다.|  
|**IgnoreNamespaces**|요소의 네임스페이스 URI(Uniform Resource Identifier)와 해당 특성 이름이 비교되는지 여부를 지정하는 값입니다. 이 옵션 설정 하는 경우 `true`, 로컬 이름이 같지만 네임 스페이스가 다른 두 요소는 동일한 것으로 간주 됩니다.|  
|**IgnorePrefixes**|요소의 접두사 및 특성 이름이 비교되는지 여부를 지정하는 값입니다. 이 옵션 설정 하는 경우 `true,` 로컬 이름은 같지만 다른 네임 스페이스 URI 및 접두사가 있는 두 가지 요소는 동일한 것으로 간주 합니다.|  
|**IgnoreXMLDeclaration**|XML 선언이 비교되는지 여부를 지정하는 값입니다.|  
|**IgnoreOrderOfChildElements**|자식 요소의 순서가 비교되는지 여부를 지정하는 값입니다. 이 옵션을 `true`로 설정하면 형제 목록에서 위치만 다른 자식 요소는 동일한 것으로 간주됩니다.|  
|**IgnoreWhiteSpaces**|공백이 비교되는지 여부를 지정하는 값입니다.|  
|**IgnoreProcessingInstructions**|처리 명령이 비교되는지 여부를 지정하는 값입니다.|  
|**IgnoreDTD**|DTD가 무시되는지 여부를 지정하는 값입니다.|  
  
### <a name="merge-operation"></a>병합 작업  
 XPath 문을 사용하여 원본 문서의 병합 위치를 식별하는 경우 이 문은 단일 노드를 반환해야 합니다. 여러 노드가 반환되는 경우에는 첫 번째 노드만 사용됩니다. 두 번째 문서의 내용은 XPath 쿼리에서 반환하는 첫 번째 노드 아래에 병합됩니다.  
  
### <a name="xpath-operation"></a>XPath 작업  
 XPath 작업은 다른 유형의 XPath 기능을 사용하도록 구성될 수 있습니다.  
  
-   sum()과 같은 XPath 함수를 구현하려면 **Evaluation** 옵션을 선택합니다.  
  
-   선택된 노드를 XML 조각으로 반환하려면 **Node list** 옵션을 선택합니다.  
  
-   선택한 모든 노드의 내부 텍스트 값을 연결된 문자열로 반환하려면 **Values** 옵션을 선택합니다.  
  
### <a name="validation-operation"></a>유효성 검사 작업  
 유효성 검사 작업은 DTD(문서 유형 정의) 또는 XSD(XML 스키마 정의) 스키마를 사용하도록 구성될 수 있습니다.  
  
 사용 하도록 설정 `ValidationDetails` 자세한 오류 출력을 얻으려고 합니다. 자세한 내용은 [Validate XML with the XML Task](xml-task.md)를 참조하십시오.  
  
## <a name="xml-document-encoding"></a>XML 문서 인코딩  
 XML 태스크는 유니코드 문서의 병합만 지원합니다. 즉, 태스크에서 유니코드 인코딩이 포함된 문서로만 병합 작업을 적용할 수 있습니다. 다른 인코딩을 사용하면 XML 태스크가 실패합니다.  
  
> [!NOTE]  
>  비교 및 패치 작업에는 두 번째 피연산자 XML 데이터의 XML 선언을 무시하는 옵션이 포함되어 있어서 다른 인코딩이 포함된 문서를 해당 작업에서 사용할 수 있습니다.  
  
 XML 문서를 사용할 수 있는지 여부를 확인하려면 XML 선언을 확인하십시오. 선언에는 8비트 유니코드 인코딩을 나타내는 UTF-8이 명시적으로 지정되어야 합니다.  
  
 다음 태그는 유니코드 8비트 인코딩을 보여 줍니다.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>XML 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 XML 태스크에 대한 사용자 지정 로그 항목을 설명합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`XMLOperation`|태스크에서 수행한 작업에 대한 정보를 제공합니다.|  
  
## <a name="configuration-of-the-xml-task"></a>XML 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [XML 태스크 편집기 &#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [XML 태스크를 사용하여 XML 유효성 검사](xml-task.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>XML 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   agilebi.com의 블로그 항목 - [XML 대상 스크립트 구성 요소](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/)  
  
-   www.codeplex.com의 CodePlex 예제 - [프로세스 XML 데이터 패키지 예제](http://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)  
  
  