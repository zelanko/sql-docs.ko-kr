---
title: "튜플 함수를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: tuple functions
ms.assetid: fe41e3e5-a675-4169-a966-b42c18e8d741
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6131dbf1be847ca738b896fee36f56cd438f4715
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="using-tuple-functions"></a>튜플 함수 사용
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  튜플 함수는 집합에서 튜플을 검색하거나 튜플의 문자열 표현을 확인하여 튜플을 검색합니다.  
  
 튜플 함수는 멤버 함수 및 집합 함수와 마찬가지로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 사용되는 다차원 구조를 처리하는 데 필수적입니다.  
  
 세 가지 튜플 함수가 mdx에서 [현재 &#40; Mdx&#41; ](../mdx/current-mdx.md), [항목 &#40; 튜플 &#41; &#40; Mdx&#41; ](../mdx/item-tuple-mdx.md) 및 [StrToTuple &#40; Mdx&#41; ](../mdx/strtotuple-mdx.md). 다음 예제 쿼리에서는 이러한 각 튜플 함수를 사용하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [함수 &#40; MDX 구문 &#41;](../mdx/functions-mdx-syntax.md)   
 [멤버 함수를 사용 하 여](../mdx/using-member-functions.md)   
 [집합 함수 사용](../mdx/using-set-functions.md)  
  
  
