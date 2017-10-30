---
title: "DROP ACTION 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs:
- kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99866db174208e4d041e69cae3d3b520eefb8dba
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---drop-action"></a>MDX 데이터 정의-DROP 동작
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 큐브에서 특정 동작을 삭제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Action_Name*  
 삭제할 동작의 이름을 지정하는 유효한 문자열 식입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ACTION 문 &#40; 만들기 Mdx&#41;](../mdx/mdx-data-definition-create-action.md)   
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

