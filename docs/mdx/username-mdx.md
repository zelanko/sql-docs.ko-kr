---
title: UserName (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: UserName
dev_langs: kbMDX
helpviewer_keywords: UserName function
ms.assetid: ecae549b-5c5e-4483-84e6-b713cd297d7e
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bae918a1f7e275de78e4c321a3101e5443567723
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="username-mdx"></a>UserName(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 연결의 도메인 이름과 사용자 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>주의  
 반환되는 값은 다음 형식의 문자열입니다.  
  
 *도메인 이름 \ 사용자 이름*  
  
## <a name="example"></a>예제  
 다음 예에서는 쿼리를 실행하는 사용자의 이름을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 &#40; Mdx&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
