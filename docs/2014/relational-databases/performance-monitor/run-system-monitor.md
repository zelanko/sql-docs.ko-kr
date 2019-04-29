---
title: 시스템 모니터 실행 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5516ee5200f6af36461184cc095992ac4d288722
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032117"
---
# <a name="run-system-monitor"></a>시스템 모니터 실행
  시스템 모니터는 RPC(원격 프로시저 호출)를 사용하여 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 정보를 수집할 수 있습니다. Microsoft Windows에서 시스템 모니터를 실행할 권한을 가진 모든 사용자는 시스템 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 모니터링할 수 있습니다.  
  
> [!NOTE]  
>  시스템 모니터 또는 성능 모니터를 사용하면 Windows 98에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 연결할 수 없습니다.  
  
 시스템 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 모니터링하면 다른 성능 모니터링 도구로 모니터링할 때와 마찬가지로 성능 오버헤드가 발생할 수 있습니다. 특정 인스턴스에서 실제 오버헤드의 발생 여부는 하드웨어 플랫폼, 카운터 수, 선택된 업데이트 간격에 따라 결정됩니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 시스템 모니터가 통합되면서 성능 감소를 최소화하도록 설계되었습니다.  
  
> [!NOTE]  
>  시스템 모니터 스냅인에서 모니터링할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 카운터를 선택했으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되지 않은 경우에도 해당 카운터를 볼 수 있습니다.  
  
 시스템 모니터를 시작하는 방법은 [시스템 모니터 시작&#40;Windows&#41;](../performance/start-system-monitor-windows.md)을 참조하세요.  
  
  
