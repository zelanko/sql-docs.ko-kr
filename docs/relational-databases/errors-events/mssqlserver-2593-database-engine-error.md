---
title: MSSQLSERVER_2593 | Microsoft 문서
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
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f70235527f27e939acb5d493d199f8033570e360
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2593"></a>MSSQLSERVER_2593
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2593|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_OBJECT_ROW_PAGE_SUMMARY|  
|메시지 텍스트|PAGECOUNT개 페이지에 개체 'OBJECT'에 대한 행이 ROWCOUNT개 있습니다.|  
  
## <a name="explanation"></a>설명  
이 메시지는 DBCC CHECKALLOC을 제외한 모든 DBCC 검사에서 반환하는 출력 정보의 일부이며 지정된 개체의 행과 페이지 수를 나타냅니다.  
  
## <a name="user-action"></a>사용자 동작  
InclusionThresholdSetting  
  
