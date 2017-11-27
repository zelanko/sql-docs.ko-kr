---
title: IsEmpty (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISEMPTY
dev_langs:
- kbMDX
helpviewer_keywords:
- IsEmpty function
ms.assetid: b4a50996-61d1-4e23-8003-7d530195ea72
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 09475a39c4f83044b0f169f99c894801392cba7e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="isempty-mdx"></a>IsEmpty(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  평가 식이 빈 셀 값인지 여부를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>인수  
 *Value_Expression*  
 일반적으로 멤버나 튜플의 셀 좌표를 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>주의  
 **IsEmpty** 함수에서 반환 **true** 평가 식이 빈 셀 값이 있습니다. 그렇지 않으면이 함수가 반환 **false**합니다.  
  
> [!NOTE]  
>  멤버의 기본 속성은 멤버의 값입니다.  
  
 **IsEmpty** 함수는 빈 셀 값에서 특별 한 의미를 갖기 때문에 빈 셀에 대 한 안정적으로 테스트할 수 있는 유일한 방법은 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다.  
  
> [!IMPORTANT]  
>  경우 값 식의 평가 결과 오류가 반환 되는 함수는 반환 **false**합니다. 예를 들어 속성 참조가 잘못된 속성이나 존재하지 않는 속성을 참조하는 경우 값 식에서 오류가 반환될 수 있습니다.  
  
 빈 셀에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예에서는 Date 차원의 Fiscal 계층에 있는 현재 멤버에 대한 Internet Sales Amount가 빈 셀을 반환하는 경우 TRUE를 반환합니다.  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>관련 항목:  
 [빈 값 작업](../mdx/working-with-empty-values.md)   
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

