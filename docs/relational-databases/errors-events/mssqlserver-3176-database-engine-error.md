---
title: "MSSQLSERVER_3176 | Microsoft 문서"
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
helpviewer_keywords: 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 27a1dc96d923e1958c5b914ff55c8ea81417e860
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3176|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_FILE_CLAIM|  
|메시지 텍스트|'%ls'(%d) 및 '%ls'(%d)에서 파일 '%ls'을(를) 요구했습니다. WITH MOVE 절을 사용하여 하나 이상의 파일 위치를 다시 지정할 수 있습니다.|  
  
## <a name="explanation"></a>설명  
파일을 두 가지 이상의 용도로 사용하려고 합니다.  
  
### <a name="possible-causes"></a>가능한 원인  
다른 데이터베이스에서 이미 파일 이름을 사용하고 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
데이터베이스 파일을 다른 위치로 복원합니다. RESTORE 문에서 WITH MOVE 절을 사용하여 각 파일을 이동합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **데이터베이스 복원 옵션** 대화 상자의 **데이터베이스 파일을 다음으로 복원** 표에서 파일 위치를 변경합니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[새 위치로 파일 복원&#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE&#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
