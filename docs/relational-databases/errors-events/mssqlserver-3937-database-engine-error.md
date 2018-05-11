---
title: MSSQLSERVER_3937 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f02486a0a113f2e589a5f17d40344c374c1d853
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|MSSQLSERVER|  
|이벤트 ID|3937|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|XACT_FILESTREAM_ROLLBACK_ERROR|  
|메시지 텍스트|FILESTREAM 필터 드라이버로 트랜잭션이 롤백되었음을 알리는 동안 오류가 발생했습니다. 오류 코드: 0x%0x.|  
  
## <a name="explanation"></a>설명  
트랜잭션에 대한 롤백 알림을 실행하는 동안 RsFx 드라이버에서 오류가 반환되었습니다. 이 오류는 리소스 부족으로 인해 발생한 것 같습니다. 이로 인해 RsFx 필터 드라이버에서 약간의 메모리 누수가 발생할 수 있습니다. 하지만 트랜잭션을 만든 sqlservr.exe 프로세스가 종료되면 이 문제는 해결됩니다.  
  
## <a name="user-action"></a>사용자 동작  
