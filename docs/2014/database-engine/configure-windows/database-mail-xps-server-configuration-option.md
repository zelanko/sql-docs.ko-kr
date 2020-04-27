---
title: Database Mail XPs 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e916fe3b76abfa8773a757cf2779e7d5cbf26b86
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62810545"
---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XPs 서버 구성 옵션
  **DatabaseMail XPs** 옵션을 사용하여 서버에서 데이터베이스 메일을 활성화할 수 있습니다. 사용 가능한 값은  
  
-   **0** 은 데이터베이스 메일을 사용할 수 없음을 나타냅니다(기본값).  
  
-   **1** 은 데이터베이스 메일을 사용할 수 있음을 나타냅니다.  
  
 이 설정은 서버를 중지했다가 다시 시작하지 않아도 즉시 적용됩니다.  
  
 데이터베이스 메일을 활성화한 다음에는 데이터베이스 메일을 사용하도록 데이터베이스 메일 호스트 데이터베이스를 구성해야 합니다.  
  
 **데이터베이스 메일 구성 마법사** 를 사용하여 데이터베이스 메일을 구성하면 **msdb** 데이터베이스의 데이터베이스 메일 확장 저장 프로시저가 활성화됩니다. **데이터베이스 메일 구성 마법사**를 사용하는 경우 다음의 **sp_configure** 예를 사용할 필요가 없습니다.  
  
 **Database Mail XPs** 옵션을 0으로 설정하면 데이터베이스 메일을 시작할 수 없습니다. 옵션이 0인 상태에서 실행 중인 경우 **DatabaseMailExeMinimumLifeTime** 옵션에 구성된 시간 동안 유휴 상태가 될 때까지 계속 실행되면서 메일을 보냅니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 메일 확장 저장 프로시저를 활성화합니다.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
  
  
