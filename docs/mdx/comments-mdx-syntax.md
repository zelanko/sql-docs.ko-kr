---
title: 주석 (MDX 구문) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ffcb57a48c7d6e265daa786912cfd37f0b43754
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001522"
---
# <a name="comments-mdx-syntax"></a>주석(MDX 구문)


  주석은 프로그램 코드 내의 실행되지 않는 텍스트 문자열이며 설명이라고도 합니다. 코드에 대한 설명을 기록하거나 진단 중인 MDX 문 및 스크립트의 일부를 일시적으로 비활성화하는 데 주석을 사용할 수 있습니다. 주석을 사용하여 코드에 대한 설명을 기록하면 나중에 프로그램 코드를 유지 보수할 때 용이합니다. 주석은 주로 프로그램 이름, 저자 이름, 주요 코드 변경 날짜 등을 기록하는 데 사용됩니다. 또한 주석을 사용하여 복잡한 계산이나 프로그래밍 방식을 설명할 수도 있습니다.  
  
 MDX의 주석은 다음 지침을 따릅니다.  
  
-   주석에는 모든 영숫자 문자나 기호를 사용할 수 있습니다.  주석 안의 모든 문자는 무시 됩니다.  
  
-   문 또는 스크립트 내에서 주석의 길이는 제한이 없습니다. 주석은 한 개 이상의 줄을 포함할 수 있습니다.  
  
 MDX는 세 가지 유형의 주석 문자를 지원합니다.  
  
 //(이중 슬래시)  
 이 주석 문자는 실행 코드와 같은 행 또는 별도의 행에 사용할 수 있습니다. 이중 슬래시에서 시작하여 행 끝까지 주석으로 처리되며 주석이 여러 행일 경우 각 주석 행의 시작 부분에 이중 슬래시를 입력해야 합니다. 자세한 내용은 [MDX&#41;&#41; &#40;&#40;설명 ](../mdx/comment-mdx-double-slash.md)을 참조 하세요.  
  
 -- (이중 하이픈)  
 이 주석 문자는 실행 코드와 같은 행 또는 별도의 행에 사용할 수 있습니다. 이중 하이픈에서 시작하여 행 끝까지 주석으로 처리되며 주석이 여러 행일 경우 각 주석 행의 시작 부분에 이중 하이픈을 입력해야 합니다. 자세한 내용은 [&#40;주석&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)를 참조 하세요.  
  
 /* ... \*/(슬래시-별표 문자 쌍)  
 실행 코드와 같은 행이나 별도의 행은 물론 실행 코드 내에서도 사용할 수 있는 주석 문자입니다. 열린 주석 쌍 (/\*)부터 닫는 주석 문자 (\*/) 까지의 모든 항목은 주석의 일부로 간주 됩니다. 여러 줄로 된 주석의 경우 여는 주석 문자 쌍 (/\*)은 주석을 시작 해야 하 고, 닫는 주석 문자 쌍 (\*/)은 주석을 종료 해야 합니다. 주석 행 내에서는 다른 주석 문자를 포함할 수 없습니다. 자세한 내용은/*를 참조 하세요. [ / \*(주석)](../mdx/comment-mdx.md).  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Mdx 구문 요소 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
