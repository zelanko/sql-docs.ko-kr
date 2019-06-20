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
manager: kfile
ms.openlocfilehash: 84eda6f42b674ebde8793605816f98e82af350d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065046"
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
  
## <a name="remarks"></a>Remarks  
 Analysis Services 계층 구조를 알 수 없는 경우 팩트 테이블 데이터를 계층과 연결을 알 수 없는 멤버를 만듭니다. 알 수 없는 멤버는 다음 수준 중 하나에 있을 수 있습니다.  
  
-   집계되지 않는 특성 계층의 최상위 수준  
  
-   아래의 첫 번째 수준 합니다 **모든** 자연 계층에 대 한 수준입니다.  
  
-   비자연 계층에 대한 임의의 수준  
  
 멤버 식이 지정 하는 경우는 **UnknownMember** 함수에 지정된 된 멤버의 알 수 없는 멤버 자식을 반환 합니다. 지정한 멤버가 존재하지 않는 경우 함수는 Null을 반환합니다.  
  
 계층 식이 지정 하는 경우는 **UnknownMember** 함수 있을 경우 최상위 수준에서 알 수 없는 멤버를 반환 합니다.  
  
 알 수 없는 멤버 수준 또는 멤버에 없는 경우는 **UnknownMember** 함수는 null 멤버를 만듭니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
