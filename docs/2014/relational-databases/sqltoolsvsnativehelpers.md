---
title: SqlToolsVSNativeHelpers | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 992f8288018fb248b14db13b2ed1104aeecab04d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63285554"
---
# <a name="sqltoolsvsnativehelpers"></a>SqlToolsVSNativeHelpers
  Visual Studio에서 SQL Server 기능을 지원하는 라이브러리입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID /*lpReserved*/)  
```  
  
## <a name="return-value"></a>Return Value  
 DLL 진입점이 올바르게 초기화된 경우 부울 값 `True`이고, 그렇지 않으면 `False`입니다.  
  
## <a name="see-also"></a>참고 항목  
 [FrameWindowVisible](sqltoolsvsnativehelpers-framewindowvisible.md)  
  
  
