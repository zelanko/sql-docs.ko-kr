---
title: MSSQLSERVER_1457 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f45545212b494f955c6b9be97ccf0df7efeb622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869915"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1457|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBM_PAGE_UNDO_PENDING|  
|메시지 텍스트|미러 데이터베이스 '%.*ls'의 동기화가 중단되어 데이터베이스가 일관성이 없는 상태가 되었습니다. ALTER DATABASE 명령이 실패했습니다. 미러 데이터베이스가 다시 켜져 온라인 상태인지 확인한 다음 미러 서버 인스턴스를 다시 연결하여 미러 데이터베이스의 동기화를 완료하십시오.|  
  
## <a name="explanation"></a>설명  
 이 메시지는 ALTER DATABASE *database_name* SET PARTNER OFF 문이 실패했음을 나타냅니다. 데이터베이스 미러링을 제거하려는 시도가 실패하여 미러 데이터베이스의 동기화가 중단되었습니다. 데이터베이스가 일관성이 없는 상태에 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 오류를 해결하려면 다음 동작 중 하나를 수행하십시오.  
  
-   미러 데이터베이스가 동기화되도록 미러 서버와 주 서버 간의 연결을 복원합니다.  
  
-   미러 데이터베이스를 삭제합니다.  
  
     미러 데이터베이스를 삭제한 후 백업에서 새 미러 데이터베이스를 만들 수 있습니다.  
  
    > [!NOTE]  
    >  SET PARTNER OFF 문이 실패한 후 미러링이 계속 활성화된 경우에만 미러 데이터베이스를 삭제할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
  
