---
title: FrameWindowVisible | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
caps.latest.revision: 6
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 12d0e87d50f96dbd69973b5c196303d4286a5ec5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325563"
---
# <a name="framewindowvisible"></a>FrameWindowVisible
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
  

<!-- Necessary temporarily. GeneMi, 2018-05-01.
     But 'release-sql2014-migration' should win the Conflict Resolution later in May, because this will then be a good link!
## See Also  
 [SqlToolsVSNativeHelpers](sqltoolsvsnativehelpers.md)  
-->
  
  
