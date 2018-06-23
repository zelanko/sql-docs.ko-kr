---
title: MSSQLSERVER_1406 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 259d6e37f0798cfacaac39c89dec091053c16c57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082505"
---
# <a name="mssqlserver1406"></a>MSSQLSERVER_1406
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1406|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBM_BADSTATEFORFORCESERVICE|  
|메시지 텍스트|서비스를 안전하게 강제 실행할 수 없습니다. 액세스하려면 데이터베이스 미러링을 제거한 다음 데이터베이스 "%.*ls"을(를) 복구하십시오.|  
  
## <a name="explanation"></a>설명  
 미러링 상태에서 강제 서비스 프로세스가 제대로 동작하는지 보장할 수 없기 때문에 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 서비스를 강제 실행할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 데이터베이스 미러링을 제거합니다. 그런 다음 미러 데이터베이스를 복구하여 이 데이터베이스에 액세스할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링 세션에 서비스 강제 수행&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)   
 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  