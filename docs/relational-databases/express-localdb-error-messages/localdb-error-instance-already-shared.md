---
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e0d9f1c191c40aca1777942b738e9ec09a5f4a9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="localdberrorinstancealreadyshared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|284|  
|이벤트 원본|SQL Server 로컬 데이터베이스 런타임 12.0|  
|구성 요소|로컬 데이터베이스 런타임 API|  
|메시지 텍스트|지정된 로컬 데이터베이스 인스턴스는 이미 공유되어 있습니다.|  
  
## <a name="explanation"></a>설명  
 지정된 로컬 데이터베이스 인스턴스는 이미 다른 이름으로 공유되어 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 먼저 공유 인스턴스의 공유를 해제한 후 다른 공유 이름으로 다시 공유하십시오.  
  
  
