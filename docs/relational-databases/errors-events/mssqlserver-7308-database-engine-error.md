---
title: MSSQLSERVER_7308 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f67200d7489bf90102325cf3463b5ea58424f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7308|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|RMT_STA_DISABLED|  
|메시지 텍스트|OLE DB 공급자 '%ls'은(는) 단일 스레드 아파트 모드에서 실행되도록 구성되어 있으므로 분산 쿼리에 사용할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
STA(단일 스레드 아파트) 모드에서 실행되도록 구성된 OLE DB 공급자를 사용했습니다. STA(단일 스레드 아파트) 모드에서 실행되도록 구성된 OLE DB 공급자는 분산 쿼리에 사용할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 문제를 해결하려면 MTA(다중 스레드 아파트) 모드에서 실행되도록 OLE DB 공급자를 구성합니다. OLE DB 공급자가 MTA를 지원하지 않으며 MTA를 지원하는 버전으로 OLE DB 공급자를 업그레이드할 수 없는 경우 out-of-process를 실행하도록 OLE DB 공급자를 구성합니다. OLE DB 공급자가 MTA 또는 out-of-process 실행을 지원하는 경우 해당 OLE DB 공급자의 공급업체는 사용자에게 이를 알려줄 수 있어야 합니다.  
  
