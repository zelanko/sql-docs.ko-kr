---
title: SMO and DMO XPs 서버 구성 옵션 | Microsoft Docs
description: 서버에서 SMO(SQL Server 관리 개체) 확장 저장 프로시저를 사용하도록 설정하는 방법을 알아봅니다. "SMO 및 DMO XP" 구성 옵션에 대한 정보를 확인합니다.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a636f58ba3f7e9e178489e87af4dc3aa777fdbab
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773609"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO and DMO XPs 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SMO 및 DMO XP 옵션을 사용하여 현재 서버에서 SMO( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object) 확장 저장 프로시저를 사용하도록 설정할 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 DMO는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거되었습니다.  
  
 다음 표에서는 이 옵션에 사용할 수 있는 값을 설명합니다.  
  
|값|의미|  
|-----------|-------------|  
|0|SMO XP를 사용할 수 없습니다.|  
|1|SMO XP를 사용할 수 있습니다. 이것이 기본값입니다.|  
  
 설정은 즉시 적용됩니다.  
  
## <a name="examples"></a>예제  
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
  
  
