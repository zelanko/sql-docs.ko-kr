---
title: MSSQLSERVER_845 | Microsoft 문서
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
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2d9b231b6cf2152e825b07dc1e3e218815d9df1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver845"></a>MSSQLSERVER_845
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|845|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|BUFLATCH_TIMEOUT|  
|메시지 텍스트|데이터베이스 ID %d, 페이지 %S_PGID에 대한 버퍼 래치 유형 %d을(를) 기다리는 중 시간이 초과되었습니다.|  
  
## <a name="explanation"></a>설명  
프로세스에서 래치를 얻기 위해 기다렸지만 시간 제한이 초과되어 래치를 얻지 못했습니다. 이 오류는 일반적으로 시스템 프로세스를 차단하는 다른 태스크로 인해 I/O 작업을 완료하는 데 너무 많은 시간이 소요되는 경우 발생할 수 있습니다. 하드웨어 오류로 인해 이 오류가 발생하는 경우도 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
다음 태스크를 수행하면 이 오류를 방지할 수 있습니다.  
  
-   작업을 줄입니다.  
  
-   오류 로그나 이벤트 로그에 관련된 I/O 오류가 있는지 확인합니다. I/O 오류는 일반적으로 디스크 오류로 인해 발생합니다.  
  
-   오류 로그에 잠겨 있는 태스크 및 기타 오류가 있는지 확인합니다.  
  
-   어설션과 같은 오류가 자주 발생하면 이 문제를 해결하십시오.  
  
오류가 지속되면 Microsoft 고객 서비스 지원 센터에 문의하십시오.  
  
