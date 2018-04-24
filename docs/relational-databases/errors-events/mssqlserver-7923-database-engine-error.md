---
title: MSSQLSERVER_7923 | Microsoft 문서
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
- 7923 (Database Engine error)
ms.assetid: b09a95e2-0ffe-4847-aa77-51e6639259f6
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2015fe496e17e020904a1bf82706f45274bf107d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7923"></a>MSSQLSERVER_7923
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7923|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_SUMMARY_TABLE_NAME|  
|메시지 텍스트|테이블 TABLE                개체 ID O_ID.|  
  
## <a name="explanation"></a>설명  
DBCC CHECKALLOC 명령의 정보 메시지입니다. 테이블의 모든 할당 단위에 대한 할당 정보 목록을 포함하며 이 목록의 맨 위에 테이블 이름 및 ID가 표시됩니다.  
  
## <a name="user-action"></a>사용자 동작  
InclusionThresholdSetting  
  
