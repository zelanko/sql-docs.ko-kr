---
title: "SqlToolsVSNativeHelpers | Microsoft 문서"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
caps.latest.revision: "5"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59c3761c6baca8e622d90dc0535608f624eacf0f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="sqltoolsvsnativehelpers"></a>SqlToolsVSNativeHelpers
  Visual Studio에서 SQL Server 기능을 지원하는 라이브러리입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID /*lpReserved*/)  
```  
  
## <a name="return-value"></a>반환 값  
 DLL 진입점이 올바르게 초기화된 경우 부울 값 **True** 이고, 그렇지 않으면 **False**입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [FrameWindowVisible](../relational-databases/sqltoolsvsnativehelpers-framewindowvisible.md)  
  
  
