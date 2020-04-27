---
title: 업그레이드 하면 메시지 큐를 사용 하는 지연 업데이트 구독이 수정 됩니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c723050f9e860534c5298df9a487337e319ff91
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091409"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>업그레이드하면 메시지 큐를 사용하는 지연 업데이트 구독이 수정됩니다.
  업그레이드 관리자가 MSMQ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing)를 사용하는 지연 업데이트 구독이 하나 이상 있을 수 있음을 감지했습니다. 복제는 메시지 큐를 더 이상 지원하지 않습니다. 따라서 구독은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐를 사용하도록 수정됩니다.  
  
 **sql** 의 값만 허용됩니다. 메시지 큐를 사용하는 기존 게시는 업그레이드 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐를 사용하도록 수정됩니다. 메시지 큐를 사용하는 지연 업데이트에 종속된 애플리케이션의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 큐를 허용하도록 다시 작성해야 합니다. 지연 업데이트 구독에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "트랜잭션 복제를 위한 업데이트 가능 구독"을 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 업그레이드되는 동안 메시지 큐 서비스가 실행 중이면 업그레이드 후에 기존 메시지 큐 구독 큐가 제거됩니다.  
  
 메시지 큐 서비스가 실행되고 있지 않은 경우에는 업그레이드가 완료된 후에 큐를 수동으로 제거하십시오. 큐를 제거하는 방법은 Windows 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [복제 업그레이드 문제](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
