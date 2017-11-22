---
title: (String) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Members
dev_langs: kbMDX
helpviewer_keywords: Members function
ms.assetid: 21fca354-448b-4b05-93f4-111bde1568f1
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 86f1471db7ccf4314ed59defdb1cd1b183c4e60d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="members-string-mdx"></a>Members(문자열)(MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  문자열 식으로 지정된 멤버를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Name*  
 멤버 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 **(String)** 함수 이름이 지정 된 단일 멤버를 반환 합니다. 일반적으로 사용 된 **(String)** 함수를 제공 하는 외부 함수와 함께 **(String)** 함수에 멤버를 식별 하는 문자열 및 **(String)** 지정 된이 멤버 함수는 값을 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 **(String)** 함수 지정된 된 문자열을 유효한 멤버로 변환한 한 다음 문자열에 지정 된 멤버에 대 한 기본 측정값을 반환 합니다. 지정된 문자열은 작은따옴표 안에 있습니다. 기본 측정값은 Reseller Sales Amount 측정값입니다.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
