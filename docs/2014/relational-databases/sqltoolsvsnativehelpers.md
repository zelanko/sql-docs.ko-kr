---
title: SqlToolsVSNativeHelpers | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 847423f199a321c0af29c46528041980f06f3488
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48223807"
---
# <a name="sqltoolsvsnativehelpers"></a>SqlToolsVSNativeHelpers
  Visual Studio에서 SQL Server 기능을 지원하는 라이브러리입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID /*lpReserved*/)  
```  
  
## <a name="return-value"></a>반환 값  
 DLL 진입점이 올바르게 초기화된 경우 부울 값 `True`이고, 그렇지 않으면 `False`입니다.  
  
## <a name="see-also"></a>관련 항목  
 [FrameWindowVisible](sqltoolsvsnativehelpers-framewindowvisible.md)  
  
  
