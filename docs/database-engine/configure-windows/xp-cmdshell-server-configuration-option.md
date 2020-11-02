---
title: xp_cmdshell 서버 구성 옵션
description: "\"xp_cmdshell\" 옵션에 대해 알아보세요. 이 옵션으로 SQL Server에서의 \"xp_cmdshell\" 확장 저장 프로시저 실행 여부를 제어하는 방법을 확인합니다. 옵션을 사용 설정하는 방법을 알아보세요."
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- xp_cmdshell
ms.assetid: c147c9e1-b81d-49c8-b800-3019f4d86a13
author: markingmyname
ms.author: maghan
ms.custom: contperfq4
ms.date: 06/12/2020
ms.openlocfilehash: 004a7b0a50a657632bb2b9970f0558857d416494
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257976"
---
# <a name="xp_cmdshell-server-configuration-option"></a>xp_cmdshell 서버 구성 옵션

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 문서에서는 **xp_cmdshell** SQL Server 구성 옵션을 사용 설정하는 방법을 설명합니다. 이 옵션은 시스템 관리자가 시스템에서 [xp_cmdshell 확장 저장 프로시저](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md) 실행 여부를 제어할 수 있게 합니다. 기본적으로 **xp_cmdshell** 옵션은 새로운 설치에서 사용할 수 없습니다.

이 옵션을 사용 설정하기 전에 잠재적 보안 문제를 고려해야 합니다.

- 새로 개발한 코드는 **xp_cmdshell** 저장 프로시저를 사용해선 안 되면 대부분의 경우 해제 상태를 유지합니다.
- 일부 레거시 응용 프로그램에서는 **xp_cmdshell** 를 사용하도록 설정해야 합니다. 이러한 저장 프로시저를 사용하지 않도록 수정할 수 없다면 아래 설명에 따라 사용 설정할 수 있습니다.

> [!NOTE]  
> **xp_cmdshell** 을 사용해야 하는 경우에는 이를 필요로 하는 실제 작업이 지속되는 기간에만 사용하는 것이 보안상 가장 좋습니다.

**xp_cmdshell** 을 사용 설정해야 한다면 아래 코드 예제와 같이 [정책 기반 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)를 사용하거나 **sp_configure** 시스템 저장 프로시저를 사용하면 됩니다.  
  
``` sql
-- To allow advanced options to be changed.  
EXECUTE sp_configure 'show advanced options', 1;  
GO  
-- To update the currently configured value for advanced options.  
RECONFIGURE;  
GO  
-- To enable the feature.  
EXECUTE sp_configure 'xp_cmdshell', 1;  
GO  
-- To update the currently configured value for this feature.  
RECONFIGURE;  
GO  
```  
  
## <a name="next-steps"></a>다음 단계

- [xp_cmdshell 확장 저장 프로시저](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)
- [서버 구성 옵션(SQL Server)](server-configuration-options-sql-server.md)
- [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
