---
description: UserName(MDX)
title: UserName (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fbcc17cc34c6f4353698b918d0ab5ee3dc55701
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341139"
---
# <a name="username-mdx"></a>UserName(MDX)


  현재 연결의 도메인 이름과 사용자 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>설명  
 반환되는 값은 다음 형식의 문자열입니다.  
  
 *domain-name\user-name*  
  
## <a name="example"></a>예제  
 다음 예에서는 쿼리를 실행하는 사용자의 이름을 반환합니다.  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
