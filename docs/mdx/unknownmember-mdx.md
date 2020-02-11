---
title: UnknownMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a0332b200a74044dcd4e7d8d308923cc4b759738
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097279"
---
# <a name="unknownmember-mdx"></a>UnknownMember(MDX)


  수준 또는 멤버와 연결된 알 수 없는 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Hierarchy_Expression*  
 계층을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 계층 구조를 알 수 없는 경우 Analysis Services은 알 수 없는 멤버를 만들어 팩트 테이블 데이터를 계층과 연결 합니다. 알 수 없는 멤버는 다음 수준 중 하나에 있을 수 있습니다.  
  
-   집계되지 않는 특성 계층의 최상위 수준  
  
-   자연 계층에 대 한 **모든** 수준 아래의 첫 번째 수준  
  
-   비자연 계층에 대한 임의의 수준  
  
 멤버 식이 지정 된 경우 **UnknownMember** 함수는 지정 된 멤버의 알 수 없는 멤버 자식을 반환 합니다. 지정한 멤버가 존재하지 않는 경우 함수는 Null을 반환합니다.  
  
 계층 식이 지정 된 경우 **UnknownMember** 함수는 최상위 수준의 알 수 없는 멤버 (있는 경우)를 반환 합니다.  
  
 해당 수준이 나 멤버에 알 수 없는 멤버가 없으면 **UnknownMember** 함수는 null 멤버를 만듭니다.  
  
> [!NOTE]  
>  계층이나 멤버에 알 수 없는 멤버가 존재하지 않으면 오류가 생성됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Measures 차원의 모든 멤버에 대해 Product 특성 계층에 있는 All Products 멤버의 알 수 없는 멤버를 반환합니다.  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 다음 예에서는 Measures 차원의 모든 멤버에 대해 Product Categories 계층의 알 수 없는 멤버를 반환합니다.  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 함수 참조 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
