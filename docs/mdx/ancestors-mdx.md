---
title: Ancestors (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANCESTORS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ancestors function
ms.assetid: abdf2e9c-72c8-4f2e-a823-d42efc4cc7d5
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2d6304b9a87bcdb87a98a8351d4e60074ebb4d8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ancestors-mdx"></a>Ancestors(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 수준이나 지정된 멤버로부터 지정된 거리만큼 떨어진 수준에서 지정된 멤버의 모든 상위 항목 집합을 반환하는 함수입니다. 와 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 반환 되는 집합은 항상 단일 멤버로 구성 되며 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 단일 멤버에 대 한 여러 부모를 지원 하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Level syntax  
Ancestors(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestors(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Level_Expression*  
 수준을 반환하는 유효한 MDX 식입니다.  
  
 *거리*  
 지정된 멤버와의 거리를 지정하는 유효한 숫자 식입니다.  
  
## <a name="remarks"></a>주의  
 와 **상위** 함수를 제공 하는 함수 MDX 멤버 식을 사용 하 여 고 해당 멤버의 상위 항목인 수준의 MDX 식 또는 해당 멤버 위의 수준 수를 나타내는 숫자 식을 제공 합니다. 이 정보는 **상위** 함수는 해당 수준의 멤버 (한 멤버의 구성 된 집합을 됩니다)의 집합을 반환 합니다.  
  
> [!NOTE]  
>  상위 집합을 사용 하는 것이 아니라 상위 멤버를 사용 하 여 반환 하는 [상위](../mdx/ancestor-mdx.md) 함수입니다.  
  
 수준 식이 지정 되는 **상위** 함수는 지정 된 수준에서 지정된 된 멤버의 모든 상위 항목 집합을 반환 합니다. 지정된 멤버가 지정된 수준과 동일한 계층 내에 없으면 이 함수는 오류를 반환합니다.  
  
 거리를 지정 하는 경우는 **상위** 함수는 멤버 식으로 지정 된 계층에 지정 된 단계 수 만큼 위에 있는 모든 멤버 집합을 반환 합니다. 멤버는 특성 계층, 사용자 정의 계층 또는 경우에 따라 부모-자식 계층의 멤버로 지정될 수 있습니다. 숫자 1은 부모 수준의 멤버 집합을 반환하고 숫자 2는 최상위 수준의 멤버 집합(있는 경우)을 반환합니다. 숫자 0은 멤버만 포함된 집합을 반환합니다.  
  
> [!NOTE]  
>  이 형식을 사용 하 여는 **상위** 함수 경우은 부모의 수준을 알 수 없는 또는 명명할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 **상위** 멤버, 부모 및 최상위 항목에 대 한 Internet Sales Amount 측정값을 반환 하는 함수입니다. 이 예에서는 수준 식을 사용하여 반환할 수준을 지정합니다. 수준은 멤버 식에 지정된 멤버와 동일한 계층에 있습니다.  
  
```  
SELECT {  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Category]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Subcategory]),  
    Ancestors([Product].[Product Categories].[Product].[Mountain-100 Silver, 38],[Product].[Product Categories].[Product])  
    } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
 다음 예제에서는 **상위** 멤버, 부모 및 최상위 항목에 대 한 Internet Sales Amount 측정값을 반환 하는 함수입니다. 이 예에서는 숫자 식을 사용하여 반환할 수준을 지정합니다. 수준은 멤버 식에 지정된 멤버와 동일한 계층에 있습니다.  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],2  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],1  
      ),  
   Ancestors(  
      [Product].[Product Categories].[Product].[Mountain-100 Silver, 38],0  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM  [Adventure Works]  
```  
  
 다음 예제에서는 **상위** 특성 계층의 멤버의 부모에 대 한 Internet Sales Amount 측정값을 반환 하는 함수입니다. 이 예에서는 숫자 식을 사용하여 반환할 수준을 지정합니다. 멤버 식의 멤버는 특성 계층의 멤버이므로 해당 부모는 [All] 수준입니다.  
  
```  
SELECT {  
   Ancestors(  
      [Product].[Product].[Mountain-100 Silver, 38],1  
      )  
   } ON 0,  
[Measures].[Internet Sales Amount] ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

