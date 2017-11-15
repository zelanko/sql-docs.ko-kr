---
title: "in-doubt xact resolution 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9fd01be5efcc847708bb7f12f2e9eb5e83a1806f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>in-doubt xact resolution 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **미결 트랜잭션 확인** 옵션을 사용하여 MS DTC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator)가 해결할 수 없는 트랜잭션의 기본 결과를 조정합니다. MS DTC가 꺼진 경우나 복구 시 알 수 없는 트랜잭션 결과가 있는 경우에는 트랜잭션을 해결할 수 없습니다.  
  
 다음 표에서는 미결 트랜잭션을 해결하기 위한 가능한 결과 값 목록을 보여 줍니다.  
  
|결과 값|설명|  
|-------------------|-----------------|  
|0|가정 없음. MS DTC가 미결 트랜잭션을 해결할 수 없으면 복구에 실패합니다.|  
|1|커밋 가정. 모든 MS DTC 미결 트랜잭션을 커밋된 것으로 가정합니다.|  
|2|중단 가정. 모든 MS DTC 미결 트랜잭션을 중단된 것으로 가정합니다.|  
  
 종료 시간이 연장되지 않게 하려면 관리자는 다음 예와 같이 이 옵션을 선택하여 커밋을 가정하거나 중단을 가정하도록 구성할 수 있습니다.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 2 -– presume abort  
GO  
RECONFIGURE  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 또한 관리자는 다음 예와 같이 기본값(가정 없음)을 유지하고 DTC 실패에 대해 알리기 위해 복구에 실패하도록 할 수 있습니다.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 1 -– presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE –- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 –- back to no assumptions  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 **미결 트랜잭션 확인** 옵션은 고급 옵션입니다. **sp_configure** 시스템 저장 프로시저를 사용하여 설정을 변경하는 경우 **고급 옵션 표시** 를 1로 설정할 때만 **미결 트랜잭션 확인** 을 변경할 수 있습니다. 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
> [!NOTE]  
>  모든 분산 트랜잭션에 관련된 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 이 옵션을 일관되게 구성하면 데이터 불일치를 방지할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
