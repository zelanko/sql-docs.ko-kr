---
title: MSSQLSERVER_7913 | Microsoft 문서
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
- 7913 (Database Engine error)
ms.assetid: 9d8ad456-b1a2-4f79-a252-657fbec9ad9b
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3e7f5b24d0c2eed407324e5947c7ba5cf08f9e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7913"></a>MSSQLSERVER_7913
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7913|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_REPAIR_EXTENT_DEALLOCATED|  
|메시지 텍스트|복구: 익스텐트 P_ID이(가) 개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 단위 ID A_ID(TYPE 유형)에서 할당 취소되었습니다.|  
  
## <a name="explanation"></a>설명  
익스텐트가 지정된 개체에서 할당 취소되었음을 나타내는 REPAIR의 정보 메시지입니다.  
  
## <a name="user-action"></a>사용자 동작  
InclusionThresholdSetting  
  
