---
title: 변수 및 매개 변수 (MDX)를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 22adb713c5a75d4cf038e5683a6ddec8adbe836d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266109"
---
# <a name="using-variables-and-parameters-mdx"></a>변수 및 매개 변수 사용(MDX)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서는 MDX(Multidimensional Expressions) 문을 매개 변수화할 수 있습니다. 매개 변수가 있는 문을 사용하면 런타임에 사용자 정의가 가능한 범용 문을 만들 수 있습니다.  
  
 매개 변수가 있는 문을 만들 때 매개 변수 이름은 이름 앞에 @ 부호를 붙여 식별합니다. 예를 들어 @Year 유효한 매개 변수 이름 이어야 합니다  
  
 MDX는 리터럴 또는 스칼라 값을 위한 매개 변수만 지원합니다. 멤버, 집합 또는 튜플을 참조하는 매개 변수를 만들려면 [StrToMember](/sql/mdx/strtomember-mdx) 또는 [StrToSet](/sql/mdx/strtoset-mdx)와 같은 함수를 사용해야 합니다.  
  
 Analysis (XMLA) 예를 들어 다음 xml에서은 @CountryName 매개 변수는 고객에 대 한 데이터가 검색 되는 국가 포함 됩니다.  
  
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
  
 OLE DB를 사용 하 여이 기능을 사용 하려면 사용 된 `ICommandWithParameters` 인터페이스입니다. ADOMD.Net과 함께 이 기능을 사용하려면 **AdomdCommand.Parameters** 컬렉션을 사용하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 스크립팅 기본 사항 &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
