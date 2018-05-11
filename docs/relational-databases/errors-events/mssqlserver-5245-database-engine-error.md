---
title: MSSQLSERVER_5245 | Microsoft 문서
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
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d3f2dcaca260ceff3974585aa5c88b257e8f3d99
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|5245|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|메시지 텍스트|개체 ID O_ID(개체 'NAME'): 잠금 요청 제한 시간이 초과되었으므로 DBCC가 이 개체를 잠글 수 없습니다. 이 개체를 건너뛰었으므로 처리되지 않습니다.|  
  
## <a name="explanation"></a>설명  
DBCC가 지정된 개체에 대한 테이블을 잠그기 위해 기다리는 동안 잠금 제한 시간이 초과되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
DBCC 명령을 다시 실행하십시오.  
  
