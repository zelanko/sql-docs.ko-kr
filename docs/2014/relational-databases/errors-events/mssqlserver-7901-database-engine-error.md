---
title: MSSQLSERVER_7901 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b07984eb30c39ade07f9a18855eff8cadcac77ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187196"
---
# <a name="mssqlserver7901"></a>MSSQLSERVER_7901
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7901|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|메시지 텍스트|복구 문이 처리되지 않았습니다. 데이터베이스가 응급 모드인 경우 이 복구 수준은 지원되지 않습니다.|  
  
## <a name="explanation"></a>설명  
 데이터베이스가 응급 모드이며 REPAIR_ALLOW_DATA_LOSS 이외의 복구 수준이 지정되었습니다. REPAIR_ALLOW_DATA_LOSS를 지정하지 않는 한 응급 모드에서는 복구할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 명령을 다시 실행하고 REPAIR_ALLOW_DATA_LOSS 옵션을 지정합니다.  
  
  