---
title: xp_cmdshell 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a7feec1765cf6ffaa3e46a300a5155ae73fb13db
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934695"
---
# <a name="xp_cmdshell-server-configuration-option"></a>xp_cmdshell 서버 구성 옵션
  **xp_cmdshell** 옵션은 시스템 관리자가 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] xp_cmdshell **확장 저장 프로시저를 실행할 수 있는지 여부를 제어할 수 있도록 하는** 서버 구성 옵션입니다. 기본적으로 **xp_cmdshell** 옵션은 새 설치에서는 사용할 수 없도록 되어 있지만 다음 코드 예제에서 볼 수 있듯이 정책 기반 관리를 사용하거나 **sp_configure** 시스템 저장 프로시저를 실행하여 사용 가능하도록 할 수 있습니다.  
  
```  
-- To allow advanced options to be changed.  
EXEC sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXEC sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
