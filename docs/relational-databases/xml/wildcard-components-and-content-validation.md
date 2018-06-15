---
title: 와일드카드 구성 요소 및 콘텐츠 유효성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d5828b51d24d9e6112d2c4adc21070984f33ae9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014000"
---
# <a name="wildcard-components-and-content-validation"></a>와일드카드 구성 요소 및 콘텐츠 유효성 검사
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  와일드카드 구성 요소는 콘텐츠 모델에 나타나는 형식의 유연성을 향상시키는 데 사용됩니다. 이러한 구성 요소는 XSD 언어에서 다음과 같은 방식으로 지원됩니다.  
  
-   요소 와일드카드 구성 요소: 이러한 구성 요소는 **\<xsd:any>** 요소로 표시됩니다.  
  
-   특성 와일드카드 구성 요소: 이러한 구성 요소는 **\<xsd:anyAttribute>** 요소로 표시됩니다.  
  
 **\<xsd:any>** 및 **\<xsd:anyAttribute>** 와일드카드 문자 요소는 모두 **processContents** 특성의 사용을 지원합니다. 이렇게 하면 XML 응용 프로그램에서 이러한 와일드카드 문자 요소와 관련된 문서 내용에 대한 유효성 검사를 처리하는 방법을 나타내는 값을 지정할 수 있습니다. 다음은 다양한 값과 해당 기능에 대한 설명입니다.  
  
-   **strict** 값은 콘텐츠의 유효성을 완전히 검사하도록 지정합니다.  
  
-   **skip** 값은 콘텐츠의 유효성을 검사하지 않도록 지정합니다.  
  
-   **lax** 값은 스키마 정의가 사용 가능한 요소와 특성에 대해서만 유효성을 검사하도록 지정합니다.  
  
## <a name="lax-validation-and-xsanytype-elements"></a>lax 유효성 검사 및 xs:anyType 요소  
 XML 스키마 사양에서는 **anyType** 유형의 요소에 대해 **lax** 유효성 검사를 실행합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서는 lax 유효성 검사를 지원하지 않았으므로 **anyType**요소에 엄격한 유효성 검사가 적용되었습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 lax 유효성 검사가 지원되므로 이를 통해 **anyType** 유형 요소의 콘텐츠에 대한 유효성이 검사됩니다.  
  
 다음 예에서는 lax 유효성 검사를 보여 줍니다. 스키마 요소 `e` 는 **anyType** 유형 중 하나입니다. 이 예에서는 형식화된 **xml** 변수를 만들고 **anyType** 유형 요소의 lax 유효성 검사에 대해 보여 줍니다.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 `<e>` 의 유효성 검사가 성공하므로 다음 예도 성공합니다.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 다음 예도 성공합니다. 스키마에서 `<c>` 요소가 정의되지 않더라도 인스턴스는 수락됩니다.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 다음 예에서 `<a>` 요소의 정의는 문자열 값을 사용할 수 없기 때문에 XML 인스턴스가 거부됩니다.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
