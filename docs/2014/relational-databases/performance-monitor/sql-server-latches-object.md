---
title: SQL Server, Latches 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d0d9249a5cfb801e07a85132060bb4d1781346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63251096"
---
# <a name="sql-server-latches-object"></a>SQL Server, Latches 개체
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 **SQLServer: 래치** 개체는 래치 라고 하는 내부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 잠금을 모니터링 하는 카운터를 제공 합니다. 래치를 모니터링하면 사용자 동작 및 리소스 사용을 확인해 성능 병목 상태를 찾아낼 때 유용합니다.  
  
 이 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **래치** 카운터에 대해 설명합니다.  
  
|SQL Server Latches 카운터|Description|  
|---------------------------------|-----------------|  
|**평균 래치 대기 시간 (밀리초)**|기다린 래치 요청에 대한 밀리초 단위의 평균 래치 대기 시간입니다.|  
|**래치 대기/초**|즉시 충족시킬 수 없는 래치 요청 수입니다.|  
|**슈퍼 래치 수**|현재 SuperLatches인 래치 수입니다.|  
|**슈퍼 래치 강등/초**|마지막 1초 동안 일반 래치로 강등된 SuperLatches 수 입니다.|  
|**슈퍼 래치 프로 모션/초**|마지막 1초 동안 SuperLatches로 승격된 래치 수입니다.|  
|**총 래치 대기 시간 (ms)**|마지막 1초 동안 기다렸던 래치 요청에 대한 밀리초 단위의 총 래치 대기 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
