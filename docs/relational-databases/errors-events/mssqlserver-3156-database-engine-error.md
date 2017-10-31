---
title: "MSSQLSERVER_3156 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 08f8ea872ef58a42b07254417db0a19a5dfd9fd7
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3156"></a>MSSQLSERVER_3156
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3156|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_CANT_WRITE|  
|메시지 텍스트|파일 '%ls'을(를) '%ls'(으)로 복원할 수 없습니다. WITH MOVE를 사용하여 올바른 파일 위치를 확인하십시오.|  
  
## <a name="explanation"></a>설명  
이 일반적인 메시지는 지정된 위치와 관련된 문제로 인해 복원할 수 없는 논리적 또는 물리적 파일 이름을 식별합니다.  
  
### <a name="possible-causes"></a>가능한 원인  
가능한 원인은 다음과 같습니다.  
  
-   지정된 Windows 디렉터리에 대한 액세스 권한이 없을 수 있습니다.  
  
-   경로를 잘못 입력했거나 존재하지 않는 경로를 지정했을 수 있습니다.  
  
-   해당 파일 이름이 덮어쓸 수 없는 파일에 사용되고 있을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
자세한 내용은 오류 로그에서 다른 메시지를 참조하십시오.  
  
액세스 권한을 부여하거나 RESTORE 문에 WITH MOVE 옵션을 사용하는 방법으로 파일의 위치를 다시 지정하여 지정된 위치와 관련된 문제를 수정합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[새 위치로 파일 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  

