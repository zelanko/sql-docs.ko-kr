---
title: "변수 및 매개 변수 사용(MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "매개 변수 [MDX]"
  - "쿼리 [MDX], 변수"
  - "쿼리 [MDX], 매개 변수"
  - "변수 [MDX]"
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# 변수 및 매개 변수 사용(MDX)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 MDX(Multidimensional Expressions) 문을 매개 변수화할 수 있습니다. 매개 변수가 있는 문을 사용하면 런타임에 사용자 정의가 가능한 범용 문을 만들 수 있습니다.  
  
 매개 변수가 있는 문을 만들 때 매개 변수 이름은 이름 앞에 @ 부호를 붙여 식별합니다. 예를 들어 @Year는 유효한 매개 변수 이름입니다.  
  
 MDX는 리터럴 또는 스칼라 값을 위한 매개 변수만 지원합니다. 멤버, 집합 또는 튜플을 참조하는 매개 변수를 만들려면 [StrToMember](../../../mdx/strtomember-mdx.md) 또는 [StrToSet](../../../mdx/strtoset-mdx.md)와 같은 함수를 사용해야 합니다.  
  
 예를 들어 다음 XMLA(XML for Analysis) 예에서 @CountryName 매개 변수는 고객 데이터 검색 대상 국가를 포함하게 됩니다.  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 OLE DB와 함께 이 기능을 사용하려면 **ICommandWithParameters** 인터페이스를 사용하십시오. ADOMD.Net과 함께 이 기능을 사용하려면 **AdomdCommand.Parameters** 컬렉션을 사용하십시오.  
  
## 관련 항목:  
 [MDX 스크립팅 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  