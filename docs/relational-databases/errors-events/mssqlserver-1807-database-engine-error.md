---
title: "MSSQLSERVER_1807 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6042f6788352b1dae1e7922c9e3e3ba59eefb91f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1807|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|CANNOT_EX_LOCK|  
|메시지 텍스트|데이터베이스 '%.*ls'에 대한 배타적 잠금을 얻을 수 없습니다. 나중에 작업을 다시 시도하십시오.|  
  
## <a name="explanation"></a>설명  
데이터베이스에 대한 단독 액세스를 필요로 하는 작업에서 배타적 잠금을 얻을 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
해당 데이터베이스에 대한 모든 연결을 끊거나 나중에 쿼리를 다시 시도하십시오.  
  
