---
title: "XML 태스크 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.xmltask.f1
- sql13.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 05d4d7b905c0539a67120983a562ee6936791c97
ms.contentlocale: ko-kr
ms.lasthandoff: 08/11/2017

---
# <a name="xml-task"></a>XML Task
  XML 태스크는 XML 데이터를 통한 작업 시 사용됩니다. 패키지는 이 태스크를 사용하여 XML 문서를 검색하고, XSLT(Extensible Stylesheet Language Transformations) 스타일시트 및 XPath 식을 통해 문서에 작업을 적용하고, 여러 문서를 병합하거나 업데이트된 문서를 파일 및 변수에 대해 유효성을 검사하고, 비교 및 저장할 수 있습니다.  
  
 이 태스크를 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 XML 문서를 런타임에 동적으로 수정할 수 있습니다. XML 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   XML 문서 형식을 다시 지정합니다. 예를 들어 태스크에서 XML 파일에 있는 보고서에 액세스하고 XSLT 스타일시트를 동적으로 적용하여 문서를 사용자 지정 방식으로 표현할 수 있습니다.  
  
-   XML 문서의 섹션을 선택합니다. 예를 들어 태스크에서 XML 파일에 있는 보고서에 액세스하고 XPath 식을 동적으로 적용하여 문서의 섹션을 선택할 수 있습니다. 이 작업은 문서의 값을 가져오고 처리할 수도 있습니다.  
  
-   여러 원본으로부터 문서를 병합합니다. 예를 들어 태스크에서 여러 원본으로부터 보고서를 다운로드하고 이를 하나의 포괄적인 XML 문서로 동적으로 병합할 수 있습니다.  
  
-   XML 문서의 유효성을 검사하고 필요에 따라 자세한 오류 출력을 가져옵니다. 자세한 내용은 [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)를 참조하십시오.  
  
 XML 원본을 사용하여 XML 문서에서 값을 추출하면 데이터 흐름에 XML 데이터를 포함시킬 수 있습니다. 자세한 내용은 [XML Source](../../integration-services/data-flow/xml-source.md)을 참조하세요.  
  
## <a name="xml-operations"></a>XML 작업  
 XML 태스크에서 수행하는 첫 번째 동작은 특정 XML 문서를 검색하는 것입니다. 이 동작은 XML 태스크에 포함되며 자동으로 발생합니다. 검색된 XML 문서는 XML 태스크에서 수행하는 작업에 대한 데이터 원본으로 사용됩니다.  
  
 비교, 병합 및 패치와 같은 XML 작업에는 두 개의 피연산자가 필요합니다. 첫 번째 피연산자는 원본 XML 문서를 지정합니다. 두 번째 피연산자도 XML 문서를 지정하지만 이 문서의 내용은 작업 요구 사항에 따라 달라집니다. 예를 들어 비교 작업은 두 문서를 비교하므로 두 번째 피연산자는 원본 XML 문서가 비교될 비슷한 다른 XML 문서를 지정합니다.  
  
 XML 태스크는 변수나 파일 연결 관리자를 원본으로 사용하거나 태스크 속성에 XML 데이터를 포함시킬 수 있습니다.  
  
 원본이 변수인 경우 지정된 변수에는 XML 문서의 경로가 포함됩니다.  
  
 원본이 파일 연결 관리자인 경우 지정된 파일 연결 관리자는 원본 정보를 제공합니다. 파일 연결 관리자는 XML 태스크와 별도로 구성되며 XML 태스크에서 참조됩니다. 파일 연결 관리자의 연결 문자열은 XML 파일의 경로를 지정합니다. 자세한 내용은 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)를 참조하세요.  
  
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
|**IgnoreNamespaces**|요소의 네임스페이스 URI(Uniform Resource Identifier)와 해당 특성 이름이 비교되는지 여부를 지정하는 값입니다. 이 옵션을 **true**로 설정하면 로컬 이름이 같지만 네임스페이스가 다른 두 요소는 동일한 것으로 간주됩니다.|  
|**IgnorePrefixes**|요소의 접두사 및 특성 이름이 비교되는지 여부를 지정하는 값입니다. 이 옵션을 **true,** 로 설정하면 로컬 이름이 같지만 네임스페이스 URI가 다른 두 요소는 동일한 것으로 간주됩니다.|  
|**IgnoreXMLDeclaration**|XML 선언이 비교되는지 여부를 지정하는 값입니다.|  
|**IgnoreOrderOfChildElements**|자식 요소의 순서가 비교되는지 여부를 지정하는 값입니다. 이 옵션을 **true**로 설정하면 형제 목록에서 위치만 다른 자식 요소는 동일한 것으로 간주됩니다.|  
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
  
 **ValidationDetails** 를 사용하도록 설정하여 자세한 오류 출력을 가져옵니다. 자세한 내용은 [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)를 참조하십시오.  
  
## <a name="xml-document-encoding"></a>XML 문서 인코딩  
 XML 태스크는 유니코드 문서의 병합만 지원합니다. 즉, 태스크에서 유니코드 인코딩이 포함된 문서로만 병합 작업을 적용할 수 있습니다. 다른 인코딩을 사용하면 XML 태스크가 실패합니다.  
  
> [!NOTE]  
>  비교 및 패치 작업에는 두 번째 피연산자 XML 데이터의 XML 선언을 무시하는 옵션이 포함되어 있어서 다른 인코딩이 포함된 문서를 해당 작업에서 사용할 수 있습니다.  
  
 XML 문서를 사용할 수 있는지 여부를 확인하려면 XML 선언을 확인하십시오. 선언에는 8비트 유니코드 인코딩을 나타내는 UTF-8이 명시적으로 지정되어야 합니다.  
  
 다음 태그는 유니코드 8비트 인코딩을 보여 줍니다.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>XML 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 XML 태스크에 대한 사용자 지정 로그 항목을 설명합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**XMLOperation**|태스크에서 수행한 작업에 대한 정보를 제공합니다.|  
  
## <a name="configuration-of-the-xml-task"></a>XML 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [XML 태스크를 사용 하 여 XML 유효성 검사](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>XML 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="xml-task-editor-general-page"></a>XML 태스크 편집기(일반 페이지)
  **XML 태스크 편집기** 대화 상자의 **일반** 노드를 사용하여 작업 유형을 지정하고 작업을 구성할 수 있습니다.  
  
 이 태스크에 대 한 자세한 내용은 [Validate XML with the XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)합니다. XML 문서 및 데이터 작업 방법은 MSDN Library의 "[.NET Framework에 XML 적용(Employing XML in the .NET Framework)](http://go.microsoft.com/fwlink/?LinkId=56214)"을 참조하십시오.  
  
### <a name="static-options"></a>정적 옵션  
 **OperationType**  
 목록에서 작업 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**유효성 검사**|DTD(문서 유형 정의) 또는 XSD(XML 스키마 정의) 스키마와 비교하여 XML 문서의 유효성을 검사합니다. 이 옵션을 선택하면 아래의 **Validate**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**XSLT**|XML 문서에 대해 XSL 변환을 수행합니다. 이 옵션을 선택하면 아래의 **XSLT**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**XPATH**|XPath 쿼리 및 계산을 수행합니다. 이 옵션을 선택하면 아래의 **XPATH**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**병합**|두 개의 XML 문서를 병합합니다. 이 옵션을 선택하면 아래의 **Merge**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Diff**|두 개의 XML 문서를 비교합니다. 이 옵션을 선택하면 아래의 **Diff**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Patch**|비교 작업의 출력을 적용하여 새 문서를 만듭니다. 이 옵션을 선택하면 아래의 **Patch**섹션에 설명된 동적 옵션이 표시됩니다.|  
  
 **SourceType**  
 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **원본**  
 **Source** 를 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **소스** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **소스** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭  **\<새 변수... >** 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="operationtype-dynamic-options"></a>OperationType 동적 옵션  
  
#### <a name="operationtype--validate"></a>OperationType = Validate  
 유효성 검사 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 유효성 검사 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 기존 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **ValidationType**  
 유효성 검사 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**DTD**|DTD(문서 유형 정의)를 사용합니다.|  
|**XSD**|XSD(XML 스키마 정의) 스키마를 사용합니다. 이 옵션을 선택하면 아래의 **ValidationType**섹션에 설명된 동적 옵션이 표시됩니다.|  
  
 **FailOnValidationFail**  
 문서의 유효성 검사에 실패하는 경우 작업이 실패할지 여부를 지정합니다.  
  
 **ValidationDetails**  
 이 속성의 값이 true일 때 풍부한 오류 출력을 제공합니다. 자세한 내용은 [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)를 참조하십시오.  
  
### <a name="validationtype-dynamic-options"></a>ValidationType 동적 옵션  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 두 번째 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 **SecondOperandType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **SecondOperandType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **XPathStringSourceType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--xslt"></a>OperationType = XSLT  
 XSLT 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 XSLT 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 경우 **DestinationType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **DestinationType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 두 번째 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 **SecondOperandType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **SecondOperandType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **XPathStringSourceType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--xpath"></a>OperationType = XPATH  
 XPath 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 XPath 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 경우 **DestinationType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **DestinationType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 두 번째 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 **SecondOperandType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **SecondOperandType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **XPathStringSourceType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **PutResultInOneNode**  
 결과를 단일 노드에 쓸지 여부를 지정합니다.  
  
 **XPathOperation**  
 XPath 결과 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**Evaluation**|XPath 함수의 결과를 반환합니다.|  
|**노드 목록**|선택한 노드를 XML 조각으로 반환합니다.|  
|**값**|선택한 모든 노드의 내부 텍스트 값을 연결 문자열로 반환합니다.|  
  
#### <a name="operationtype--merge"></a>OperationType = Merge  
 병합 작업에 대한 옵션을 지정합니다.  
  
 **XPathStringSourceType**  
 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **XPathStringSource**  
 **XPathStringSourceType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **XPathStringSourceType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **XPathStringSourceType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 XPath 문을 사용하여 원본 문서의 병합 위치를 식별하는 경우 이 문은 단일 노드를 반환해야 합니다. 여러 노드가 반환되는 경우에는 첫 번째 노드만 사용됩니다. 두 번째 문서의 내용은 XPath 쿼리에서 반환하는 첫 번째 노드 아래에 병합됩니다.  
  
 **SaveOperationResult**  
 XML 태스크가 병합 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 경우 **DestinationType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **DestinationType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 두 번째 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 **SecondOperandType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **SecondOperandType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **SecondOperandType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--diff"></a>OperationType = Diff  
 비교 작업에 대한 옵션을 지정합니다.  
  
 **DiffAlgorithm**  
 문서를 비교할 때 사용할 비교 알고리즘을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**자동**|XML 태스크에서 처리 속도가 빠른 알고리즘을 사용할 것인지 아니면 정확도가 높은 알고리즘을 사용할 것인지 결정합니다.|  
|**빠름**|빠르지만 정확도가 떨어지는 비교 알고리즘을 사용합니다.|  
|**정확**|정확한 비교 알고리즘을 사용합니다.|  
  
 **DiffOptions**  
 비교 작업에 적용할 비교 옵션을 설정합니다. 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|XML 선언을 비교할지 여부를 지정합니다.|  
|**IgnoreDTD**|DTD(문서 유형 정의)를 무시할지 여부를 지정합니다.|  
|**IgnoreWhiteSpaces**|문서 비교 시 공백 양의 차이를 무시할 것인지 여부를 지정합니다.|  
|**IgnoreNamespaces**|요소의 네임스페이스 URI(Uniform Resource Identifier)와 해당 요소의 특성 이름을 비교할지 여부를 지정합니다.<br /><br /> 참고: 이 옵션을 **True**로 설정하는 경우 로컬 이름은 같지만 네임스페이스가 다른 두 요소를 동일한 것으로 간주합니다.|  
|**IgnoreProcessingInstructions**|처리 명령을 비교할지 여부를 지정합니다.|  
|**IgnoreOrderOfChildElements**|자식 요소의 순서를 비교할지 여부를 지정합니다.<br /><br /> 참고: 이 옵션을 **True**로 설정하는 경우 형제 목록에서의 위치만 다른 여러 자식 요소를 동일한 것으로 간주합니다.|  
|**IgnoreComments**|주석 노드를 비교할지 여부를 지정합니다.|  
|**IgnorePrefixes**|요소와 특성 이름의 접두사를 비교할지 여부를 지정합니다.<br /><br /> 참고: 이 옵션을 **True**로 설정하는 경우 로컬 이름은 같지만 네임스페이스 URI 및 접두사가 다른 두 요소를 동일한 것으로 간주합니다.|  
  
 **FailOnDifference**  
 비교 작업이 실패할 경우 태스크가 실패할지 여부를 지정합니다.  
  
 **SaveDiffGram**  
 비교 결과인 DiffGram 문서를 저장할지 여부를 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 비교 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 경우 **DestinationType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **DestinationType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 **SecondOperandType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **SecondOperandType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **SecondOperandType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--patch"></a>OperationType = Patch  
 패치 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 패치 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 경우 **DestinationType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **DestinationType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 **SecondOperandType** 을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 경우 **SecondOperandType** 로 설정 된 **파일 연결**, 파일 연결 관리자를 선택 하거나 클릭 \< **새 연결...** > 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 경우 **SecondOperandType** 로 설정 된 **변수**기존 변수를 선택 하거나 클릭 \< **새 변수...** > 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>관련 내용  
  
-   agilebi.com의 블로그 항목 - [XML 대상 스크립트 구성 요소](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/)  
  
-   www.codeplex.com의 CodePlex 예제 - [프로세스 XML 데이터 패키지 예제](http://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)  
  
  

