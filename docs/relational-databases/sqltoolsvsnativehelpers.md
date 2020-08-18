---
description: SqlToolsVSNativeHelpers
title: SqlToolsVSNativeHelpers | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: d33cb556-0380-490a-9220-b74062dbd6d9
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2a367470a4f6ca7c8d6b3015ab45b77888bbab2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88324890"
---
# <a name="sqltoolsvsnativehelpers"></a>SqlToolsVSNativeHelpers
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
  Visual Studio에서 SQL Server 기능을 지원하는 라이브러리입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID /*lpReserved*/)  
```  
  
## <a name="return-value"></a>Return Value  
 DLL 진입점이 올바르게 초기화된 경우 부울 값 **True** 이고, 그렇지 않으면 **False**입니다.  
  
## <a name="see-also"></a>관련 항목  
 [FrameWindowVisible](../relational-databases/sqltoolsvsnativehelpers-framewindowvisible.md)  
  
  
