---
title: 튜플 함수 사용 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 578192fa982b8bbf65527f4ff1d71b6595a2400d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251640"
---
# <a name="using-tuple-functions"></a>튜플 함수 사용


  튜플 함수는 집합에서 튜플을 검색하거나 튜플의 문자열 표현을 확인하여 튜플을 검색합니다.  
  
 튜플 함수는 멤버 함수 및 집합 함수와 마찬가지로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용되는 다차원 구조를 처리하는 데 필수적입니다.  
  
 세 가지 튜플 함수에 MDX [현재 &#40;MDX&#41;](../mdx/current-mdx.md)를 [항목 &#40;튜플&#41; &#40;MDX&#41; ](../mdx/item-tuple-mdx.md) 하 고 [StrToTuple &#40;&#41;](../mdx/strtotuple-mdx.md). 다음 예제 쿼리에서는 이러한 각 튜플 함수를 사용하는 방법을 보여 줍니다.  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of Years and Countries`  
  
 `SET MyTuples AS  [Date].[Calendar Year].[Calendar Year].MEMBERS * [Customer].[Country].[Country].MEMBERS`  
  
 `//Returns a string representation of that set using the Current and Generate functions`  
  
 `MEMBER MEASURES.CURRENTDEMO AS GENERATE(MyTuples, TUPLETOSTR(MyTuples.CURRENT), ", ")`  
  
 `//Retrieves the fourth tuple from that set and displays it as a string`  
  
 `MEMBER MEASURES.ITEMDEMO AS TUPLETOSTR(MyTuples.ITEM(3))`  
  
 `//Creates a tuple consisting of the measure Internet Sales Amount and the country Australia from a string`  
  
 `MEMBER MEASURES.STRTOTUPLEDEMO AS STRTOTUPLE("([Measures].[Internet Sales Amount]" + ", [Customer].[Country].&[Australia])")`  
  
 `SELECT{MEASURES.CURRENTDEMO,MEASURES.ITEMDEMO,MEASURES.STRTOTUPLEDEMO} ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목  
 [함수 &#40;MDX 구문&#41;](../mdx/functions-mdx-syntax.md)   
 [멤버 함수를 사용 하 여](../mdx/using-member-functions.md)   
 [집합 함수 사용](../mdx/using-set-functions.md)  
  
  
