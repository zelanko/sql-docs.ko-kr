---
title: 주석 (MDX 구문) | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- remarks [MDX]
- MDX [Analysis Services], comments
- commenting characters
- nonexecuting text strings [MDX]
- Multidimensional Expressions [Analysis Services], comments
- comments [MDX]
ms.assetid: 9c00b30c-28f6-4f23-b812-ccc0e900daa5
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4d3a333b2a8fdbb89f718d67a849c08142da8f79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="comments-mdx-syntax"></a>주석(MDX 구문)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  주석은 프로그램 코드 내의 실행되지 않는 텍스트 문자열이며 설명이라고도 합니다. 코드에 대한 설명을 기록하거나 진단 중인 MDX 문 및 스크립트의 일부를 일시적으로 비활성화하는 데 주석을 사용할 수 있습니다. 주석을 사용하여 코드에 대한 설명을 기록하면 나중에 프로그램 코드를 유지 보수할 때 용이합니다. 주석은 주로 프로그램 이름, 저자 이름, 주요 코드 변경 날짜 등을 기록하는 데 사용됩니다. 또한 주석을 사용하여 복잡한 계산이나 프로그래밍 방식을 설명할 수도 있습니다.  
  
 MDX의 주석은 다음 지침을 따릅니다.  
  
-   주석에는 모든 영숫자 문자나 기호를 사용할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 주석 내의 모든 문자를 무시합니다.  
  
-   문 또는 스크립트 내에서 주석의 길이는 제한이 없습니다. 주석은 한 개 이상의 줄을 포함할 수 있습니다.  
  
 MDX는 세 가지 유형의 주석 문자를 지원합니다.  
  
 //(이중 슬래시)  
 이 주석 문자는 실행 코드와 같은 행 또는 별도의 행에 사용할 수 있습니다. 이중 슬래시에서 시작하여 행 끝까지 주석으로 처리되며 주석이 여러 행일 경우 각 주석 행의 시작 부분에 이중 슬래시를 입력해야 합니다. 자세한 내용은 참조 [ &#40;주석&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)합니다.  
  
 -- (이중 하이픈)  
 이 주석 문자는 실행 코드와 같은 행 또는 별도의 행에 사용할 수 있습니다. 이중 하이픈에서 시작하여 행 끝까지 주석으로 처리되며 주석이 여러 행일 경우 각 주석 행의 시작 부분에 이중 하이픈을 입력해야 합니다. 자세한 내용은 참조 [- &#40;주석&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)합니다.  
  
 /* ... \*/ (슬래시-별표 문자 쌍)  
 실행 코드와 같은 행이나 별도의 행은 물론 실행 코드 내에서도 사용할 수 있는 주석 문자입니다. 주석 문자에 이르기까지 (/\*)부터 닫는 주석 문자 (\*/) 설명의 일부로 간주 됩니다. 여러 줄 주석이 일 경우 오픈 주석 문자 (/\*) 메모를 하 고 닫는 주석 문자 쌍 시작 해야 합니다 (\*/) 주석으로 처리를 종료 해야 합니다. 주석 행 내에서는 다른 주석 문자를 포함할 수 없습니다. 자세한 내용은 참조 [/ *... \*/ (Comment)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>예제  
 다음 쿼리에서는 세 가지 유형의 주석 예를 모두 보여 줍니다.  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 구문 요소 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
