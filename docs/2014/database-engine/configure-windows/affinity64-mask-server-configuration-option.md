---
title: affinity64 mask 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- affinity64 mask option
- binding processors [SQL Server]
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d2ea6d2e364feaa67d91de0055617aac9dc285ab
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935944"
---
# <a name="affinity64-mask-server-configuration-option"></a>affinity64 mask 서버 구성 옵션
  affinity64 mask는 프로세서를 특정 스레드에 바인딩하며 affinity mask 옵션과 비슷합니다. 선호도 마스크를 사용하여 처음 32개 프로세서를 바인딩하고 affinity64 마스크를 사용하여 컴퓨터의 나머지 프로세서를 바인딩할 수 있습니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]64비트 버전에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)][ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)을 대신 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [선호도 마스크 서버 구성 옵션](affinity-mask-server-configuration-option.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
