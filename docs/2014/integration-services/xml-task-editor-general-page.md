---
title: XML 태스크 편집기 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa0f92cc3275810b73d1dbe661a1f8473c7234df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054275"
---
# <a name="xml-task-editor-general-page"></a>XML 태스크 편집기(일반 페이지)
  
  **XML 태스크 편집기** 대화 상자의 **일반** 노드를 사용하여 작업 유형을 지정하고 작업을 구성할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [XML Task](control-flow/xml-task.md)를 참조하십시오. XML 문서 및 데이터 작업 방법은 MSDN Library의 "[.NET Framework에 XML 적용(Employing XML in the .NET Framework)](https://go.microsoft.com/fwlink/?LinkId=56214)"을 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **OperationType**  
 목록에서 작업 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**유효성 검사**|DTD(문서 유형 정의) 또는 XSD(XML 스키마 정의) 스키마와 비교하여 XML 문서의 유효성을 검사합니다. 이 옵션을 선택하면 아래의 **Validate**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**XSLT**|XML 문서에 대해 XSL 변환을 수행합니다. 이 옵션을 선택하면 아래의 **XSLT**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**XPATH**|XPath 쿼리 및 계산을 수행합니다. 이 옵션을 선택하면 아래의 **XPATH**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**병합**|두 개의 XML 문서를 병합합니다. 이 옵션을 선택하면 아래의 **Merge**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Diff**|두 개의 XML 문서를 비교합니다. 이 옵션을 선택하면 아래의 **Diff**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**패치**|비교 작업의 출력을 적용하여 새 문서를 만듭니다. 이 옵션을 선택하면 아래의 **Patch**섹션에 설명된 동적 옵션이 표시됩니다.|  
  
 **SourceType**  
 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **원본**  
 
  **Source**를 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(…)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **Source**를 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **Source**를 **변수**로 설정한 경우 기존 변수를 선택하거나 **\<새 변수...>** 를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
## <a name="operationtype-dynamic-options"></a>OperationType 동적 옵션  
  
### <a name="operationtype--validate"></a>OperationType = Validate  
 유효성 검사 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 유효성 검사 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 기존 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **ValidationType**  
 유효성 검사 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**DTD**|DTD(문서 유형 정의)를 사용합니다.|  
|**XSD**|XSD(XML 스키마 정의) 스키마를 사용합니다. 이 옵션을 선택하면 아래의 **ValidationType**섹션에 설명된 동적 옵션이 표시됩니다.|  
  
 **FailOnValidationFail**  
 문서의 유효성 검사에 실패하는 경우 작업이 실패할지 여부를 지정합니다.  
  
 **ValidationDetails**  
 이 속성의 값이 true일 때 풍부한 오류 출력을 제공합니다. 자세한 내용은 [Validate XML with the XML Task](control-flow/validate-xml-with-the-xml-task.md)를 참조하십시오.  
  
### <a name="validationtype-dynamic-options"></a>ValidationType 동적 옵션  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 두 번째 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 
  **SecondOperandType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **SecondOperandType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **XPathStringSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 XSLT 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 XSLT 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 
  **DestinationType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **DestinationType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 두 번째 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 
  **SecondOperandType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **SecondOperandType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **XPathStringSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 XPath 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 XPath 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 
  **DestinationType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **DestinationType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 두 번째 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 
  **SecondOperandType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **SecondOperandType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **XPathStringSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **PutResultInOneNode**  
 결과를 단일 노드에 쓸지 여부를 지정합니다.  
  
 **XPathOperation**  
 XPath 결과 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Evaluation**|XPath 함수의 결과를 반환합니다.|  
|**노드 목록**|선택한 노드를 XML 조각으로 반환합니다.|  
|**값**|선택한 모든 노드의 내부 텍스트 값을 연결 문자열로 반환합니다.|  
  
### <a name="operationtype--merge"></a>OperationType = Merge  
 병합 작업에 대한 옵션을 지정합니다.  
  
 **XPathStringSourceType**  
 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **XPathStringSource**  
 
  **XPathStringSourceType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **XPathStringSourceType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **XPathStringSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 XPath 문을 사용하여 원본 문서의 병합 위치를 식별하는 경우 이 문은 단일 노드를 반환해야 합니다. 여러 노드가 반환되는 경우에는 첫 번째 노드만 사용됩니다. 두 번째 문서의 내용은 XPath 쿼리에서 반환하는 첫 번째 노드 아래에 병합됩니다.  
  
 **SaveOperationResult**  
 XML 태스크가 병합 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 
  **DestinationType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **DestinationType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 두 번째 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 
  **SecondOperandType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **SecondOperandType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **SecondOperandType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--diff"></a>OperationType = Diff  
 비교 작업에 대한 옵션을 지정합니다.  
  
 **DiffAlgorithm**  
 문서를 비교할 때 사용할 비교 알고리즘을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Auto**|XML 태스크에서 처리 속도가 빠른 알고리즘을 사용할 것인지 아니면 정확도가 높은 알고리즘을 사용할 것인지 결정합니다.|  
|**빠름**|빠르지만 정확도가 떨어지는 비교 알고리즘을 사용합니다.|  
|**정확**|정확한 비교 알고리즘을 사용합니다.|  
  
 **Diff 옵션**  
 비교 작업에 적용할 비교 옵션을 설정합니다. 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|XML 선언을 비교할지 여부를 지정합니다.|  
|**IgnoreDTD**|DTD(문서 유형 정의)를 무시할지 여부를 지정합니다.|  
|**IgnoreWhite**|문서 비교 시 공백 양의 차이를 무시할 것인지 여부를 지정합니다.|  
|**IgnoreNamespaces**|요소의 네임스페이스 URI(Uniform Resource Identifier)와 해당 요소의 특성 이름을 비교할지 여부를 지정합니다.<br /><br /> 참고: 이 옵션을 `True`로 설정하는 경우 로컬 이름은 같지만 네임스페이스가 다른 두 요소를 동일한 것으로 간주합니다.|  
|**IgnoreProcessingInstructions**|처리 명령을 비교할지 여부를 지정합니다.|  
|**Ignoreorderofchildelements의 ignoreorder**|자식 요소의 순서를 비교할지 여부를 지정합니다.<br /><br /> 참고: 이 옵션을 `True`로 설정하는 경우 형제 목록에서의 위치만 다른 여러 자식 요소를 동일한 것으로 간주합니다.|  
|**IgnoreComments**|주석 노드를 비교할지 여부를 지정합니다.|  
|**IgnorePrefixes**|요소와 특성 이름의 접두사를 비교할지 여부를 지정합니다.<br /><br /> 참고: 이 옵션을 `True`로 설정하는 경우 로컬 이름은 같지만 네임스페이스 URI 및 접두사가 다른 두 요소를 동일한 것으로 간주합니다.|  
  
 **FailOnDifference**  
 비교 작업이 실패할 경우 태스크가 실패할지 여부를 지정합니다.  
  
 **SaveDiffGram**  
 비교 결과인 DiffGram 문서를 저장할지 여부를 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 비교 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 
  **DestinationType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **DestinationType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 
  **SecondOperandType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **SecondOperandType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **SecondOperandType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--patch"></a>OperationType = Patch  
 패치 작업에 대한 옵션을 지정합니다.  
  
 **SaveOperationResult**  
 XML 태스크가 패치 작업의 출력을 저장할지 여부를 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수를 덮어쓸지 여부를 지정합니다.  
  
 **대상**  
 
  **DestinationType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **DestinationType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **DestinationType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperandType**  
 XML 문서의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **SecondOperand**  
 
  **SecondOperandType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표 단추 **(...)** 를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 
  **SecondOperandType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 
  **SecondOperandType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목**: [Integration Services &#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [식 페이지](expressions/expressions-page.md)  
  
  
