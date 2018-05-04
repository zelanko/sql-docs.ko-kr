---
title: UnknownMember (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UnknownMember
dev_langs:
- kbMDX
helpviewer_keywords:
- UnknownMember function
ms.assetid: 5ae39cbe-65c8-4a59-9548-71b28ecf6eb5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7fe0fe0706d6b88c19f5683a71de15516dddecec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="unknownmember-mdx"></a>UnknownMember(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>주의  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 계층 구조를 알 수 없는 경우 팩트 테이블 데이터는 계층 구조와 연결 하려면 알 수 없는 멤버를 만듭니다. 알 수 없는 멤버는 다음 수준 중 하나에 있을 수 있습니다.  
  
-   집계되지 않는 특성 계층의 최상위 수준  
  
-   아래의 첫 번째 수준에서 **모든** 자연 계층에 대 한 수준.  
  
-   비자연 계층에 대한 임의의 수준  
  
 멤버 식이 지정 되는 **UnknownMember** 함수는 지정 된 멤버의 알 수 없는 멤버 자식을 반환 합니다. 지정한 멤버가 존재하지 않는 경우 함수는 Null을 반환합니다.  
  
 계층 식이 지정 되는 **UnknownMember** 있는 경우 함수는 최상위 수준의 알 수 없는 멤버를 반환 합니다.  
  
 알 수 없는 멤버 수준이 나 멤버에 존재 하지 않는 경우는 **UnknownMember** 함수는 null 멤버를 만듭니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
