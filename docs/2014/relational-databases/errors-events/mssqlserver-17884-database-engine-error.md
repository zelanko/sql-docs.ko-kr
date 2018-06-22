---
title: MSSQLSERVER_17884 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8ea4b8825e1906c7c34b0ecb75d0857104816b62
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081349"
---
# <a name="mssqlserver17884"></a>MSSQLSERVER_17884
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|17884|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SRV_SCHEDULER_DEADLOCK|  
|메시지 텍스트|노드 %d의 프로세스에 할당된 새 쿼리가 최근 %d초 내에 작업자 스레드에 의해 선택되지 않았습니다. 차단 쿼리 또는 오래 실행되는 쿼리가 이 상황을 유발할 수 있으며 클라이언트 응답 시간을 저하시킬 수 있습니다. "max worker threads" 구성 옵션을 사용하여 허용 스레드 수를 늘리거나 현재 실행 중인 쿼리를 최적화하십시오.  SQL 프로세스 사용률: %d%%. 시스템 유휴 시간: %d%%.|  
  
## <a name="explanation"></a>설명  
 각 스케줄러에서 진행률 기호가 표시되지 않습니다. 이 오류는 스레드를 더 이상 진행할 수 없고 새 작업을 선택 및 처리할 수 없는 교착 상태로 인해 발생할 수 있습니다. 프로세스 사용률이 시스템에 있는 다른 프로세스보다 낮으면 서버 프로세스 CPU가 고갈될 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 차단이 발생하고 진행이 이루어지지 않는 원인을 확인하고 상황을 적절히 해결합니다. 프로세스 사용률이 낮으면 다른 프로세스에 의해 발생한 시스템 로드를 확인합니다.  
  
  