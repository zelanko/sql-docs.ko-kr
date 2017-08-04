---
title: "CLEAR CALCULATIONS 문 (MDX) | Microsoft Docs"
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
- CLEAR CALCULATIONS
- clalculations
- clear
dev_langs:
- kbMDX
helpviewer_keywords:
- clearing calculations
- CLEAR CALCULATIONS statement
- deleting calculations
- removing calculations
- calculations [Analysis Services], clearing
- cubes [Analysis Services], calculations
ms.assetid: aebec9a1-1d1d-4697-aa3f-cc2449625603
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 042c7b9bedc396d63aa70d23926728b015527a99
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-manipulation---clear-calculations"></a>CLEAR CALCULATIONS-MDX 데이터 조작
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  큐브에서 모든 계산을 제거하고 큐브를 계산 패스 0으로 되돌립니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Expression*  
 유효한 MDX 큐브 식입니다.  
  
## <a name="remarks"></a>주의  
 **FROM** 큐브의 컨텍스트가 알려진 등에서 MDX 스크립트 경우 절을 생략할 수 있습니다.  
  
> [!NOTE]  
>  이 문은 서버 또는 데이터베이스 관리자나 큐브의 원본 데이터에 액세스할 수 있는 역할(즉, ReadSourceData=true인 역할)의 멤버만 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDX 데이터 조작 문 &#40; Mdx&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  

