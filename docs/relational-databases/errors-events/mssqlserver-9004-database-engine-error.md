---
title: "MSSQLSERVER_9004 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6d2d5cefa8aa83b92f589d939f1c7c53b23b3f1f
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9004|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LOG_CORRUPT|  
|메시지 텍스트|데이터베이스 '%.*ls'의 로그를 처리하는 동안 오류가 발생했습니다.  가능하면 백업을 사용하여 복원하십시오. 백업이 없을 경우 로그를 다시 만들어야 합니다.|  
  
## <a name="explanation"></a>설명  
롤백, 복구 또는 복제 중 로그를 처리하는 동안 오류가 발생했습니다. 운영 체제에서 발견한 오류이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 발견한 내부 일관성 오류일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 오류를 수정하려면 다음 중 하나를 수행하십시오.  
  
-   백업에서 복원합니다.  
  
-   로그를 다시 작성합니다.  
  
또한 시스템 이벤트나 오류 로그를 검사하여 문제를 일으킬 수 있는 시스템 내의 문제를 파악하십시오.  
  

