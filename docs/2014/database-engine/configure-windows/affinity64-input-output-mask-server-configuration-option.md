---
title: affinity64 I/O mask 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7449be34c7697f770b18357c465da41cd57164b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210163"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 Input-Output mask 서버 구성 옵션
  **affinity64 I/O mask** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] affinity I/O mask **옵션과 유사한 방식으로** 디스크 I/O를 지정한 CPU 하위 집합으로 바인딩합니다. **affinity I/O mask** 를 사용하여 처음 32개의 프로세서를 바인딩한 다음 **affinity64 I/O mask** 를 사용하여 컴퓨터의 남은 프로세서를 바인딩하세요. **affinity64 I/O mask**를 다시 구성하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작해야 합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]64비트 버전에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [선호도 입력-출력 마스크 서버 구성 옵션](affinity-input-output-mask-server-configuration-option.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
