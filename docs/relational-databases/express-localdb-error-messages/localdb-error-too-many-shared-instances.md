---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbade1092a7d7ba4ba84f7b2be98fd5535c603c0
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="localdberrortoomanysharedinstances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|287|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|공유 인스턴스가 너무 많아 고유한 사용자 인스턴스 이름을 생성할 수 없습니다. 기존 공유 인스턴스 중 일부의 공유를 해제하십시오.|  
  
## <a name="explanation"></a>설명  
 공유 인스턴스가 너무 많아 고유한 사용자 인스턴스 이름을 생성할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 하나 이상의 공유 로컬 데이터베이스 런타임 인스턴스의 공유를 해제하고 다시 시도하십시오.  
  
  
