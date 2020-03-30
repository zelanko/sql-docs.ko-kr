---
title: Database Mail XPs 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e16286e558d860a346ba8fff366009f064e65f91
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011963"
---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XPs 서버 구성 옵션

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**DatabaseMail XPs** 옵션을 사용하여 서버에서 데이터베이스 메일을 활성화할 수 있습니다. 사용 가능한 값은  
  
- `0`: 데이터베이스 메일을 사용할 수 없습니다(기본값).  
  
- `1`: 데이터베이스 메일을 사용할 수 있습니다.  
  
 이 설정은 서버를 중지했다가 다시 시작하지 않아도 즉시 적용됩니다.  
  
 데이터베이스 메일을 활성화한 다음에는 데이터베이스 메일을 사용하도록 데이터베이스 메일 호스트 데이터베이스를 구성해야 합니다.  
  
 **데이터베이스 메일 구성 마법사**를 사용하여 데이터베이스 메일을 구성하면 `msdb` 데이터베이스에서 데이터베이스 메일 확장 저장 프로시저가 활성화됩니다. **데이터베이스 메일 구성 마법사**를 사용하는 경우 다음의 `sp_configure` 예제를 사용할 필요가 없습니다.  
  
 **Database Mail XPs** 옵션을 `0`으로 설정하면 데이터베이스 메일을 시작할 수 없습니다. 옵션이 `0`으로 설정된 상태에서 실행 중인 경우 `DatabaseMailExeMinimumLifeTime` 옵션에 구성된 시간 동안 유휴 상태가 될 때까지 계속 실행되면서 메일을 보냅니다.  
  
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

다음 예제에서는 데이터베이스 메일 확장 저장 프로시저를 활성화합니다(아직 활성화되지 않은 경우).

```sql
IF EXISTS (
    SELECT 1 FROM sys.configurations 
    WHERE NAME = 'Database Mail XPs' AND VALUE = 0)
BEGIN
  PRINT 'Enabling Database Mail XPs'
  EXEC sp_configure 'show advanced options', 1;  
  RECONFIGURE
  EXEC sp_configure 'Database Mail XPs', 1;  
  RECONFIGURE  
END
```

## <a name="see-also"></a>참고 항목
[데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
