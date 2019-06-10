---
title: xp_cmdshell 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
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
manager: jroth
ms.openlocfilehash: 4679a937c99dcf4e58fa1b8184de48f189663980
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775044"
---
# <a name="xpcmdshell-server-configuration-option"></a>xp_cmdshell 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **xp_cmdshell** 옵션은 시스템 관리자가 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] xp_cmdshell **확장 저장 프로시저를 실행할 수 있는지 여부를 제어할 수 있도록 하는** 서버 구성 옵션입니다. 기본적으로 **xp_cmdshell** 옵션은 새로운 설치에서 사용할 수 없습니다. 이 옵션을 설정하기 전에 이 옵션의 사용과 관련된 잠재적 보안 문제를 고려해야 합니다. 새로 개발된 코드는 일반적으로 사용 안 함 상태이어야 하기 때문에 이 옵션을 사용하지 않아야 합니다. 일부 레거시 애플리케이션을 사용하도록 설정해야 합니다. 또한 이 옵션을 사용하지 않도록 수정할 수 없는 경우 다음 코드 예제에 표시된 대로 정책 기반 관리를 사용하거나 **sp_configure** 시스템 저장 프로시저를 실행하여 사용하도록 설정할 수 있습니다.  
  
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
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
