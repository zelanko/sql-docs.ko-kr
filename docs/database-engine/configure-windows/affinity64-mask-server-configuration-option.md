---
title: affinity64 mask 서버 구성 옵션 | Microsoft Docs
description: affinity64 mask 옵션에 대해 알아봅니다. 이 옵션을 SQL Server에서 사용하여 특정 스레드에 프로세서를 바인딩하는 경우를 확인합니다.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- affinity64 mask option
- binding processors [SQL Server]
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 452075955c30d7e49eb317f40bf377a6e894af29
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85631410"
---
# <a name="affinity64-mask-server-configuration-option"></a>affinity64 mask 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  affinity64 mask는 프로세서를 특정 스레드에 바인딩하며 affinity mask 옵션과 비슷합니다. 선호도 마스크를 사용하여 처음 32개 프로세서를 바인딩하고 affinity64 마스크를 사용하여 컴퓨터의 나머지 프로세서를 바인딩할 수 있습니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]64비트 버전에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)][ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)을 대신 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [선호도 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
