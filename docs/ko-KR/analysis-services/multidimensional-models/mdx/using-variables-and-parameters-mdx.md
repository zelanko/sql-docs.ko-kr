---
title: 변수 및 매개 변수 (MDX)를 사용 하 여 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 039668b719a2c6c715139682496117b8239425aa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-variables-and-parameters-mdx"></a>변수 및 매개 변수 사용(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 MDX(Multidimensional Expressions) 문을 매개 변수화할 수 있습니다. 매개 변수가 있는 문을 사용하면 런타임에 사용자 정의가 가능한 범용 문을 만들 수 있습니다.  
  
 매개 변수가 있는 문을 만들 때 매개 변수 이름은 이름 앞에 @ 부호를 붙여 식별합니다. 예를 들어 @Year 유효한 매개 변수 이름 이어야 합니다  
  
 MDX는 리터럴 또는 스칼라 값을 위한 매개 변수만 지원합니다. 멤버, 집합 또는 튜플을 참조하는 매개 변수를 만들려면 [StrToMember](../../../mdx/strtomember-mdx.md) 또는 [StrToSet](../../../mdx/strtoset-mdx.md)와 같은 함수를 사용해야 합니다.  
  
 Analysis (XMLA) 예를 들어 다음 XML에는 @CountryName 매개 변수는 고객에 대 한 데이터가 검색 되는 국가 포함 됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 스크립팅 기본 사항 & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
