---
title: 오류 및 경고 처리 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 856886a5edfa5dcae604b44f5c2dca356ba0addb
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156390"
---
# <a name="handling-errors-and-warnings-xmla"></a>오류 및 경고 처리(XMLA)
  경우 XML for Analysis (XMLA) 오류 해결이 필요한 [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) 또는 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 메서드 호출 실행 되지 않습니다, 성공적으로 실행 되지만 오류 또는 경고를 생성 또는 성공적으로 실행 되었으나 결과 반환 합니다. 오류를 포함 하는입니다.  
  
|Error|보고|  
|-----------|---------------|  
|XMLA 메서드 호출이 실행되지 않음|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 오류의 세부 정보가 포함 된 SOAP 오류 메시지를 반환 합니다.<br /><br /> 자세한 내용은 섹션을 참조 하세요 [SOAP 오류](#handling_soap_faults)합니다.|  
|메서드 호출이 성공적으로 실행되었으나 오류 또는 경고 발생|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 포함을 [오류](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) 또는 [경고](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla) 각 오류 또는 경고에 대 한 요소 각각를 [메시지](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla) 의 속성을 [루트](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) 요소 메서드 호출 결과가 들어 있는입니다.<br /><br /> 자세한 내용은 섹션을 참조 하세요 [오류 및 경고 처리](#handling_errors_and_warnings)합니다.|  
|메서드 호출이 성공적으로 실행되었으나 결과에 오류가 있음|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인라인 `error` 또는 `warning` 요소는 오류 또는 경고에 대 한 적절 한 내에서 각각 [셀](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) 또는 [행](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla) 메서드 호출의 결과 요소입니다.<br /><br /> 자세한 내용은 섹션을 참조 하세요 [인라인 오류 및 경고](#handling_inline_errors_and_warnings)합니다.|  
  
##  <a name="handling_soap_faults"></a> SOAP 오류 해결  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SOAP 오류가 반환되는 경우는 다음과 같습니다.  
  
-   XMLA 메서드가 포함된 SOAP 메시지가 올바른 형식이 아니거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 해당 메시지의 유효성을 확인할 수 없는 경우  
  
-   XMLA 메서드가 포함된 SOAP 메시지와 관련된 통신 또는 기타 오류가 발생한 경우  
  
-   XMLA 메서드가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 실행되지 않은 경우  
  
 XMLstartA에 대한 SOAP 오류 코드는 "XMLForAnalysis"로 시작하며 그 뒤에 마침표와 16진수 HRESULT 결과 코드가 붙습니다. 예를 들어 오류 코드 "`0x80000005`"는 "`XMLForAnalysis.0x80000005`"가 됩니다. SOAP 오류 형식에 대한 자세한 내용은 W3C SOAP(Simple Object Access Protocol) 1.1에서 Soap Fault를 참조하십시오.  
  
### <a name="fault-code-information"></a>오류 코드 정보  
 다음 표에서는 SOAP 응답의 세부 정보 섹션에 포함된 XMLA 오류 코드 정보를 보여 줍니다. 열은 SOAP 오류의 세부 정보 섹션에 포함된 오류의 특성을 나타냅니다.  
  
|열 이름|형식|Description|Null 허용<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|메서드의 성공 또는 실패를 나타내는 코드를 반환합니다. 16진수 값은 `UnsignedInt` 값으로 변환되어야 합니다.|아니요|  
|`WarningCode`|`UnsignedInt`|경고 조건을 나타내는 코드를 반환합니다. 16진수 값은 `UnsignedInt` 값으로 변환되어야 합니다.|사용자 계정 컨트롤|  
|`Description`|`String`|오류가 발생한 구성 요소에서 반환한 오류 또는 경고에 대한 텍스트와 설명입니다.|사용자 계정 컨트롤|  
|`Source`|`String`|오류 또는 경고가 발생한 구성 요소의 이름입니다.|사용자 계정 컨트롤|  
|`HelpFile`|`String`|오류 또는 경고를 설명하는 도움말 파일 또는 항목의 경로 또는 URL입니다.|사용자 계정 컨트롤|  
  
 <sup>1</sup> 여부를 나타내는 반환 해야 하는 데이터를 반드시 또는 여부 데이터가 선택적 열 적용 되지 않는 경우 null 문자열이 허용 됩니다.  
  
 다음은 메서드 호출이 실패했을 때 발생하는 SOAP 오류 예입니다.  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a> 오류 및 경고 처리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 명령 실행 후 다음과 같은 상황이 발생할 경우 명령에 대한 `Messages` 요소에 `root` 속성을 반환합니다.  
  
-   메서드 자체는 실패하지 않았지만 메서드가 성공적으로 호출된 후 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 오류가 발생한 경우  
  
-   명령을 성공적으로 실행했지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 경고를 반환한 경우  
  
 `Messages` 속성은 `root` 요소에 포함된 속성 중 마지막 속성이며 `Message` 요소를 한 개 이상 포함할 수 있습니다. 또한 각 `Message` 요소는 지정된 명령에 대해 발생한 오류나 경고를 설명하는 단일 `error` 또는 `warning` 요소를 포함할 수 있습니다.  
  
 오류 및 경고에 포함 된에 대 한 자세한 내용은 합니다 `Messages` 속성을 참조 하세요 [메시지 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla).  
  
### <a name="handling-errors-during-serialization"></a>직렬화 중 오류 해결  
 후 오류가 발생 하는 경우는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 이미 성공적으로 실행 된 명령의 출력을 직렬화 하는 작업 시작 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 반환는 [예외](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla) 오류 시점에 다른 네임 스페이스에서 요소입니다. 그러면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 클라이언트에 보낸 XML 문서가 유효한 문서가 되도록 열려 있는 요소를 모두 닫습니다. 또한 오류에 대한 설명이 들어 있는 `Messages` 요소도 반환합니다.  
  
##  <a name="handling_inline_errors_and_warnings"></a> 인라인 오류 및 경고 처리  
 XMLA 메서드 자체는 실패하지 않았지만 XMLA 메서드가 성공적으로 호출된 후 반환된 결과의 데이터 요소와 관련된 오류가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 발생하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 명령에 대한 인라인 `error` 또는 `warning`을 반환합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인라인을 제공 `error` 및 `warning` 다른 데이터 또는 셀에 문제 관련 된 경우 요소 내에 포함 된를 `root` 요소를 사용 하 여를 [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla) 보안 등의 데이터 형식 발생할 오류 또는 서식 지정 셀에 대 한 오류가 발생 했습니다. 이러한 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 오류 또는 경고가 포함된 `error` 또는 `warning` 요소에 `Cell` 또는 `row` 요소를 반환합니다.  
  
 다음 예제에서 반환 된 행에 오류가 포함 된 결과 집합을는 `Execute` 메서드를 사용 하는 [문](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) 명령입니다.  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
