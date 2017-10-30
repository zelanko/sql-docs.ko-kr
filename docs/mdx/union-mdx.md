---
title: Union (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- functions [MDX], Union
ms.assetid: cc083455-8b3b-46af-bb55-1e238376f162
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d68afa2f9c424a0bb745ad2feaf781923eac624a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="union--mdx"></a>Union (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  두 집합의 합집합을 반환합니다. 필요에 따라 중복된 멤버를 포함할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Standard syntax  
Union(Set_Expression1, Set_Expression2 [,...n][, ALL])  
  
Alternate syntax 1  
Set_Expression1 + Set_Expression2 [+...n]  
  
Alternate syntax 2  
{Set_Expression1 , Set_Expression2 [,...n]}  
```  
  
## <a name="arguments"></a>인수  
 *집합 식 1*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *집합 식 2*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 이 함수는 2의 합집합을 반환 하거나 이상 지정 된 집합*합니다.* 표준 구문을 사용 하 여 및 대체 구문 1 기본적으로 중복 항목이 제거 됩니다. 표준 구문을 사용 하 여 사용 하는 **모든** 플래그는 조인 된 집합에서 중복 요소를 유지 합니다. 중복 항목은 집합의 뒷부분부터 삭제됩니다. 대체 구문 2를 사용하면 중복 항목이 항상 유지됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는의 동작을 보여 주기는 **Union** 각 구문을 사용 하 여 작동 합니다.  
  
### <a name="standard-syntax-duplicates-eliminated"></a>중복 항목을 제거하는 표준 구문  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="standard-syntax-duplicates-retained"></a>중복 항목을 유지하는 표준 구문  
  
```  
SELECT Union   
   ([Date].[Calendar Year].children  
   , {[Date].[Calendar Year].[CY 2002]}  
   , {[Date].[Calendar Year].[CY 2003]}  
   , ALL  
   ) ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-1-duplicates-eliminated"></a>중복 항목을 제거하는 대체 구문 1  
  
```  
SELECT   
   [Date].[Calendar Year].children   
   + {[Date].[Calendar Year].[CY 2002]}   
   + {[Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
### <a name="alternate-syntax-2-duplicates-retained"></a>중복 항목을 유지하는 대체 구문 2  
  
```  
SELECT   
   {[Date].[Calendar Year].children  
   , [Date].[Calendar Year].[CY 2002]  
   , [Date].[Calendar Year].[CY 2003]} ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [+ &#40; Union &#41; &#40; Mdx&#41;](../mdx/union-mdx-operator-reference.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

