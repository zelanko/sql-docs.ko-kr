---
title: FrameWindowVisible | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bacf2e0b9e109f36a29edb79d3e15aefe7aa1ce1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623111"
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
  
  
