---
title: 미러링 상태(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- PENDING_FAILOVER state
- mirroring states [SQL Server]
- DISCONNECTED state
- SYNCHRONIZING state
- SYNCHRONIZED state
- SUSPENDED state
- database mirroring [SQL Server], states
ms.assetid: 90062917-74f9-471b-b49e-bc153ae1a468
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e3e3756f65baa7e1b62e3a84ff709a60b9c887b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754549"
---
# <a name="mirroring-states-sql-server"></a>미러링 상태(SQL Server)
  데이터베이스 미러링 세션 동안 미러된 데이터베이스는 항상 특정 상태( *미러링 상태*)가 됩니다. 이러한 데이터베이스의 상태는 통신 상태, 데이터 흐름 및 파트너 간의 데이터 차이를 반영합니다. 데이터베이스 미러링 세션은 주 데이터베이스와 같은 상태가 됩니다.  
  
 데이터베이스 미러링 세션 동안 서버 인스턴스는 서로를 모니터링합니다. 파트너는 미러링 상태를 사용하여 데이터베이스를 모니터링합니다. PENDING_FAILOVER 상태를 제외하고 주 데이터베이스와 미러 데이터베이스는 항상 동일한 상태입니다. 세션에 미러링 모니터 서버가 설정되어 있으면 각 파트너는 연결 상태(CONNECTED 또는 DISCONNECTED)를 사용하여 미러링 모니터 서버를 모니터링합니다.  
  
 가능한 데이터베이스 미러링 상태는 다음과 같습니다.  
  
|미러링 상태|Description|  
|---------------------|-----------------|  
|SYNCHRONIZING|미러 데이터베이스의 내용이 주 데이터베이스의 내용보다 오래된 것입니다. 주 서버에서 로그 레코드를 미러 서버로 보내면 미러 서버에서 변경 내용을 미러 데이터베이스에 적용하여 롤포워드합니다.<br /><br /> 데이터베이스 미러링 세션의 시작 부분에서는 데이터베이스가 SYNCHRONIZING 상태입니다. 주 서버에서 데이터베이스를 제공하고 미러 서버는 계속 동기화를 시도합니다.|  
|SYNCHRONIZED|미러 서버가 주 서버와 충분히 동기화되면 미러링 상태가 SYNCHRONIZED로 변경됩니다. 주 서버에서 계속 변경 내용을 미러 서버로 보내고 미러 서버에서 계속 변경 내용을 미러 데이터베이스에 적용하면 데이터베이스는 이 상태로 유지됩니다.<br /><br /> 트랜잭션 보안을 FULL로 설정하면 SYNCHRONIZED 상태에서 자동 장애 조치(Failover)와 수동 장애 조치가 모두 지원되며 장애 조치 후 데이터가 손실되지 않습니다.<br /><br /> 트랜잭션 보안을 해제하면 SYNCHRONIZED 상태에서도 항상 일부 데이터가 손실될 수 있습니다.|  
|SUSPENDED|데이터베이스의 미러 복사본을 사용할 수 없습니다. 주 데이터베이스가 미러 서버에 로그를 보내지 않은 상태로 실행되고 있으며 이러한 상태를 *노출 실행*이라고 합니다. 이는 장애 조치(Failover) 이후의 상태입니다.<br /><br /> 다시 실행 오류가 발생하거나 관리자가 세션을 일시 중지한 경우에도 세션이 SUSPENDED 상태가 될 수 있습니다.<br /><br /> SUSPENDED는 파트너 종료 및 시작 후에도 유지되는 영구 상태입니다.|  
|PENDING_FAILOVER|이 상태는 장애 조치가 시작되었지만 미러 역할로 전환되지 않은 주 서버에서만 나타납니다.<br /><br /> 장애 조치가 시작되면 주 데이터베이스는 PENDING_FAILOVER 상태가 되고 모든 사용자 연결을 신속하게 종료한 후 즉시 미러 역할을 수행합니다.|  
|DISCONNECTED|해당 파트너와 다른 파트너의 통신이 끊어진 상태입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
