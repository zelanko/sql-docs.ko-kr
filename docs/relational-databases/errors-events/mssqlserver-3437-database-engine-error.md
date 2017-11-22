---
title: "MSSQLSERVER_3437 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c8656cbd521e20e9b53bc845d714c57355fc9b9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3437|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|NODTC|  
|메시지 텍스트|데이터베이스 '%.*ls'을(를) 복구하는 중 오류가 발생했습니다. MS DTC(Microsoft Distributed Transaction Coordinator)에 연결하여 트랜잭션 %S_XID의 완료 상태를 확인할 수 없습니다. MS DTC를 수정하고 복구 작업을 다시 실행하십시오.|  
  
## <a name="explanation"></a>설명  
데이터베이스가 종료될 때 MS DTC([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator)를 사용하는 하나 이상의 분산 트랜잭션이 완전하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 트랜잭션을 완료하거나 롤백하기 위해 MS DTC에 연결할 수 없으므로 이 데이터베이스를 복구하지 못했습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 데이터베이스를 복구하려면 MS DTC 문제를 먼저 해결해야 합니다. MS DTC 문제를 확인하려면 Windows 이벤트 로그를 검사하십시오. MS DTC 문제를 해결할 수 없어 데이터베이스를 복구할 수 없는 경우 데이터베이스의 백업을 복원하십시오.  
  
