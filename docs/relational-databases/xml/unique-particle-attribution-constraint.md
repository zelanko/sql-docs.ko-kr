---
title: "UNIQUE PARTICLE ATTRIBUTION 제약 조건 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 712668f3b495017765205b939c390db0f0d75456
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="unique-particle-attribution-constraint"></a>UNIQUE PARTICLE ATTRIBUTION 제약 조건
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] XSD에서 복잡한 콘텐츠 모델은 UPA(Unique Particle Attribution) 제약 조건 규칙에 의해 제한됩니다. 이 규칙에서는 항목 문서의 각 요소가 해당 부모 콘텐츠 모델에 있는 정확히 하나의 `<xsd:element>` 또는 `<xsd:any>` 파티클과 분명하게 일치해야 합니다. 잠재적으로 모호한 콘텐츠 모델이 있는 유형이 포함되는 스키마는 모두 거부됩니다.  
  
 모호성에 대한 가장 일반적인 원인은 minOccurs < maxOccurs와 같은 변수 발생 범위가 있는 `<xsd:any>` 와일드카드 문자 및 파티클입니다. 예를 들어 다음 콘텐츠 모델은 <`e1`> 요소가 `<xsd:element>` 또는 `<xsd:any>` 요소 중 하나와 일치할 수 있기 때문에 모호합니다.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 다음 콘텐츠 모델도 모호합니다.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 `<root><e1/><e2/><e1/></root>` 와 같은 문서는 분명하게 유효성을 검사할 수 있지만 `<root><e1/><e1/></root>` 와 같은 문서는 두 번째 `<xsd:element>` 에 해당하는 `<e1/>` 가 명확하지 않기 때문에 분명하게 유효성을 검사할 수 없습니다. 일부 문서는 분명하게 유효성을 검사할 수 있더라도 잠재적 모호성으로 인해 스키마가 거부됩니다.  
  
 콘텐츠 모델이 유효하려면 자세한 검사 없이도 모든 항목의 유효성을 분명하게 검사할 수 있어야 합니다. 예를 들어 다음과 같은 콘텐츠 모델에 유의하십시오.  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 `<root><e1/><e3/></root>`와 같은 문서에서 `<e1/><e3/>` 시퀀스는 두 번째 `<xsd:sequence>`와 분명하게 일치합니다. 하지만 `<xsd:element>` 을 검사하지 않고서는 `<e1/>` 에 해당하는 `<e3/>`를 확인할 수 없기 때문에 이 콘텐츠 모델은 UPA 제약 조건 규칙에 위배됩니다.  
  
## <a name="finding-more-information"></a>추가 정보 찾기  
 다음 문서는 W3C(World Wide Web Consortium)에서 발행했으며 UNIQUE PARTICLE ATTRIBUTION 제약 조건에 대한 기술적인 설명이 포함되어 있습니다.  
  
 "XML 스키마 1부: 구조 제2판, W3C 제안 수정 추천":  
  
-   섹션 3.8.6: 모델 그룹 스키마 구성 요소의 제한 사항  
  
-   부록 H: Unique Particle Attribution 제약 조건 분석(비표준)  
  
 문서를 보려면 [http://www.w3.org/TR/xmlschema-1](http://go.microsoft.com/fwlink/?linkid=48881)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 스키마 컬렉션&#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
