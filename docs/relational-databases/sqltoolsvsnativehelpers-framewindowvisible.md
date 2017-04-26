---
title: "FrameWindowVisible | Microsoft 문서"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f09e83d79a913bb56042a5a48b832a940e0f9ea9
ms.lasthandoff: 04/11/2017

---
# <a name="sqltoolsvsnativehelpers---framewindowvisible"></a>SqlToolsVSNativeHelpers - FrameWindowVisible
  지정된 창 프레임이 표시되는지 여부를 지정하는 속성입니다. 도우미 메서드는 관리 코드에서 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL WINAPI IsFrameWindowVisible(IVsWindowFrame* frame)  
{  
    if (NULL == frame)  
    {  
        return FALSE;  
    }  
  
    return S_OK == frame->IsVisible();  
}  
```  
  
#### <a name="parameters"></a>매개 변수  
 *frame*  
  
 Visual Studio WindowFrame에 대한 IVsWindowFrame* 포인터입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 *frame* 으로 지정된 창 프레임이 표시되는지 여부를 지정하는 부울 값입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SqlToolsVSNativeHelpers](../relational-databases/sqltoolsvsnativehelpers.md)  
  
  
