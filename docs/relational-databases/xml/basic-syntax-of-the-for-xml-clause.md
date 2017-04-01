---
title: "FOR XML 절의 기본 구문 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "BINARY BASE64 지시어"
  - "ROOT 지시어"
  - "FOR XML 절, BINARY BASE64 지시어"
  - "FOR XML 절, 구문"
  - "FOR XML 절, ROOT 지시어"
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# FOR XML 절의 기본 구문
  FOR XML 모드는 RAW, AUTO, EXPLICIT 또는 PATH일 수 있습니다. 이 모드는 결과 XML의 셰이프를 결정합니다.  
  
> [!IMPORTANT]  
>  XMLDATA 지시어에 FOR XML 옵션은 더 이상 사용되지 않습니다. RAW 및 AUTO 모드의 경우 XSD 생성을 사용하세요. EXPLICT 모드의 XMLDATA 지시어의 경우에는 대체할 옵션이 없습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 다음은 [FOR 절(Transact-SQL)](../Topic/FOR%20Clause%20\(Transact-SQL\).md)에 설명된 기본 구문입니다.  
  
```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]   
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  
  
## 인수  
 RAW[('*ElementName*')]  
 쿼리 결과를 사용하여 결과 집합의 각 행을 요소 태그로 \<row /> 일반 식별자를 갖는 XML 요소로 변환합니다. 이 지시어를 사용하는 경우 필요에 따라 행 요소에 대한 이름을 지정할 수 있습니다. 결과 XML은 각 행에 대해 행 요소가 생성될 때 지정된 *ElementName* 을 사용합니다. 자세한 내용은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.  
  
 AUTO  
 단순하게 중첩된 XML 트리로 쿼리 결과를 반환합니다. 최소한 한 개의 열이 SELECT 절에 나열되는 FROM 절의 각 테이블은 XML 요소로 표시됩니다. SELECT 절에 나열되는 열은 해당 요소의 특성에 매핑됩니다. 자세한 내용은 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)을 참조하세요.  
  
 EXPLICIT  
 결과 XML 트리 셰이프가 명시적으로 정의되도록 지정합니다. 쿼리는 이 모드를 사용하여 원하는 중첩에 대한 추가 정보가 명시적으로 지정되도록 특정 방식으로 작성되어야 합니다. 자세한 내용은 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)을 참조하세요.  
  
 PATH  
 요소와 특성을 혼합하고 추가 중첩을 사용하여 복잡한 속성을 나타내는 보다 간단한 방법을 제공합니다. FOR XML EXPLICIT 모드 쿼리를 사용하여 행 집합에서 이러한 종류의 XML을 구성할 수 있지만 PATH 모드는 복잡할 수도 있는 EXPLICIT 모드 쿼리 대신 훨씬 간단한 방법을 제공합니다. **XML** 유형 인스턴스를 반환하는 중첩 FOR XML 쿼리 및 TYPE 지시어 작성 기능과 함께 PATH 모드를 사용하면 보다 간편하게 쿼리를 작성할 수 있습니다. 이 모드는 대부분의 EXPLICIT 모드 쿼리 작성을 대신할 방법을 제공합니다. 기본적으로 PATH 모드는 결과 집합의 각 행에 대한 \<row> 요소 래퍼를 생성합니다. 필요에 따라 요소 이름을 지정할 수 있습니다. 요소 이름을 지정한 경우 지정된 이름이 래퍼 요소 이름으로 사용됩니다. 빈 문자열(FOR XML PATH (''))을 제공하면 래퍼 요소가 생성되지 않습니다. 자세한 내용은 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)을 참조하세요.  
  
 XMLDATA  
 인라인 XDR(XML-Data Reduced) 스키마가 반환되어야 함을 지정합니다. 스키마는 인라인 스키마로 문서 앞에 놓이게 됩니다. 작업 샘플은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.  
  
 XMLSCHEMA  
 인라인 W3C XML 스키마(XSD)를 반환합니다. 이 지시어를 지정할 때 필요에 따라 대상 네임스페이스 URI를 지정할 수 있습니다. 이렇게 하면 스키마에 지정된 네임스페이스를 반환합니다. 자세한 내용은 [인라인 XSD 스키마 생성](../../relational-databases/xml/generate-an-inline-xsd-schema.md)을 참조하세요. 작업 샘플은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.  
  
 ELEMENTS  
 ELEMENTS 옵션이 지정되면 열이 하위 요소로 반환됩니다. 그렇지 않은 경우에는 XML 특성에 매핑됩니다. 이 옵션은 RAW, AUTO 및 PATH 모드에서만 지원됩니다. 이 지시어를 사용하는 경우 필요에 따라 XSINIL 또는 ABSENT를 지정할 수 있습니다. XSINIL은 True로 설정된 **xsi:nil** 특성이 있는 요소가 NULL 열 값에 대해 생성되도록 지정합니다. 기본적으로 또는 ABSENT가 ELEMENTS와 함께 지정된 경우 요소가 NULL 값에 대해 생성되지 않습니다. 작업 샘플은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md) 및 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)을 참조하세요.  
  
 BINARY BASE64  
 BINARY Base64 옵션이 지정되면 쿼리에서 반환되는 이진 데이터가 모두 base64 인코딩 형식으로 표시됩니다. RAW와 EXPLICIT 모드를 사용하여 이진 데이터를 검색하려면 이 옵션을 지정해야 합니다. AUTO 모드에서 이진 데이터는 기본적으로 참조로 반환됩니다. 작업 샘플은 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)을 참조하세요.  
  
 TYPE  
 쿼리가 결과를 **xml** 형식으로 반환하도록 지정합니다. 자세한 내용은 [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md)를 참조하세요.  
  
 ROOT [('*RootName*')]  
 단일 최상위 요소가 결과 XML에 추가되도록 지정합니다. 필요에 따라 생성할 루트 요소 이름을 지정할 수 있습니다. 기본값은 "root"입니다.  
  
## 참고 항목  
 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)   
 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [FOR XML에서 EXPLICIT 모드 사용](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML&#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  