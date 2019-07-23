---
title: MSSQLSERVER_3431 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 921dde33b466cf9f72a8254f304d2a0abd739f7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132386"
---
# <a name="mssqlserver3431"></a>MSSQLSERVER_3431
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3431|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|UNRESOLVED_XACT|  
|메시지 텍스트|해결되지 않은 트랜잭션 결과로 인해 데이터베이스 '%.*ls'(데이터베이스 ID %d)을(를) 복구할 수 없습니다. MS DTC(Microsoft Distributed Transaction Coordinator) 트랜잭션이 준비되었지만 문제를 해결할 수 없습니다. 문제를 해결하려면 MS DTC를 수정하거나, 전체 백업에서 데이터베이스를 복원하거나, 데이터베이스를 복구하십시오.|  
  
## <a name="explanation"></a>설명  
데이터베이스가 종료될 때 MS DTC([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator)를 사용하는 하나 이상의 분산 트랜잭션이 완전하지 않습니다. MS DTC의 자세한 정보 없이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 트랜잭션을 완료하거나 롤백할 수 없으므로 이 데이터베이스를 복구할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 데이터베이스를 복구하려면 MS DTC 문제를 먼저 해결해야 합니다. MS DTC 문제를 확인하려면 Windows 이벤트 로그를 검사하십시오. MS DTC 문제를 해결할 수 없어 데이터베이스를 복구할 수 없는 경우 데이터베이스의 백업을 복원하십시오.  
  
