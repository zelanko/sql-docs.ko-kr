---
title: CLEAR CALCULATIONS 문 (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f210f2ad8af7b0d4e71482946a496d326fe63f24
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579785"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>CLEAR CALCULATIONS-MDX 데이터 조작
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  큐브에서 모든 계산을 제거하고 큐브를 계산 패스 0으로 되돌립니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Expression*  
 유효한 MDX 큐브 식입니다.  
  
## <a name="remarks"></a>Remarks  
 **FROM** 큐브의 컨텍스트가 알려진 등에서 MDX 스크립트 경우 절을 생략할 수 있습니다.  
  
> [!NOTE]  
>  이 문은 서버 또는 데이터베이스 관리자나 큐브의 원본 데이터에 액세스할 수 있는 역할(즉, ReadSourceData=true인 역할)의 멤버만 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 조작 문 &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
