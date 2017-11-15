---
title: "SMO and DMO XPs 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26b79d125d64a1c262c28b71d4c17bbc1824bf6f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SMO 및 DMO XP 옵션을 사용하여 현재 서버에서 SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object) 확장 저장 프로시저를 사용하도록 설정할 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 DMO는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거되었습니다.  
  
 다음 표에서는 이 옵션에 사용할 수 있는 값을 설명합니다.  
  
|값|의미|  
|-----------|-------------|  
|0|SMO XP를 사용할 수 없습니다.|  
|1|SMO XP를 사용할 수 있습니다. 기본값입니다.|  
  
 이 설정은 즉시 적용됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 SMO 확장 저장 프로시저를 사용하도록 설정합니다.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [SMO&#40;SQL Server 관리 개체&#41; 프로그래밍 가이드](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
