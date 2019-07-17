---
title: CALL 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: de74590ac4c43a9141c0ab2092babf41ffd23ba5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106298"
---
# <a name="mdx-data-manipulation---call"></a>MDX 데이터 조작 - CALL


  현재 범위 또는 지정된 큐브에서 void를 반환하는 저장 프로시저를 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CALL SP_Name   
   [ (SP_Argument   
      [, SP_Argument ,...n]  
      ) ]   
[ONCube_Expression]  
```  
  
## <a name="arguments"></a>인수  
 *SP_Name*  
 저장 프로시저의 이름을 지정하는 유효한 문자열 식입니다.  
  
 *SP_Argument*  
 호출된 저장 프로시저에 인수를 지정하는 유효한 문자열 식입니다.  
  
 *Cube_Expression*  
 큐브의 이름을 지정하는 유효한 문자열 큐브 식입니다.  
  
## <a name="remarks"></a>설명  
 합니다 **호출** 문은 필요에 따라 지정된 된 저장된 프로시저에 대 한 하나 이상의 인수를 포함 하 여 지정 된 등록 된 저장된 프로시저를 실행 합니다. 합니다 **호출** 문을 void를 반환 하는 저장된 프로시저에만 사용 됩니다. 이 문은 MDX 식 내의 다른 함수 또는 연산자와 조합될 수 없습니다. 값을 반환하는 등록된 저장 프로시저는 MDX 식 내에서 직접 호출될 수 있으며 다른 MDX 함수 및 연산자와 조합될 수 있습니다.  
  
 큐브가 지정되지 않은 경우 이 문은 현재 큐브에서 저장 프로시저를 실행합니다.  
  
> [!NOTE]  
>  클라이언트에서 저장된 프로시저를 등록 하지 않은 경우는 **호출** 문에서 인스턴스에서 저장된 프로시저를 호출 하려고 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 조작 문 &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [저장 프로시저 사용 &#40;MDX&#41;](../mdx/using-stored-procedures-mdx.md)  
  
  
