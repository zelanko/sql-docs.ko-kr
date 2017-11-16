---
title: "MSSQLSERVER_8966 | Microsoft 문서"
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
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4c93290eaf142f7048458d9e4a18d12bc70e028b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8966|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|메시지 텍스트|래치 유형이 TYPE인 페이지 P_ID을(를) 읽어 래치할 수 없습니다. OPERATION이(가) 실패했습니다.|  
  
## <a name="explanation"></a>설명  
페이지를 읽지 못했거나 PFS 또는 GAM 페이지에서 래치를 가져올 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 래치 제한 시간 또는 다른 관련 메시지가 있을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
SQL 오류 로그에서 관련 메시지를 살펴보고 오류를 해결하십시오.  
  

