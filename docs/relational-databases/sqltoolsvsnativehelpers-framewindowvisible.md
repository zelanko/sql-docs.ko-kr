---
title: FrameWindowVisible | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c9bcce51781c0306946a7bb3cabe5363ccd55d1
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716654"
---
# <a name="sqltoolsvsnativehelpers---framewindowvisible"></a>SqlToolsVSNativeHelpers - FrameWindowVisible
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>참고 항목  
 [SqlToolsVSNativeHelpers](../relational-databases/sqltoolsvsnativehelpers.md)  
  
  
