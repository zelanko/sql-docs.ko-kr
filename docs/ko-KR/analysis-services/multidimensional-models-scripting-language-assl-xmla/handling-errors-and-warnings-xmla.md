---
title: 오류 및 경고 처리 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de925e6bb83f7219ec1bd453f47d63a3fb3624a1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors-and-warnings-xmla"></a>오류 및 경고 처리(XMLA)
  오류 처리는 필요한 경우 XML for Analysis (XMLA) [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드 호출이 실행 되지 않습니다, 성공적으로 실행 하지만 오류 또는 경고를 생성 또는 성공적으로 실행 되지만 결과 반환 오류가 있습니다.  
  
|오류|보고|  
|-----------|---------------|  
|XMLA 메서드 호출이 실행되지 않음|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 오류의 세부 정보가 포함 된 SOAP 오류 메시지를 반환 합니다.<br /><br /> 자세한 내용은 섹션을 참조 하십시오. [SOAP 오류 해결](#handling_soap_faults)합니다.|  
|메서드 호출이 성공적으로 실행되었으나 오류 또는 경고 발생|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 포함는 [오류](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) 또는 [경고](../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md) 각 오류 또는 경고에 대 한 요소에서 각각의 [메시지](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md) 의 속성은 [루트](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 요소 메서드 호출 결과가 들어 있는입니다.<br /><br /> 자세한 내용은 섹션을 참조 하십시오. [오류 및 경고 처리](#handling_errors_and_warnings)합니다.|  
|메서드 호출이 성공적으로 실행되었으나 결과에 오류가 있음|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인라인 **오류** 또는 **경고** 요소 오류 또는 경고에 대 한 적절 한 내에서 각각 [셀](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) 또는 [행](../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md) 메서드 호출의 결과의 요소입니다.<br /><br /> 자세한 내용은 섹션을 참조 하십시오. [인라인 오류 및 경고](#handling_inline_errors_and_warnings)합니다.|  
  
##  <a name="handling_soap_faults"></a> SOAP 오류 해결  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 SOAP 오류가 반환되는 경우는 다음과 같습니다.  
  
-   XMLA 메서드가 포함된 SOAP 메시지가 올바른 형식이 아니거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 해당 메시지의 유효성을 확인할 수 없는 경우  
  
-   XMLA 메서드가 포함된 SOAP 메시지와 관련된 통신 또는 기타 오류가 발생한 경우  
  
-   XMLA 메서드가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 실행되지 않은 경우  
  
 XMLstartA에 대한 SOAP 오류 코드는 "XMLForAnalysis"로 시작하며 그 뒤에 마침표와 16진수 HRESULT 결과 코드가 붙습니다. 예를 들어 오류 코드 "`0x80000005`"는 "`XMLForAnalysis.0x80000005`"가 됩니다. SOAP 오류 형식에 대한 자세한 내용은 W3C SOAP(Simple Object Access Protocol) 1.1에서 Soap Fault를 참조하십시오.  
  
### <a name="fault-code-information"></a>오류 코드 정보  
 다음 표에서는 SOAP 응답의 세부 정보 섹션에 포함된 XMLA 오류 코드 정보를 보여 줍니다. 열은 SOAP 오류의 세부 정보 섹션에 포함된 오류의 특성을 나타냅니다.  
  
|열 이름|유형|Description|Null 허용<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|**ErrorCode**|**UnsignedInt**|메서드의 성공 또는 실패를 나타내는 코드를 반환합니다. 16 진수 값으로 변환 해야는 **UnsignedInt** 값입니다.|아니요|  
|**WarningCode**|**UnsignedInt**|경고 조건을 나타내는 코드를 반환합니다. 16 진수 값으로 변환 해야는 **UnsignedInt** 값입니다.|예|  
|**설명**|**문자열**|오류가 발생한 구성 요소에서 반환한 오류 또는 경고에 대한 텍스트와 설명입니다.|예|  
|**원본**|**문자열**|오류 또는 경고가 발생한 구성 요소의 이름입니다.|예|  
|**HelpFile**|**문자열**|오류 또는 경고를 설명하는 도움말 파일 또는 항목의 경로 또는 URL입니다.|예|  
  
 <sup>1</sup> 고 여부를 나타내는 데이터 필수 항목이 며 반환 되어야 합니다 또는 여부는 데이터는 없어도 열 적용 되지 않는 경우 null 문자열은 사용할 수 있습니다.  
  
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
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 반환 된 **메시지** 속성에는 **루트** 명령 실행 후 다음과 같은 경우 발생 하는 경우 명령에 대 한 요소:  
  
-   메서드 자체는 실패하지 않았지만 메서드가 성공적으로 호출된 후 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 오류가 발생한 경우  
  
-   명령을 성공적으로 실행했지만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 경고를 반환한 경우  
  
 **메시지** 속성 뒤에 포함 된 다른 모든 속성의 **루트** 요소를 하나 이상 포함 될 수 있습니다 및 **메시지** 요소. 각 **메시지** 요소는 단일을 포함할 수 있습니다 **오류** 또는 **경고** 동안 발생 한 오류 또는 경고를 각각 설명 하는 요소는 지정 된 명령입니다.  
  
 오류 및에 포함 된 경고에 대 한 자세한 내용은 **메시지** 속성 참조 [메시지 요소 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)합니다.  
  
### <a name="handling-errors-during-serialization"></a>직렬화 중 오류 해결  
 한 후 오류가 발생 하는 경우는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 이미 성공적으로 실행된 된 명령의 출력을 직렬화 하는 작업 시작 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 반환는 [예외](../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md) 오류 지점에서 다른 네임 스페이스의 요소입니다. 그러면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 클라이언트에 보낸 XML 문서가 유효한 문서가 되도록 열려 있는 요소를 모두 닫습니다. 인스턴스도 반환 합니다.는 **메시지** 의 오류 설명을 포함 하는 요소입니다.  
  
##  <a name="handling_inline_errors_and_warnings"></a> 인라인 오류 및 경고 처리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인라인 반환 **오류** 또는 **경고** XMLA 메서드 자체는 실패 하지 않았지만 하지만에서 메서드에 의해 반환 된 결과의 데이터 요소에 특정 오류가 발생 하는 경우 명령에 대 한는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XMLA 메서드 호출에 성공 후 인스턴스입니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인라인 제공 **오류** 및 **경고** 는 문제 관련 하 여 셀 또는 다른 데이터 요소 내에 포함 된 한 **루트** 사용 하 여 요소는 [ MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 보안 오류 또는 셀 형식 지정 오류와 같은 데이터 형식 발생 합니다. 이러한 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 반환는 **오류** 또는 **경고** 요소에는 **셀** 또는 **행** 오류를 포함 하는 요소 또는 경고, 각각.  
  
 다음 예제에서는 결과 집합에서 반환 된 행 집합의 오류를 포함 하는 **Execute** 메서드를 사용 하 여는 [문을](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) 명령입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
